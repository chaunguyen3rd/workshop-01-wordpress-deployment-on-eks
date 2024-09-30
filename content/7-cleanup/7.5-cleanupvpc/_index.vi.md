---
title : "Cleanup VPC"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 7.5 </b> "
---

### Cleanup VPC
#### Cleanup Route table
1. Go to [VPC service management console](https://console.aws.amazon.com/vpc/home)
  - Click **Route tables**.
  - Choose **labPublicRT01**.
  - Click **Subnet associations**.
  - Click **Edit subnet associations**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup13.png)

2. At **Edit subnet associations** page.
  - Unchecked all available subnets.
  - Click **Save associations**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup14.png)

3. Go to [VPC service management console](https://console.aws.amazon.com/vpc/home)
  - Click **Route tables**.
  - Choose **labPrivateRT01**.
  - Click **Subnet associations**.
  - Click **Edit subnet associations**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup15.png)

4. At **Edit subnet associations** page.
  - Unchecked all available subnets.
  - Click **Save associations**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup14.png)

5. Go to [VPC service management console](https://console.aws.amazon.com/vpc/home)
  - Click **Route tables**.
  - Choose **labPrivateRT01** and **labPublicRT01**.
  - Click **Actions**.
  - Click **Delete route table**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup16.png)
  - At the popup, enter **delete** and click **Delete**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup17.png)

#### Cleanup NAT gateways
1. Go to [VPC service management console](https://console.aws.amazon.com/vpc/home)
  - Click **NAT gateways**.
  - Choose **labNATGW01**.
  - Click **Actions**.
  - Click **Delete NAT gateway**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup18.png)

2. Go to [VPC service management console](https://console.aws.amazon.com/vpc/home)
  - Click **Elastic IPs**.
  - Click on **52.6.199.235**. Change ``52.6.199.235`` to your **Elastic IP**.
  - Click **Actions**.
  - Click **Release Elastic IP addresses**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup19.png)
  - At the popup, click **Release**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup20.png)

#### Cleanup Internet gateways
1. Go to [VPC service management console](https://console.aws.amazon.com/vpc/home)
  - Click **Internet gateways**.
  - Choose **labIGW01**.
  - Click **Actions**.
  - Click **Detach from VPC**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup21.png)
  - At the popup, click **Detach internet gateway**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup22.png)

2. At [VPC service management console](https://console.aws.amazon.com/vpc/home) page.
  - Click **Internet gateways**.
  - Choose **labIGW01**.
  - Click **Actions**.
  - Click **Delete internet gateway**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup23.png)
  - At the popup, type **delete** and click **Delete internet gateway**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup24.png)

#### Cleanup VPC
1. Go to [VPC service management console](https://console.aws.amazon.com/vpc/home)
  - Click **Your VPCs**.
  - Choose **labVPC01**.
  - Click **Actions**.
  - Click **Delete VPC**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup27.png)
  - At the popup, type **delete** and click **Delete**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup28.png)

Next, we will cleanup IAM roles and policies.