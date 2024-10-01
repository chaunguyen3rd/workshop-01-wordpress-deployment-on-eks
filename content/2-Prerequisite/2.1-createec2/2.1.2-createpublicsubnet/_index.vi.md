---
title : "Tạo mạng con công cộng"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.1.2 </b> "
---

#### Tạo mạng con công cộng

1. Bấm **Subnets**.
  + Bấm **Create subnet**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc03.png)

2. Ở trang **Create subnet**.
  + Ở mục **VPC ID**, Bấm **labVPC01**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc04.png)

2. Ở mục **Subnet settings**.
  - Ở mục **Subnet 1 of 1**.
    + Ở trường **Subnet name**, nhập **labPublicSubnet01**.
    + Ở **Availability Zone**, chọn **US EAST (N. Virginia) / us-east-1a**.
    + Ở trường **IPv4 CIDR block** nhập **10.0.1.0/24**.
    + Bấm **Add new subnet**.
    ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc05.png)

  - Ở mục **Subnet 2 of 2**.
    + Ở trường **Subnet name**, nhập **labPublicSubnet02**.
    + Ở trường **Availability Zone**, chọn **US EAST (N. Virginia) / us-east-1b**.
    + Ở trường **IPv4 CIDR block**, nhập **10.0.2.0/24**.
    + Bấm **Add new subnet**.
    ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc06.png)

  - Ở mục **Subnet 3 of 3**.
    + Ở trường **Subnet name**, nhập **labPublicSubnet03**.
    + Ở **Availability Zone**, chọn **US EAST (N. Virginia) / us-east-1c**.
    + Ở trường **IPv4 CIDR block**, nhập **10.0.3.0/24**.
    + Bấm **Create subnet**.
    ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc07.png)

4. Bấm **labPublicSubnet01**.
  + Bấm **Actions**.
  + Bấm **Edit subnet settings**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc08.png)

5. Bấm **Enable auto-assign public IPv4 address**.
  + Bấm **Save**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc09.png)

6. Bấm **Internet Gateways**.
  + Bấm **Create internet gateway**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc10.png)

7. Ở trang **Create internet gateway**.
  + Ở trường **Name tag**, nhập **labIGW01**.
  + Bấm **Create internet gateway**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc11.png)

8. Sau khi tạo thành công, Bấm **Actions**.
  + Bấm **Attach to VPC**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc12.png)

9. Ở trang **Attach to VPC**.
  + Ở **Available VPCs**, chọn **labVPC01**.
  + Bấm **Attach internet gateway**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc13.png)

10. Tiếp theo chúng ta sẽ tạo một bảng định tuyến tùy chỉnh để gán cho **labPublicSubnet01, labPublicSubnet02 và labPublicSubnet03**.
  + Bấm **Route Tables**.
  + Bấm **Create route table**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc14.png)

11. Ở trang **Create route table**.
  + Ở trường **Name**, nhập **labPublicRT01**.
  + Ở **VPC**, chọn **labVPC01**.
  + Bấm **Create route table**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc15.png)

12. Sau khi tạo bảng định tuyến thành công.
  + Bấm **Edit routes**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc16.png)

13. Ở trang **Edit routes**.
  + Bấm **Add route**.
  + Ở **Destination** field, nhập 0.0.0.0/0
  + Ở **Target**, chọn **Internet Gateway** và chọn **labIGW01**.
  + Bấm **Save changes**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc17.png)

14. Bấm vào tab **Subnet associations**.
  + Bấm **Edit subnet associations** để tiến hành liên kết bảng định tuyến tùy chỉnh mà chúng ta vừa tạo trong **Lab Public Subnet**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc18.png)

15. Ở trang **Edit subnet associations**.
  + Bấm chọn **Name** để chọn tất cả **labPublicSubnet0\***.
  + Bấm **Save associations**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc19.png)

16. Kiểm tra mục thông tin bảng tuyến đường đã được liên kết với 3 **labPublicSubnet0\*** và thông tin tuyến đường internet đã được chuyển đến Cổng Internet như hiển thị bên dưới.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc20.png)

Tiếp theo, chúng ta sẽ tạo mạng con riêng tư.