---
title: "Tạo security groups"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 2.1.4 </b> "
---

#### Tạo security groups

Trong bước này, chúng ta sẽ tiến hành tạo các security groups được sử dụng cho máy chủ Bastion của chúng ta. Như bạn có thể thấy, các nhóm bảo mật này sẽ không cần phải mở các cổng truyền thống để **ssh** như cổng **22**.

#### Tạo security group cho máy Linux nằm trong mạng con công cộng

1. Đi đến [VPC service management console](https://console.aws.amazon.com/vpc)

- Bấm **Security Group**.
- Bấm **Create security group**.
  ![SG](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createsg01.png)

2. Ở trường **Security group name**, nhập **labBastionHostSG01**.

- Ở mục **Description**, nhập **labBastionHostSG01**.
- Ở mục **VPC**, bấm **X** để chọn lại **labVPC01** bạn đã tạo ra cho bài lab này.
  ![SG](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createsg02.png)

3. Ở mục **Inbound rules**.

- Thêm loại **SSH rule** để cho phép kết nối TCP 22 từ 0.0.0.0/0.
  ![SG](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createsg03.png)

4. Giữ **Outbound rule** mặc định, kéo chuột xuống dưới.

- Bấm **Create security group**.

{{%notice tip%}}
Như bạn có thể thấy, security groups mà chúng ta tạo ra để sử dụng cho các phiên bản Linux công khai sẽ không cần phải mở các cổng truyền thống tới **ssh** như cổng **22**.
{{%/notice%}}

#### Tạo security groups cho cụm EKS nằm trong mạng con riêng

1. Sau khi tạo thành công security groups cho máy Linux nằm trong mạng con công khai, hãy nhấp vào liên kết security groups để quay lại danh sách security groups.
   ![SG](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createsg04.png)

2. Bấm **Create security group**.

3. Ở trường **Security group name**, nhập **labEKSClusterSG01**.

- Ở mục **Description**, nhập **labEKSClusterSG01**.
- Ở mục **VPC**, bấm **X** để chọn lại **labVPC01** bạn đã tạo ra cho bài lab này.
  ![SG](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createsg05.png)

4. Kéo xuống.

- Thêm **Inbound rule** để cho phép kết nối TCP từ 10.0.0.0/16 (CIDR của **labVPC01** chúng ta đã tạo ra).
- Giữ **Outbound rule** mặc định, kéo chuột xuống dưới.
- Bấm **Create security group**.
  ![SG](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createsg06.png)

#### Tạo security group cho EFS

1. Trong bước này, chúng ta sẽ tạo security groups cho **EFS**.

2. Sau khi tạo thành công security groups cho cụm EKS trong mạng con riêng, hãy nhấp vào liên kết security groups để quay lại danh sách security groups.
   ![SG](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createsg07.png)

3. Bấm **Create security group**.

4. Ở trường **Security group name**, nhập **labEFSSG01**.

- Ở mục **Description**, nhập **labEFSSG01**.
- Ở mục **VPC**, bấm **X** để chọn lại **labVPC01** bạn đã tạo ra cho bài lab này.
  ![SG](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createsg08.png)

5. Kéo xuống.

- Thêm **Inbound rule** để cho phép kết nối TCP từ 10.0.0.0/16 (CIDR của **labVPC01** chúng ta đã tạo ra).
- Giữ **Outbound rule** mặc định, kéo chuột xuống dưới.
- Bấm **Create security group**.
  ![SG](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createsg09.png)

Vậy là chúng ta đã tạo xong các security groups cần thiết cho EC2 instance, EKS cluster và EFS. Tiếp theo, chúng ta sẽ tạo EC2 linux bastion host.
