---
title: "Create VPC"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 2.1.1 </b> "
---

#### Create VPC **labVPC01**

1. Go to [VPC service management console](https://console.aws.amazon.com/vpc/home)

- Click **Your VPC**.
- Click **Create VPC**.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createvpc01.png)

2. At the **Create VPC** page.

- In the **Name tag** field, enter **labVPC01**.
- In the **IPv4 CIDR** field, enter: **10.0.0.0/16**.
- Click **Create VPC**.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createvpc02.png)

Next, we will create Public subnet.
