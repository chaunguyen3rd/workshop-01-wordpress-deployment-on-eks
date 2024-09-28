---
title : "Preparation "
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

{{% notice info %}}
You need to create a Linux instance on the public subnet to access to EKS cluster in private subnet.
{{% /notice %}}

To learn how to create EC2 instances and VPCs with public/private subnets, you can refer to the lab:
- [About Amazon EC2](https://000004.awsstudygroup.com/en/)
- [Works with Amazon VPC](https://000003.awsstudygroup.com/en/)

To deploy the Wordpress application on EKS cluster, we need to grant permissions to Bastion host to be able to create and operate the Wordpress application on EKS cluster. In this preparation part, we will create VPC, IAM roles, EC2 Bastion host, EFS, ... to be able to complete this lab.

### Content
- [Prepare VPC and EC2](2.1-createec2/)
- [Create IAM Role](2.2-createiamrole/)