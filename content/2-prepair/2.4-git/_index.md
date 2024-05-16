---
title : "Integrate with Github Actions"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 2.4 </b> "
---

You can leverage GitHub Actions to run automated scans for every build or specific builds, such as the ones that merge into the master branch. This action can alert on misconfigurations, or block code from being merged if certain policies are violated. Results can also be sent to Prisma Cloud and other sources for further review and remediation steps.

Let's begin by setting an action from the repository page, under the Actions tab. Then click on set up a workflow yourself -> to create a new action from scratch.



