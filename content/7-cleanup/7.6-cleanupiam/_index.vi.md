---
title : "Dọn dẹp IAM"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 7.6 </b> "
---

### Dọn dẹp vai trò và chính sách IAM
#### Dọn dẹp Access key
1. Đi đến [IAM management console](https://console.aws.amazon.com/iam/home)
  - Bấm **Users**.
  - Chọn người dùng mà đã dùng **Access key** ở các bước trước.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup29.png)

2. Ở trang **User**.
  - Chọn **Security credentials**.
  - Bấm **Actions** và bấm **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup30.png)
  - Ở popup, bấm **Deactivate**, nhập **Key** và bấm **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup31.png)

#### Dọn dẹp vai trò và chính sách IAM
1. Đi đến [IAM management console](https://console.aws.amazon.com/iam/home).
  - Bấm **Roles**.
  - Chọn **Roles** như hình bên dưới.
  - Bấm **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup32.png)
  - Ở popup, nhập **delete** và bấm **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup33.png)

2. Ở trang [IAM management console](https://console.aws.amazon.com/iam/home).
  - Bấm **Policies**.
  - Chọn **Customer managed** ở tùy chọn **Filter by Type**.
  - Chọn **labAWSLoadBalancerControllerPolicy**.
  - Bấm **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup34.png)
  - Ở popup, nhập **labAWSLoadBalancerControllerPolicy** và bấm **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup35.png)

3. Ở trang [IAM management console](https://console.aws.amazon.com/iam/home).
  - Bấm **Identity providers**.
  - Chọn **Your provider** mà đã tạo trước kia.
  - Bấm **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup36.png)
  - Ở popup, nhập **confirm** và bấm **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup37.png)

Vậy chúng ta đã hoàn thành việc dọn dẹp toàn bộ tài nguyên cần thiết cho bài lab này.