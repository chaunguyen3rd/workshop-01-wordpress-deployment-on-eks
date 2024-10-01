---
title: "Tạo mạng con riêng tư"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 2.1.3 </b> "
---

#### Tạo mạng con riêng tư

1. Bấm **Subnets**.

- Bấm **Create subnet**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc21.png)

2. Ở trang **Create subnet**.

- Ở mục **VPC ID**, bấm **labVPC01**.
- Bấm **Add new subnet**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc22.png)
- Ở mục **Subnet 1 of 1**.
  - Ở trường **Subnet name**, nhập **labPrivateSubnet01**.
  - Ở mục **Availability Zone**, chọn **US EAST (N. Virginia) / us-east-1a**.
  - Ở mục **IPv4 CIDR block**, nhập **10.0.11.0/24**.
  - Bấm **Add new subnet**.
    ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc23.png)
- Ở mục **Subnet 2 of 2**.
  - Ở trường **Subnet name**, nhập **labPrivateSubnet02**.
  - Ở mục **Availability Zone**, chọn **US EAST (N. Virginia) / us-east-1b**.
  - Ở trường **IPv4 CIDR block**, nhập **10.0.12.0/24**.
  - Bấm **Create subnet**.
    ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc24.png)

3. Ở **VPC dashboard**.

- Bấm **NAT gateways**.
- Bấm **Create NAT gateway** button.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc26.png)

4. Ở trang **Create NAT gateway**.

- Nhập **labNATGW01** ở trường **Name**.
- Chọn **labPublicSubnet01** subnet.
- Chọn **Public** Connectivity type.
- Bấm **Allocate Elastic IP** ở trường **Elastic IP allocation ID**.
- Bấm **Create NAT gateway**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc27.png)

5. Ở **VPC dashboard**.

- Bấm **Route tables**.
- Bấm **Create route table**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc28.png)

6. Ở trang **Create route table**.

- Nhập **labPrivateRT01** ở trường **Name**.
- Chọn trường **labVPC01** ở **VPC**.
- Bấm **Create route table**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc29.png)

7. Ở **labPrivateRT01** page.

- Choose **Subnets associations** tab.
- Bấm **Edit subnets associations**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc30.png)

8. Ở trang **Edit subnet associations**.

- Chọn **labPrivateSubnet01** và **labPrivateSubnet02**.
- Bấm **Save associations**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc31.png)

9. Ở trang **labPrivateRT01**.

- Chọn tab **Routes**.
- Bấm **Edit routes**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc32.png)

10. Ở trang **Edit routes**.

- Bấm **Add route**.
- Chọn **0.0.0.0/0** ở trường **Destination**.
- Chọn **NAT gateway** và bấm **NAT gateway** đã tạo từ trước.
- Bấm **Save changes**.
  ![VPC](/workshop.chaunguyen.site/images//2.prerequisite/ws01-createvpc33.png)

Bước tiếp theo là tạo các security groups cần thiết cho bài lab.
