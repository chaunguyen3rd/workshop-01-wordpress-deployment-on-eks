---
title : "Tạo Node groups"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
---

### Tổng quan
Trong **Amazon EKS (Elastic Kubernetes Service)**, **Node Groups** là tập hợp các phiên bản Amazon EC2 hoạt động như các nút worker trong cụm EKS của bạn. Các nút này chạy khối lượng công việc được chứa trong các pod và là nơi Kubernetes lên lịch và quản lý khối lượng công việc của ứng dụng.

{{% notice info %}}
Đọc thêm: https://docs.aws.amazon.com/eks/latest/userguide/managed-node-groups.html
{{% /notice %}}

#### Tạo Node groups
1. Đi đến [EKS management console](https://console.aws.amazon.com/eks/home).
  - Bấm **Clusters**.
  - Chọn cụm **labEKSCluster01**.
  ![VPC](/images/3.eks/ws01-createeks22.png)

2. Ở **labEKSCluster01** console.
  - Bấm tab **Compute**.
  - Bấm **Add node group**.
  ![VPC](/images/3.eks/ws01-createeks23.png)

3. Ở mục **Step 1: Configure node group**.
  - Nhập **labNodeGroup01** ở trường **Name**.
  - Chọn **labNodeGroupsRole** ở trường **Node IAM role**.
  ![VPC](/images/3.eks/ws01-createeks24.png)
  - Kéo xuống và bấm **Next**.
  ![VPC](/images/3.eks/ws01-createeks25.png)

4. Ở mục **Step 2: Set compute and scaling configuration**.
  - Chọn **Spot** ở **Capacity type**.
  - Chọn **m1.medium** ở **Instance types**.
  ![VPC](/images/3.eks/ws01-createeks26.png)
  - Kéo xuống và bấm **Next**.
  ![VPC](/images/3.eks/ws01-createeks27.png)

5. Ở mục **Step 3: Specify networking**.
  - Chọn **labPrivateSubnet01** và **labPrivateSubnet02** ở trường **Subnet**.
  - Bấm **Next**.
  ![VPC](/images/3.eks/ws01-createeks28.png)

6. Ở mục **Step 4: Review and create**.
  - Giữ mặc định và bấm **Create**.
  ![VPC](/images/3.eks/ws01-createeks29.png)
  {{% notice note %}}
  Sẽ mất một thời gian để nhóm Node được tạo thành công.
  {{% /notice %}}

7. Kiểm tra nếu **labNodeGroup01** tạo thành công hay chưa.
  ![VPC](/images/3.eks/ws01-createeks30.png)

Tiếp theo chúng ta sẽ cấu hình cụm EKS.