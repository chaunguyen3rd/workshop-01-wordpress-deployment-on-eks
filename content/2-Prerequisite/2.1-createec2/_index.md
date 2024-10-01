---
title: "Preparing VPC and EC2"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 2.1 </b> "
---

In this step, we will need to create a VPC with 3 public and 2 private subnets. Then create 1 EC2 Instance Linux located in the public subnet.

The architecture overview after you complete this step will be as follows:

![VPC](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-prep01.png)

To learn how to create EC2 instances and VPCs with public/private subnets, you can refer to the lab:

- [About Amazon EC2](https://000004.awsstudygroup.com/en/)
- [Works with Amazon VPC](https://000003.awsstudygroup.com/en/)

### Content

- [Create VPC](2.1.1-createvpc/)
- [Create Public Subnet](2.1.2-createpublicsubnet/)
- [Create Private Subnet](2.1.3-createprivatesubnet/)
- [Create security group](2.1.4-createsecgroup/)
- [Create public Linux server](2.1.5-createec2linux/)
- [Configure public Linux server](2.1.6-configureec2linux/)
