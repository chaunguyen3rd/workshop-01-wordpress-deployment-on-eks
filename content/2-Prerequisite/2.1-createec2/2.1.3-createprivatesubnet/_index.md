---
title : "Create Private Subnet"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 2.1.3 </b> "
---

#### Create Private Subnet

1. Click **Subnets**.
  + Click **Create subnet**.
  ![VPC](/images/2.prerequisite/ws01-createvpc21.png)

2. At the **Create subnet** page.
  - In the **VPC ID** section, click **labVPC01**.
  - Click on **Add new subnet**.
  ![VPC](/images/2.prerequisite/ws01-createvpc22.png)
  - At the **Subnet 1 of 1** section.
    + In the **Subnet name** field, enter **labPrivateSubnet01**.
    + In the **Availability Zone** section, select the **US EAST (N. Virginia) / us-east-1a**.
    + In the field **IPv4 CIDR block** enter **10.0.11.0/24**.
    + Click **Add new subnet**.
    ![VPC](/images/2.prerequisite/ws01-createvpc23.png)
  - At the **Subnet 2 of 2** section.
    + In the **Subnet name** field, enter **labPrivateSubnet02**.
    + In the **Availability Zone** section, select the **US EAST (N. Virginia) / us-east-1b**.
    + In the field **IPv4 CIDR block** enter **10.0.12.0/24**.
    + Click **Create subnet**.
    ![VPC](/images/2.prerequisite/ws01-createvpc24.png)
    
The next step is to create the necessary security groups for the lab.