---
title : "Integrate with Github Actions"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 2.4 </b> "
---

**Github Actions**

You can leverage GitHub Actions to run automated scans for every build or specific builds, such as the ones that merge into the master branch. This action can alert on misconfigurations, or block code from being merged if certain policies are violated. Results can also be sent to Prisma Cloud and other sources for further review and remediation steps.

Let's begin by setting an action from the repository page, under the `Actions` tab. Then click on `set up a workflow yourself` -> to create a new action from scratch.

![24][1]

Name the file `checkov.yaml` and add the following code snippet into the editor.

```sh
name: checkov
on:
  pull_request:
  push:
    branches:
      - main
jobs:
  scan:
    runs-on: ubuntu-latest
    permissions:
      contents: read # for actions/checkout to fetch code
      security-events: write # for GitHub/codeql-action/upload-sarif to upload SARIF results

    steps:
    - uses: actions/checkout@v2

    - name: Run checkov
      id: checkov
      uses: bridgecrewio/checkov-action@master
      with:
        directory: code/
        #soft_fail: true
        #api-key: ${{ secrets.BC_API_KEY }}
      #env:
        #PRISMA_API_URL: https://api4.prismacloud.io

    - name: Upload SARIF file
      uses: GitHub/codeql-action/upload-sarif@v2

      # Results are generated only on a success or failure
      # this is required since GitHub by default won't run the next step
      # when the previous one has failed. Alternatively, enable soft_fail in checkov action.
      if: success() || failure()
      with:
        sarif_file: results.sarif

```

Once complete, click `Commit changes`... at the top right, then select `commit directly to the main branch` and click `Commit changes`. ![24][2]

Verify that the action is running (or has run) by navigating back to the `Actions` tab. ![24][3]

View the results of the run by clickiing on the Create `checkov.yaml` link. ![24][4]

Notice the policy violations that were seen earlier in CLI/Cloud9 are now displayed here. However, this is not the only place they are sent...

**View results in Github Security**

Checkov natively supports SARIF format and generates this output by default. GitHub Security accepts SARIF for uploading security issues. The GitHub Action created earlier handles the plumbing between the two.

Navigate to the `Security` tab in GitHub, the click Code `scanning `from the left sidebar or `View alerts` in the **Security overview > Code scanning** alerts section. ![24][5]

The security issues found by checkov are surfaced here for developers to get actionable feedback on the codebase they are working in without having to leave the platform. ![24][6]

**Tag and Trace with Yor**

[Yor](https://yor.io/) is another open source tool that can be used for tagging and tracing IaC resources from code to cloud. For example, yor can be used to add git metadata and a unique hash to a terraform resource; this can be used to better manage resource lifecycles, improve change management, and ultimately to help tie code defintions to runtime configurations.

Create new file in the GitHub UI under the path `.github/workflows/yor.yaml`. ![24][7]

Add the following code snippet:

```sh
name: IaC tag and trace

on:
  push:
  pull_request:

jobs:
  yor:
    runs-on: ubuntu-latest
    permissions:
      contents: write

    steps:
      - uses: actions/checkout@v2
        name: Checkout repo
        with:
          fetch-depth: 0
      - name: Run yor action
        uses: bridgecrewio/yor-action@main

```

This time, click `Commit changes...` at the top right, then select `Create a new branch `and click `Propose changes`. Click `Create pull request` on the next screen. ![24][8]

Check that the action is running, queued, or finished under the `Actions` tab. ![24][11] ![24][12]


More importanly, look at what yor updated by following the commit history and viewing any `.tf `file in the `code/` directory. ![24][13]

Notice the yor_trace tag? This can be used track "drift" between IaC definitons and runtime configurations.

**Branch Protection Rules**

Using Branch Protection Rules allows for criteria to be set in order for pushes and pull requests to be merged to a given branch. This can be set up to run checkov and block merges if there are any misconfigurations or vulnerabilities.

Within Github, go to the `Settings` tab and navigate to `Branches` on the left sidebar, then click `Add branch protection rule`. ![24][14]

Enter **main** as the **Branch name pattern**. Then select **Require status checks to pass before merging**, search for **checkov** in the provided search bar and select it as a required check. Leave the rest as default (unchecked), then click **Create**. ![24][15] ![24][16] ![24][17] 




[1]: /ws02/images/2/24/1.png?featherlight=false&width=50pc
[2]: /ws02/images/2/24/2.png?featherlight=false&width=50pc
[3]: /ws02/images/2/24/3.png?featherlight=false&width=50pc
[4]: /ws02/images/2/24/4.png?featherlight=false&width=50pc
[5]: /ws02/images/2/24/5.png?featherlight=false&width=50pc
[6]: /ws02/images/2/24/6.png?featherlight=false&width=50pc
[7]: /ws02/images/2/24/7.png?featherlight=false&width=50pc
[8]: /ws02/images/2/24/8.png?featherlight=false&width=50pc
[9]: /ws02/images/2/24/9.png?featherlight=false&width=50pc
[10]: /ws02/images/2/24/10.png?featherlight=false&width=50pc
[11]: /ws02/images/2/24/11.png?featherlight=false&width=50pc
[12]: /ws02/images/2/24/12.png?featherlight=false&width=50pc
[13]: /ws02/images/2/24/13.png?featherlight=false&width=50pc
[14]: /ws02/images/2/24/14.png?featherlight=false&width=50pc
[15]: /ws02/images/2/24/15.png?featherlight=false&width=50pc
[16]: /ws02/images/2/24/16.png?featherlight=false&width=50pc
[17]: /ws02/images/2/24/17.png?featherlight=false&width=50pc
[18]: /ws02/images/2/24/18.png?featherlight=false&width=50pc
[19]: /ws02/images/2/24/19.png?featherlight=false&width=50pc