---
title : "Tạo cụm EKS"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---

{{% notice note %}}
Để thực hiện bước này, bạn cần hoàn thành tất cả các bước từ [Chuẩn bị](/2-Prerequisite/).
{{% /notice %}}

1. Đi đến [EKS management console](https://console.aws.amazon.com/eks/home).
  - Bấm **Clusters**.
  - Bấm **Add cluster**, then click **Create**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks01.png)

2. Ở mục **Step 1: Configure cluster**.
  - Điền vào trường **Name** với giá trị **labEKSCluster01**.
  - Ở trường **Cluster service role**, chọn **labEKSClusterRole**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks02.png)
  - Kéo xuống và bấm **Next**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks03.png)

3. Ở mục **Step 2: Specify networking**.
  - Ở trường **VPC**, chọn **labVPC01**.
  - Ở trường **Subnets**, chọn **labPrivateSubnet01** và **labPrivateSubnet02**.
  - Ở trường **Security groups**, chọn **labEKSClusterSG01**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks04.png)
  - Kéo xuống, ở mục **Cluster endpoint access**, chọn **Private**.
  - Bấm **Next**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks05.png)

4. Ở mục **Step 3: Configure observability**.
  - Giữ mặc định và bấm **Next**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks06.png)

5. Ở mục **Step 4: Select add-ons**.
  - Giữ mặc định và bấm **Next**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks07.png)

6. Ở mục **Step 5: Configure selected add-ons settings**.
  - Giữ mặc định và bấm **Next**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks08.png)

7. Ở mục **Step 6: Review and create**.
  - Giữ mặc định và bấm **Create**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks09.png)

  {{% notice note %}}
  Sẽ mất một thời gian để cụm EKS được tạo thành công.
  {{% /notice %}}

7. Kiểm tra nếu cụm **labEKSCluster01** đã tạo thành công hay chưa.
  - Lưu lại giá trị **OpenID Connect provider URL** cho bước kế tiếp.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/3.eks/ws01-createeks10.png)

Tiếp theo chúng ta sẽ tạo Node groups.