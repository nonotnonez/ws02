---
title : "Configure IAM User and API Key"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---


From the AWS console, select `IAM` or search for 'IAM' in the Search bar if not displayed. ![21][1]

In the IAM Dashboard, click `Users` on the left sidebar. ![21][2]

Click the `Create User` button on the top right. ![21][3]

Specify a `User name` that will be unique then click `Next`. ![21][4]

Next, set the permissions for the user by selecting `Attach policies directly` and attaching the `AdministratorAccess` policy. ![21][5]

Review the user details and click `Create user`. ![21][6]

Now we need to assign an API key to the user we just created. Click on the user you just created from the IAM Dashboard and then click `Create access key` on the right. ![21][7]

Select `Other` from the Access Key options. ![21][8]

Optionally, supply a tag to associate with the Access Key, then click `Create access key`. ![21][9]

Finally, save the `Access Key` data provided (copy to a local file). This credential will be used to deploy resources to AWS in a later section. When ready, click `Done`. ![21][10]

An access key will now appear on the User details page. ![21][11]

[1]: /ws02/images/2/21/1.png?featherlight=false&width=50pc
[2]: /ws02/images/2/21/2.png?featherlight=false&width=50pc
[3]: /ws02/images/2/21/3.png?featherlight=false&width=50pc
[4]: /ws02/images/2/21/4.png?featherlight=false&width=50pc
[5]: /ws02/images/2/21/5.png?featherlight=false&width=50pc
[6]: /ws02/images/2/21/6.png?featherlight=false&width=50pc
[7]: /ws02/images/2/21/7.png?featherlight=false&width=50pc
[8]: /ws02/images/2/21/8.png?featherlight=false&width=50pc
[9]: /ws02/images/2/21/9.png?featherlight=false&width=50pc
[10]: /ws02/images/2/21/10.png?featherlight=false&width=50pc
[11]: /ws02/images/2/21/11.png?featherlight=false&width=50pc