---
title : "Create EFS CSI driver role"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
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
  - Click **Identity providers**.
  - Click **Add provider**.
  ![VPC](/images/3.eks/ws01-createeks11.png)

2. At **Add an Identity provider** section.
  - Choose **OpenID Connect**.
  - At **Provider URL** field, fill the value we copied from the previous step (Check **Step 7**).
  - At **Audience** field, fill **sts.amazonaws.com** value.
  - Click **Add provider**.
  ![VPC](/images/3.eks/ws01-createeks12.png)
  - Copy this ARN value to use in the next steps.
  ![VPC](/images/3.eks/ws01-createeks15.png)

3. At [IAM management console](https://console.aws.amazon.com/iam/home) section.
  - Click **Roles**.
  - Click **Create role**.
  ![VPC](/images/2.prerequisite/ws01-createrole01.png)

4. At **Step 1: Select trusted entity** section.
  - Choose **Web identity** at **Trusted entity type** section.
  - At **Web identity** section. 
    + Choose the value of **OpenID Connect provider URL** of your EKS cluster.
    + Choose **sts.amazonaws.com** at **Audience** field.
  - Click **Next**.
  ![VPC](/images/3.eks/ws01-createeks13.png)

5. At **Step 2: Add permissions** section.
  - Enter **AmazonEFSCSIDriverPolicy** in the **Filter policies** box.
  - Select checkbox of the **AmazonEFSCSIDriverPolicy** returned in the search.
  - Click **Next**.
  ![VPC](/images/3.eks/ws01-createeks16.png)

6. At **Step 3: Name, review, and create** section.
  - At **Role details** section, enter **labEKSEFSCSIDriverRole** value at **Role name** field
  ![VPC](/images/3.eks/ws01-createeks17.png)
  - Scroll down and click **Create role**.
  ![VPC](/images/3.eks/ws01-createeks18.png)

7. At **Role management console**.
  - Choose **labEKSEFSCSIDriverRole** role that created in the previous step.
  ![VPC](/images/3.eks/ws01-createeks19.png)

8. At **labEKSEFSCSIDriverRole** section.
  - Choose **Trust relationships** tab.
  - Choose **Edit trust policy**.
  ![VPC](/images/3.eks/ws01-createeks20.png)

9. At **Edit trust policy** section.
  - Edit the current config as below.
    +  Change ``arn:aws:iam::017820706022:oidc-provider/oidc.eks.us-east-1.amazonaws.com/id/89D8A1B6165D0BD767C1B51B1C9150EE`` value to your ARN value from **step 2**.
    + Change ``oidc.eks.us-east-1.amazonaws.com/id/89D8A1B6165D0BD767C1B51B1C9150EE`` value to your Provider value from **step 2**.
    ```
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": {
            "Federated": "arn:aws:iam::017820706022:oidc-provider/oidc.eks.us-east-1.amazonaws.com/id/89D8A1B6165D0BD767C1B51B1C9150EE"
          },
          "Action": "sts:AssumeRoleWithWebIdentity",
          "Condition": {
            "StringLike": {
              "oidc.eks.us-east-1.amazonaws.com/id/89D8A1B6165D0BD767C1B51B1C9150EE:sub": "system:serviceaccount:kube-system:efs-csi-*",
              "oidc.eks.us-east-1.amazonaws.com/id/89D8A1B6165D0BD767C1B51B1C9150EE:aud": "sts.amazonaws.com"
            }
          }
        }
      ]
    }
    ```
  - Click **Update policy**.
  ![VPC](/images/3.eks/ws01-createeks21.png)