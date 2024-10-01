---
title : "Create security groups"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 2.1.4 </b> "
---

#### Create security groups

In this step, we will proceed to create the security groups used for our Bastion host. As you can see, these security groups will not need to open traditional ports to **ssh** like port **22**.

#### Create security group for Linux instance located in public subnet

1. Go to [VPC service management console](https://console.aws.amazon.com/vpc)
  - Click **Security Group**.
  - Click **Create security group**.
  ![SG](/workshop.chaunguyen.site/2.prerequisite/ws01-createsg01.png)

2. In the **Security group name** field, enter **labBastionHostSG01**.
  - In the **Description** section, enter **labBastionHostSG01**.
  - In the **VPC** section, click the **X** to reselect the **labVPC01** you created for this lab.
  ![SG](/workshop.chaunguyen.site/2.prerequisite/ws01-createsg02.png)

3. At the **Inbound rules** section.
  - Add **SSH rule** type to allow TCP 22 connection from 0.0.0.0/0.
  ![SG](/workshop.chaunguyen.site/2.prerequisite/ws01-createsg03.png)

4. Keep **Outbound rule** as default, drag the mouse to the bottom.
  + Click **Create security group**.

{{%notice tip%}}
As you can see, the security group we created to use for Linux public instances will not need to open traditional ports to **ssh** like port **22**.
{{%/notice%}}

#### Create a security group for a EKS cluster located in a private subnet

1. After successfully creating a security group for the Linux instance located in the public subnet, click the Security Groups link to return to the Security groups list.
  ![SG](/workshop.chaunguyen.site/2.prerequisite/ws01-createsg04.png)

2. Click **Create security group**.

3. In the **Security group name** field, enter **labEKSClusterSG01**.
  - In the **Description** section, enter **labEKSClusterSG01**.
  - In the **VPC** section, click the **X** to reselect the **labVPC01** you created for this lab.
  ![SG](/workshop.chaunguyen.site/2.prerequisite/ws01-createsg05.png)

4. Scroll down.
  - Add **Inbound rule** to allow All TCP connection from 10.0.0.0/16 (CIDR of **labVPC01** we created).
  - Keep **Outbound rule** as default, drag the mouse to the bottom.
  - Click **Create security group**.
  ![SG](/workshop.chaunguyen.site/2.prerequisite/ws01-createsg06.png)

#### Create security group for EFS

1. In this step, we will create security group for **EFS**.

2. After successfully creating the security group for the EKS cluster in the private subnet, click the Security Groups link to return to the Security groups list.
  ![SG](/workshop.chaunguyen.site/2.prerequisite/ws01-createsg07.png)

3. Click **Create security group**.

4. In the **Security group name** field, enter **labEFSSG01**.
  - In the **Description** section, enter **labEFSSG01**.
  - In the **VPC** section, click the **X** to reselect the **labVPC01** you created for this lab.
  ![SG](/workshop.chaunguyen.site/2.prerequisite/ws01-createsg08.png)

5. Scroll down.
  - Add **Inbound rule** to allow All TCP connection from 10.0.0.0/16 (CIDR of **labVPC01** we created).
  - Keep **Outbound rule** as default, drag the mouse to the bottom.
  - Click **Create security group**.
  ![SG](/workshop.chaunguyen.site/2.prerequisite/ws01-createsg09.png)

So we are done creating the necessary security groups for EC2 instance, EKS cluster and EFS. Next, we will create EC2 linux bastion host.