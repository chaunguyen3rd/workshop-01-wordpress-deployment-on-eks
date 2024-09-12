---
title : "Create EFS CSI driver role"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 2.2.3 </b> "
---

**The EFS CSI (Container Storage Interface) driver** is a Kubernetes plugin that allows you to manage **Amazon Elastic File System (EFS)** volumes as persistent storage for your Kubernetes workloads. With this driver, you can easily provision, mount, and use EFS file systems in a Kubernetes cluster, enabling your applications to share files across multiple pods with a fully managed, scalable, and elastic NFS file system.

Key features of the EFS CSI driver include:

- **Dynamic Provisioning**: Automatically creates EFS file systems based on PersistentVolumeClaim (PVC) specifications.
- **Multi-AZ Support**: EFS volumes can be accessed concurrently by multiple pods across different Availability Zones, ensuring high availability.
- **Shared Storage**: EFS allows multiple pods to read from and write to the same volume simultaneously, making it ideal for shared storage scenarios.
- **Security**: Supports IAM roles for access control and can be used with VPC security groups to manage network access.
  
The **EFS CSI driver** is particularly useful for stateful applications that require shared, persistent storage in Kubernetes environments.

{{% notice info %}}
Read more: https://github.com/kubernetes-sigs/aws-efs-csi-driver
{{% /notice %}}

#### Create IAM role **labEFSCSIDriverRole**
1. Go to [IAM management console](https://console.aws.amazon.com/iam/home)
  - Click **Roles**.
  - Click **Create role**.
  ![VPC](/images/2.prerequisite/ws01-createrole01.png)

2. At **Step 1: Select trusted entity** section.
  - At **Use case** section, choose **EC2** at **Service or use case** field.
  - Next, choose **EC2**.
  - Click **Next**.
  ![VPC](/images/2.prerequisite/ws01-createrole06.png)

3. At **Step 2: Add permissions** section.
  - Find and choose three policies **AmazonEKS_CNI_Policy**, **AmazonEC2ContainerRegistryReadOnly** and **AmazonEKSWorkerNodePolicy**.
  - Click **Next**.
  ![VPC](/images/2.prerequisite/ws01-createrole07.png)

4. At **Step 3: Name, review, and create** section.
  - At **Role details** section, fill the **Role name** field with **labNodeGroupsRole** value.
  ![VPC](/images/2.prerequisite/ws01-createrole08.png)
  - Scroll down and click **Create role**.
  ![VPC](/images/2.prerequisite/ws01-createrole09.png)