---
title : "Create EKS cluster"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---

{{% notice note %}}
To implement this step, you need to finish all steps from [Prerequisite](/2-Prerequisite/).
{{% /notice %}}

1. Go to [EKS service management console](https://console.aws.amazon.com/eks/home).
  - Click on **Clusters**.
  - Click **Add cluster**, then click **Create**.
  ![Connect](/images/3.eks/ws01-createeks01.png)

2. At **Step 1: Configure cluster** section.
  - Fill the **Name** field with **labEKSCluster01** value.
  - At the **Cluster service role** field, choose **labEKSClusterRole**.
  ![Connect](/images/3.eks/ws01-createeks02.png)
  - Scroll down and click **Next**.
  ![Connect](/images/3.eks/ws01-createeks03.png)

3. At **Step 2: Specify networking** section.
  - At the **VPC** field, choose **labVPC01**.
  - At the **Subnets** field, choose **labPrivateSubnet01** and **labPrivateSubnet02**.
  - At the **Security groups** field, choose **labEKSClusterSG01**.
  ![Connect](/images/3.eks/ws01-createeks04.png)
  - Scroll down, at **Cluster endpoint access** section, choose **Private**.
  - Click **Next**.
  ![Connect](/images/3.eks/ws01-createeks05.png)

4. At **Step 3: Configure observability** section.
  - Leave as default and click **Next**.
  ![Connect](/images/3.eks/ws01-createeks06.png)

5. At **Step 4: Select add-ons** section.
  - Leave as default and click **Next**.
  ![Connect](/images/3.eks/ws01-createeks07.png)

6. At **Step 5: Configure selected add-ons settings** section.
  - Leave as default and click **Next**.
  ![Connect](/images/3.eks/ws01-createeks08.png)

7. At **Step 6: Review and create** section.
  - Leave as default and click **Create**.
  ![Connect](/images/3.eks/ws01-createeks09.png)

{{% notice note %}}
It will take some time for the EKS cluster to be successfully created.
{{% /notice %}}

7. Check if labEKSCluster01 created successfully or not.
  - Save this **OpenID Connect provider URL** for the next step.
  ![Connect](/images/3.eks/ws01-createeks10.png)

Next we will create EFS CSI driver role.