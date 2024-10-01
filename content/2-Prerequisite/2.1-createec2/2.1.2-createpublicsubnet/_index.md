---
title : "Create Public Subnet"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.1.2 </b> "
---

#### Create Public Subnet

1. Click **Subnets**.
  + Click **Create subnet**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc03.png)

2. At the **Create subnet** page.
  + In the **VPC ID** section, click **labVPC01**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc04.png)

3. At the **Subnet settings** section.
  - At the **Subnet 1 of 1** section.
    + In the **Subnet name** field, enter **labPublicSubnet01**.
    + In the **Availability Zone** section, select the **US EAST (N. Virginia) / us-east-1a**.
    + In the field **IPv4 CIDR block** enter **10.0.1.0/24**.
    + Click **Add new subnet**.
    ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc05.png)

  - At the **Subnet 2 of 2** section.
    + In the **Subnet name** field, enter **labPublicSubnet02**.
    + In the **Availability Zone** section, select the **US EAST (N. Virginia) / us-east-1b**.
    + In the field **IPv4 CIDR block** enter **10.0.2.0/24**.
    + Click **Add new subnet**.
    ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc06.png)

  - At the **Subnet 3 of 3** section.
    + In the **Subnet name** field, enter **labPublicSubnet03**.
    + In the **Availability Zone** section, select the **US EAST (N. Virginia) / us-east-1c**.
    + In the field **IPv4 CIDR block** enter **10.0.3.0/24**.
    + Click **Create subnet**.
    ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc07.png)

4. Click **labPublicSubnet01**.
  + Click **Actions**.
  + Click **Edit subnet settings**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc08.png)

5. Click **Enable auto-assign public IPv4 address**.
  + Click **Save**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc09.png)

6. Click **Internet Gateways**.
  + Click **Create internet gateway**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc10.png)

7. At the **Create internet gateway** page.
  + In the **Name tag** field, enter **labIGW01**.
  + Click **Create internet gateway**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc11.png)

8. After successful creation, click **Actions**.
  + Click **Attach to VPC**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc12.png)

9. At the **Attach to VPC** page.
  + In the **Available VPCs** section, select **labVPC01**.
  + Click **Attach internet gateway**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc13.png)

10. Next we will create a custom route table to assign to **labPublicSubnet01, labPublicSubnet02 and labPublicSubnet03**.
  + Click **Route Tables**.
  + Click **Create route table**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc14.png)

11. At the **Create route table** page.
  + In the **Name** field, enter **labPublicRT01**.
  + In the **VPC** section, select **labVPC01**.
  + Click **Create route table**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc15.png)

12. After creating the route table successfully.
  + Click **Edit routes**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc16.png)

13. At the **Edit routes** page.
  + Click **Add route**.
  + In the **Destination** field, enter 0.0.0.0/0
  + In the **Target** section, select **Internet Gateway** and then select **labIGW01**.
  + Click **Save changes**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc17.png)

14. Click the **Subnet associations** tab.
  + Click **Edit subnet associations** to proceed with the associate custom route table we just created in **Lab Public Subnet**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc18.png)

15. At the **Edit subnet associations** page.
  + Click on **Name** checkbox to choose all **labPublicSubnet0\***.
  + Click **Save associations**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc19.png)

16. Check that the route table information has been associated with 3 **labPublicSubnet0\*** and the internet route information has been pointed to the Internet Gateway as shown below.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc20.png)

Next, we will create Private subnet.