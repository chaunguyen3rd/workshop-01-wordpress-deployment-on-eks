---
title : "Create EFS CSI driver role"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 2.2.3 </b> "
---

### Overall
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

<!-- Need EKS Cluster create firstly -->