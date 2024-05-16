---
title : "Configure AWS Cloud9 IDE"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

Select **Services** then select **Cloud9** under Developer Tools or enter it into the Search bar. ![22][1]

On the Cloud9 Environments page, click **Create Environment** ![22][2]

Enter a **Name** for the Environemnt and select **New EC2 instance** for Environment **Type**. ![22][3]

Select **Additional instance types** then choose **t2.micro** from the drop-down. ![22][4]

{{% notice tip %}}
With this workshop , they use a default setting
{{% /notice %}}

Leave all other options on default setting and click **Create**. ![22][5]

{{% notice info %}}
In my workshop, i will set up a manual network by myself
{{% /notice %}}

Review:

|  1| 2 |
|---|---|
| VPC | ![22][101]|
| Subnets | ![22][102]|
| Route tables | ![22][103]|
| Internet Gateways | ![22][104]|
| Security Groups | ![22][105]|

Networking for Cloud9: ![22][106]

Once the environment is created, navigate to it and click **Open in Cloud9** to launch the IDE. ![22][6]

Close all of the default windows, then create a New Terminal window. ![22][7] ![22][8] ![22][9]

Congrats! Cloud9 is now ready to use. Before installing checkov or pulling code to scan, create and activate a python virtual environment to better organize python packages.

```sh
python3 -m venv env
source ./env/bin/activate
```

 ![22][10]


[1]: /ws02/images/2/22/1.png?featherlight=false&width=50pc
[2]: /ws02/images/2/22/2.png?featherlight=false&width=50pc
[3]: /ws02/images/2/22/3.png?featherlight=false&width=50pc
[4]: /ws02/images/2/22/4.png?featherlight=false&width=50pc
[5]: /ws02/images/2/22/5.png?featherlight=false&width=50pc
[6]: /ws02/images/2/22/6.png?featherlight=false&width=50pc
[7]: /ws02/images/2/22/7.png?featherlight=false&width=50pc
[8]: /ws02/images/2/22/8.png?featherlight=false&width=50pc
[9]: /ws02/images/2/22/9.png?featherlight=false&width=50pc
[10]: /ws02/images/2/22/10.png?featherlight=false&width=50pc



[101]: /ws02/images/2/22/101.png?featherlight=false&width=50pc
[102]: /ws02/images/2/22/102.png?featherlight=false&width=50pc
[103]: /ws02/images/2/22/103.png?featherlight=false&width=50pc
[104]: /ws02/images/2/22/104.png?featherlight=false&width=50pc
[105]: /ws02/images/2/22/105.png?featherlight=false&width=50pc
[106]: /ws02/images/2/22/106.png?featherlight=false&width=50pc
