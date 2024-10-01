---
title: "Tạo vai trò EFS CSI driver"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 4.1 </b> "
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
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks11.png)

2. Ở mục **Add an Identity provider**.

- Chọn **OpenID Connect**.
- Ở trường **Provider URL**, điền giá trị bạn đã copy ở bước trước (Kiểm tra **Step 7** ở **3.1 Create EKS cluster**).
- Ở trường **Audience**, điền giá trị **sts.amazonaws.com**.
- Bấm **Add provider**.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks12.png)
- Copy giá trị ARN để sử dụng cho các bước kế tiếp.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks15.png)

3. Ở mục [IAM management console](https://console.aws.amazon.com/iam/home).

- Bấm **Roles**.
- Bấm **Create role**.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createrole01.png)

4. Ở mục **Step 1: Select trusted entity**.

- Chọn **Web identity** ở mục **Trusted entity type**.
- Ở mục **Web identity**.
  - Chọn giá trị **OpenID Connect provider URL** của cụm EKS của bạn.
  - Chọn **sts.amazonaws.com** ở trường **Audience**.
- Bấm **Next**.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks13.png)

5. Ở mục **Step 2: Add permissions**.

- Nhập **AmazonEFSCSIDriverPolicy** ở hộp **Filter policies**.
- Chọn **AmazonEFSCSIDriverPolicy** hiện ra ở ô tìm kiếm.
- Bấm **Next**.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks16.png)

6. Ở mục **Step 3: Name, review, and create**.

- Ở mục **Role details**, nhập giá trị **labEKSEFSCSIDriverRole** ở trường **Role name**
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks17.png)
- Kéo xuống và bấm **Create role**.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks18.png)

7. Ở **Role management console**.

- Chọn vai trò **labEKSEFSCSIDriverRole** mà bạn đã tạo ra ở bước trước.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks19.png)

8. Ở mục **labEKSEFSCSIDriverRole**.

- Chọn **Trust relationships**.
- Chọn **Edit trust policy**.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks20.png)

9. Ở mục **Edit trust policy**.

- Sửa cấu hình hiện tại như bên dưới.
  - Thay thế giá trị `arn:aws:iam::017820706022:oidc-provider/oidc.eks.us-east-1.amazonaws.com/id/89D8A1B6165D0BD767C1B51B1C9150EE` thành giá trị ARN ở **step 2**.
  - Thay thế giá trị `oidc.eks.us-east-1.amazonaws.com/id/89D8A1B6165D0BD767C1B51B1C9150EE` thành giá trị Provider ở **step 2**.
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
- Bấm **Update policy**.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks21.png)

Tiếp theo, chúng ta sẽ tạo EFS.
