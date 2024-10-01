---
title: "Create Node groups"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

### Overall

In **Amazon EKS (Elastic Kubernetes Service)**, **Node Groups** are collections of Amazon EC2 instances that function as worker nodes in your EKS cluster. These nodes run the containerized workloads in pods, and they are where Kubernetes schedules and manages application workloads.

{{% notice info %}}
Read more: https://docs.aws.amazon.com/eks/latest/userguide/managed-node-groups.html
{{% /notice %}}

#### Create Node groups

1. Go to [EKS management console](https://console.aws.amazon.com/eks/home).

- Click on **Clusters**.
- Choose **labEKSCluster01** cluster.
  ![VPC](/workshop.chaunguyen.site/images//3.eks/ws01-createeks22.png)

2. At **labEKSCluster01** console.

- Click **Compute** tab.
- Click **Add node group**.
  ![VPC](/workshop.chaunguyen.site/images//3.eks/ws01-createeks23.png)

3. At **Step 1: Configure node group** section.

- Enter **labNodeGroup01** value at **Name** field.
- Choose **labNodeGroupsRole** at **Node IAM role** field.
  ![VPC](/workshop.chaunguyen.site/images//3.eks/ws01-createeks24.png)
- Scroll down and click **Next**.
  ![VPC](/workshop.chaunguyen.site/images//3.eks/ws01-createeks25.png)

4. At **Step 2: Set compute and scaling configuration** section.

- Choose **Spot** at **Capacity type** field.
- Choose **m1.medium** at **Instance types** field.
  ![VPC](/workshop.chaunguyen.site/images//3.eks/ws01-createeks26.png)
- Scroll down and click **Next**.
  ![VPC](/workshop.chaunguyen.site/images//3.eks/ws01-createeks27.png)

5. At **Step 3: Specify networking** section.

- Choose **labPrivateSubnet01** and **labPrivateSubnet02** at **Subnet** field.
- Click **Next**.
  ![VPC](/workshop.chaunguyen.site/images//3.eks/ws01-createeks28.png)

6. At **Step 4: Review and create** section.

- Leave as default and click **Create**.
  ![VPC](/workshop.chaunguyen.site/images//3.eks/ws01-createeks29.png)
  {{% notice note %}}
  It will take some time for the Node groups to be successfully created.
  {{% /notice %}}

7. Check if **labNodeGroup01** created successfully or not.
   ![VPC](/workshop.chaunguyen.site/images//3.eks/ws01-createeks30.png)

Next we will configure the EKS cluster.
