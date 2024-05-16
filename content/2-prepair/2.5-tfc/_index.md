---
title : "Integrate workflow with Terraform Cloud"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 2.5 </b> "
---

Let's continue by integrating our Github repository with Terraform Cloud. We will then use Terraform Cloud to deploy IaC resource to AWS.

Navigate to [Terraform Cloud](https://app.terraform.io/session) and sign in / sign up. The community edition is all that is needed for this workshop. ![25][1] ![25][2]

Enter an Organization name and provide your email address. ![25][3]

Create a workspace using the **Version Control Workflow** option. ![25][4]

Select **Gtihub**, then **Gtihub.com** from the dropdown. Authenticate and authorize the Github.  ![25][5]

Choose the **prisma-cloud-devsecops-workshop** from the list of repositories. ![25][6] ![25][7]

Add a **Workspace** Name and click **Advanced options**. ![25][8]

In the **Terraform Working Directory** field, enter **/code/build/**. Select **Only trigger runs when files in specified paths change**.  ![25][9] 

Leave the rest of the options as default and click **Create**. ![25][10]

Almost done. In order to deploy resources to AWS, we need to provide Terraform Cloud with AWS credentials. We need to add our credentials as workspace variables. Click `Continue to workspace overview` to do continue. ![25][11]

Click `Configure variables`  ![25][12]

Add variables for `AWS_SECRET_KEY_ID` and `AWS_SECRET_ACCESS_KEY`. Ensure you select Environment variables for both and that `AWS_SECRET_ACCESS_KEY` is marked as `Sensitive`. ![25][13]

Review the variables then return the your workspace overview when finished. ![25][14]

Terraform Cloud is now configured and our pipeline is ready to go. Let's test this out by submitting a pull request.


[1]: /ws02/images/2/25/1.png?featherlight=false&width=50pc
[2]: /ws02/images/2/25/2.png?featherlight=false&width=50pc
[3]: /ws02/images/2/25/3.png?featherlight=false&width=50pc
[4]: /ws02/images/2/25/4.png?featherlight=false&width=50pc
[5]: /ws02/images/2/25/5.png?featherlight=false&width=50pc
[6]: /ws02/images/2/25/6.png?featherlight=false&width=50pc
[7]: /ws02/images/2/25/7.png?featherlight=false&width=50pc
[8]: /ws02/images/2/25/8.png?featherlight=false&width=50pc
[9]: /ws02/images/2/25/9.png?featherlight=false&width=50pc
[10]: /ws02/images/2/25/10.png?featherlight=false&width=50pc
[11]: /ws02/images/2/25/11.png?featherlight=false&width=50pc
[12]: /ws02/images/2/25/12.png?featherlight=false&width=50pc
[13]: /ws02/images/2/25/13.png?featherlight=false&width=50pc
[14]: /ws02/images/2/25/14.png?featherlight=false&width=50pc
