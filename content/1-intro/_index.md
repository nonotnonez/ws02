---
title : "Introduction"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

**In this workshop, we will learn how to:**

1. Gain an understanding of DevSecOps and infrastructure as code (IaC) using Terraform
2. Scan IaC files for misconfigurations locally
3. Set up CI/CD pipelines to automate security scanning and policy enforcement
4. Fix security findings and AWS resource misconfigurations with Prisma Cloud

**DevSecOps**

The foundation of DevSecOps lies in the DevOps movement, wherein development and operations functions have merged to make deployments faster, safer, and more repeatable. Common DevOps practices include automated infrastructure build pipelines (CI/CD) and version-controlled manifests (GitOps) to make it easier to control cloud deployments. By baking software and infrastructure quality requirements into the release lifecycle, teams save time manually reviewing code, letting teams focus on shipping features

![1](/ws02/images/1/2.png?featherlight=false&width=50pc)

As deployments to production speed up, many traditional cloud security concepts break down. With the rise of containerized technologies, serverless functions, and IaC frameworks, it is increasingly harder to maintain visibility of cloud security posture.

By leveraging DevOps foundations, security and development teams can build security scanning and policy enforcement into automated pipelines. The ultimate goal with DevSecOps is to “shift cloud security left.” What shifting cloud security left means is automating it and embedding it earlier into the development lifecycle so that actions can be taken earlier. Preventing risky deployments is a more proactive approach to traditional cloud security which often slows down development teams with deployment rollbacks and disruptive fixes.

To successfully implement DevSecOps, it is critical that teams building secure infrastructure must embracing existing tools and workflows. At Palo Alto Networks, we’re committed to making it as simple, effective, and painless as possible to automate security controls and integrate them seamlessly into standard workflows.

**Infrastructure as Code Using Terraform**

Infrastructure as code (IaC) frameworks, such as HashiCorp Terraform, make cloud provisioning scalable and straightforward by leveraging automation and code. Defining our cloud infrastructure in code simplifies repetitive DevOps tasks and gives us a versioned, auditable source of truth for the state of an environment.

![1](/ws02/images/1/3.png?featherlight=false&width=50pc)

Terraform is useful for defining resource configurations and interacting with APIs in a codified, stateful manor. Any updates we want to make, such as adding more instances or changes to a configuration, can be handled by Terraform.

For example, the following Terraform resource block defines a simple AWS S3 bucket:

```sh
resource "aws_s3_bucket" "data" {
  bucket     = "my_bucket_name"
  acl        = "public-read-write"
}
```
After performing `terraform init` we can provision an S3 bucket with the following command:

```sh
terraform apply
```
Any changes made to the resource definition within a `.tf `file, such as adding tags or changing the acl, can be pushed with the `terraform apply` command.

Another benefit of using Terraform to define infrastructure is that code can be scanned for misconfigurations before the resource is created. This allows for security controls to be integrated into the development process, preventing issues from being introduced, deployed and exploited.

**AWS Cloud9 IDE**

To ensure we all have the same environent configuration, we will use AWS Cloud9, a cloud-delivered IDE from AWS, to carry out many of the steps in this workshop. AWS Cloud9  is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser. It includes a code editor, debugger, and terminal. Cloud9 comes pre-packaged with essential tools for popular programming languages and the AWS Command Line Interface (CLI) pre-installed so you don’t need to install files or configure your laptop for this workshop.

Your Cloud9 environment will have access to the same AWS resources as the user with which you logged into the AWS Management Console. We strongly recommend using Cloud9 to complete this workshop.

Cloud9 works best with Chrome or Firefox, not Safari. It cannot be used from a tablet.

**Checkov**

[Checkov](https://checkov.io/) is an open source 'policy-as-code' tool that scans cloud infrastructure defintions to find misconfigurations before they are deployed. Some of the key benefits of checkov:

- Runs as a command line interface (CLI) tool
- Supports many common plaftorms and frameworks
- Ships with thousands of default policies
- Works on windows/mac/linux (any system with python installed)


#### Content

1. [Introduction](/ws02/1-intro/)
2. [Prepairation](/ws02/2-prepair/)
3. [Configure](/ws02/3-config/)
4. [Cleanup](/ws02/4-cleanup/)