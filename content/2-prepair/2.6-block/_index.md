---
title : "Block a Pull Request, Prevent a Deployment"
date :  "`r Sys.Date()`" 
weight : 6
chapter : false
pre : " <b> 2.6 </b> "
---

We have now configured a GitHub repository to be scanned with checkov and to trigger Terraform Cloud to deploy infrastructure. Let's see how this works in action.

Create a new file in the GitHub UI under the path `code/build/s3.tf`. Enter the following code snippet into the new file.

```sh
provider "aws" {
  region = "ap-southeast-1"
}

resource "aws_s3_bucket" "dev_s3" {
  bucket_prefix = "dev-"

  tags = {
    Environment      = "Dev"
  }
}

resource "aws_s3_bucket_ownership_controls" "dev_s3" {
  bucket = aws_s3_bucket.dev_s3.id
  rule {
    object_ownership = "BucketOwnerPreferred"
  }
}


```


![26][1]

Once complete, click `Commit changes...` at the top right, then select `Create a new branch and start a pull request` and click `Propose changes`. ![26][2]

At the next screen, review the diff then click `Create pull request`. ![26][3]

One more time... click Create pull request to open the PR. ![26][4]

Wait for the checks to run. Then take note of the result: a blocked pull request! ![26][5]

Either bypass branch protections and `Merge pull request` or go back to the Github Action for checkov and uncomment the line with `--soft-fail=true`. This will require closing and reopening a new pull request.  ![26][6] ![26][10] ![26][11] ![26][12]

[1]: /ws02/images/2/26/1.png?featherlight=false&width=50pc
[2]: /ws02/images/2/26/2.png?featherlight=false&width=50pc
[3]: /ws02/images/2/26/3.png?featherlight=false&width=50pc
[4]: /ws02/images/2/26/4.png?featherlight=false&width=50pc
[5]: /ws02/images/2/26/5.png?featherlight=false&width=50pc
[6]: /ws02/images/2/26/6.png?featherlight=false&width=50pc
[7]: /ws02/images/2/26/7.png?featherlight=false&width=50pc
[8]: /ws02/images/2/26/8.png?featherlight=false&width=50pc
[9]: /ws02/images/2/26/9.png?featherlight=false&width=50pc
[10]: /ws02/images/2/26/10.png?featherlight=false&width=50pc
[11]: /ws02/images/2/26/11.png?featherlight=false&width=50pc
[12]: /ws02/images/2/26/12.png?featherlight=false&width=50pc
[13]: /ws02/images/2/26/13.png?featherlight=false&width=50pc
[14]: /ws02/images/2/26/14.png?featherlight=false&width=50pc
