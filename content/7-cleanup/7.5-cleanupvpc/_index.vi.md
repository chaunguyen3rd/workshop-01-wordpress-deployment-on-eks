---
title: "Dọn dẹp VPC"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: " <b> 7.5 </b> "
---

### Dọn dẹp VPC

#### Dọn dẹp Route table

1. Đi đến [VPC service management console](https://console.aws.amazon.com/vpc/home)

- Bấm **Route tables**.
- Chọn **labPublicRT01**.
- Bấm **Subnet associations**.
- Bấm **Edit subnet associations**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup13.png)

2. Ở trang **Edit subnet associations**.

- Bỏ chọn tất các các mạng con có sẵn
- Bấm **Save associations**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup14.png)

3. Đi đến [VPC service management console](https://console.aws.amazon.com/vpc/home)

- Bấm **Route tables**.
- Chọn **labPrivateRT01**.
- Bấm **Subnet associations**.
- Bấm **Edit subnet associations**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup15.png)

4. Ở trang **Edit subnet associations**.

- Bỏ chọn tất các các mạng con có sẵn
- Bấm **Save associations**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup14.png)

5. Đi đến [VPC service management console](https://console.aws.amazon.com/vpc/home)

- Bấm **Route tables**.
- Chọn **labPrivateRT01** và **labPublicRT01**.
- Bấm **Actions**.
- Bấm **Delete route table**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup16.png)
- Ở popup, nhập **delete** và bấm **Delete**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup17.png)

#### Cleanup NAT gateways

1. Đi đến [VPC service management console](https://console.aws.amazon.com/vpc/home)

- Bấm **NAT gateways**.
- Chọn **labNATGW01**.
- Bấm **Actions**.
- Bấm **Delete NAT gateway**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup18.png)

2. Đi đến [VPC service management console](https://console.aws.amazon.com/vpc/home)

- Bấm **Elastic IPs**.
- Bấm **52.6.199.235**. Thay đổi `52.6.199.235` thành **Elastic IP** của bạn.
- Bấm **Actions**.
- Bấm **Release Elastic IP addresses**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup19.png)
- Ở popup, bấm **Release**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup20.png)

#### Cleanup Internet gateways

1. Đi đến [VPC service management console](https://console.aws.amazon.com/vpc/home)

- Bấm **Internet gateways**.
- Chọn **labIGW01**.
- Bấm **Actions**.
- Bấm **Detach from VPC**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup21.png)
- Ở popup, bấm **Detach internet gateway**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup22.png)

2. At [VPC service management console](https://console.aws.amazon.com/vpc/home) page.

- Bấm **Internet gateways**.
- Chọn **labIGW01**.
- Bấm **Actions**.
- Bấm **Delete internet gateway**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup23.png)
- At the popup, gõ **delete** và bấm **Delete internet gateway**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup24.png)

#### Cleanup VPC

1. Đi đến [VPC service management console](https://console.aws.amazon.com/vpc/home)

- Bấm **Your VPCs**.
- Chọn **labVPC01**.
- Bấm **Actions**.
- Bấm **Delete VPC**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup27.png)
- Ở popup, gõ **delete** và bấm **Delete**.
  ![Cleanup](/workshop.chaunguyen.site/images//7.cleanup/ws01-cleanup28.png)

Tiếp theo, chúng ta sẽ dọn dẹp vai trò và chính sách IAM.
