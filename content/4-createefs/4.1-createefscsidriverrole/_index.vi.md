---
title : "Tạo vai trò EFS CSI driver"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---

### Tổng quan
**The EFS CSI (Container Storage Interface) driver** là một plugin Kubernetes cho phép bạn quản lý **Amazon Elastic File System (EFS)** dưới dạng lưu trữ liên tục cho khối lượng công việc Kubernetes của bạn. Với trình điều khiển này, bạn có thể dễ dàng cung cấp, gắn kết và sử dụng hệ thống tệp EFS trong cụm Kubernetes, cho phép các ứng dụng của bạn chia sẻ tệp trên nhiều nhóm với hệ thống tệp NFS được quản lý hoàn toàn, có thể mở rộng và đàn hồi.

Các tính năng chính của trình điều khiển EFS CSI bao gồm:
- **Cung cấp động**: Tự động tạo hệ thống tệp EFS dựa trên thông số kỹ thuật PersistentVolumeClaim (PVC).
- **Hỗ trợ nhiều AZ**: Nhiều pod trên nhiều Vùng khả dụng khác nhau có thể truy cập đồng thời các ổ đĩa EFS, đảm bảo tính khả dụng cao.
- **Lưu trữ chia sẻ**: EFS cho phép nhiều pod đọc và ghi vào cùng một ổ đĩa cùng lúc, lý tưởng cho các tình huống lưu trữ chia sẻ.
- **Bảo mật**: Hỗ trợ các vai trò IAM để kiểm soát truy cập và có thể được sử dụng với các nhóm bảo mật VPC để quản lý quyền truy cập mạng.

**Trình điều khiển EFS CSI** đặc biệt hữu ích cho các ứng dụng có trạng thái yêu cầu lưu trữ chia sẻ, liên tục trong môi trường Kubernetes.

{{% notice info %}}
Đọc thêm: https://github.com/kubernetes-sigs/aws-efs-csi-driver
{{% /notice %}}

#### Tạo vai trò IAM **labEFSCSIDriverRole**
1. Đi đến [IAM management console](https://console.aws.amazon.com/iam/home)
  - Bấm **Identity providers**.
  - Bấm **Add provider**.
  ![VPC](/images/3.eks/ws01-createeks11.png)

1. Ở mục **Add an Identity provider**.
  - Choose **OpenID Connect**.
  - At **Provider URL** field, fill the value we copied from the previous step (Check **Step 7** at **3.1 Create EKS cluster**).
  - At **Audience** field, fill **sts.amazonaws.com** value.
  - Click **Add provider**.
  ![VPC](/images/3.eks/ws01-createeks12.png)
  - Copy this ARN value to use in the next steps.
  ![VPC](/images/3.eks/ws01-createeks15.png)

1. At [IAM management console](https://console.aws.amazon.com/iam/home) section.
  - Click **Roles**.
  - Click **Create role**.
  ![VPC](/images/2.prerequisite/ws01-createrole01.png)

1. At **Step 1: Select trusted entity** section.
  - Choose **Web identity** at **Trusted entity type** section.
  - At **Web identity** section. 
    + Choose the value of **OpenID Connect provider URL** of your EKS cluster.
    + Choose **sts.amazonaws.com** at **Audience** field.
  - Click **Next**.
  ![VPC](/images/3.eks/ws01-createeks13.png)

1. At **Step 2: Add permissions** section.
  - Enter **AmazonEFSCSIDriverPolicy** in the **Filter policies** box.
  - Select checkbox of the **AmazonEFSCSIDriverPolicy** returned in the search.
  - Click **Next**.
  ![VPC](/images/3.eks/ws01-createeks16.png)

1. At **Step 3: Name, review, and create** section.
  - At **Role details** section, enter **labEKSEFSCSIDriverRole** value at **Role name** field
  ![VPC](/images/3.eks/ws01-createeks17.png)
  - Scroll down and click **Create role**.
  ![VPC](/images/3.eks/ws01-createeks18.png)

1. At **Role management console**.
  - Choose **labEKSEFSCSIDriverRole** role that created in the previous step.
  ![VPC](/images/3.eks/ws01-createeks19.png)

1. At **labEKSEFSCSIDriverRole** section.
  - Choose **Trust relationships** tab.
  - Choose **Edit trust policy**.
  ![VPC](/images/3.eks/ws01-createeks20.png)

1. At **Edit trust policy** section.
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

Next, we will create EFS.