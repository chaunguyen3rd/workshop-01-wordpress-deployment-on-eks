---
title: "Create Private Subnet"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 2.1.3 </b> "
---

#### Create Private Subnet

1. Click **Subnets**.

- Click **Create subnet**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc21.png)

2. At the **Create subnet** page.

- In the **VPC ID** section, click **labVPC01**.
- Click on **Add new subnet**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc22.png)
- At the **Subnet 1 of 1** section.
  - In the **Subnet name** field, enter **labPrivateSubnet01**.
  - In the **Availability Zone** section, select the **US EAST (N. Virginia) / us-east-1a**.
  - In the field **IPv4 CIDR block** enter **10.0.11.0/24**.
  - Click **Add new subnet**.
    ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc23.png)
- At the **Subnet 2 of 2** section.
  - In the **Subnet name** field, enter **labPrivateSubnet02**.
  - In the **Availability Zone** section, select the **US EAST (N. Virginia) / us-east-1b**.
  - In the field **IPv4 CIDR block** enter **10.0.12.0/24**.
  - Click **Create subnet**.
    ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc24.png)

3. At the **VPC dashboard**.

- Click **NAT gateways**.
- Click **Create NAT gateway** button.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc26.png)

4. At the **Create NAT gateway** page.

- Enter **labNATGW01** value at **Name** field.
- Choose **labPublicSubnet01** subnet.
- Choose **Public** Connectivity type.
- Click **Allocate Elastic IP** at **Elastic IP allocation ID** field.
- Click **Create NAT gateway**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc27.png)

5. At the **VPC dashboard**.

- Click **Route tables**.
- Click **Create route table** button.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc28.png)

6. At the **Create route table** page.

- Enter **labPrivateRT01** at **Name** field.
- Choose **labVPC01** at **VPC** field.
- Click **Create route table**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc29.png)

7. At the **labPrivateRT01** page.

- Choose **Subnets associations** tab.
- Click **Edit subnets associations**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc30.png)

8. At the **Edit subnet associations** page.

- Choose **labPrivateSubnet01** and **labPrivateSubnet02**.
- Click **Save associations**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc31.png)

9. At the **labPrivateRT01** page.

- Choose **Routes** tab.
- Click **Edit routes**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc32.png)

10. At the **Edit routes** page.

- Click **Add route**.
- Choose **0.0.0.0/0** at **Destination** field.
- Choose **NAT gateway** and click on the **NAT gateway** created before.
- Click **Save changes**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc33.png)

The next step is to create the necessary security groups for the lab.
