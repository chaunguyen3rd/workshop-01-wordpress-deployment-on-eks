---
title : "Tạo VPC"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1.1 </b> "
---

#### Tạo VPC **labVPC01**
1. Đi đến [VPC service management console](https://console.aws.amazon.com/vpc/home)
  - Bấm **Your VPC**.
  - Bấm **Create VPC**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc01.png)

2. Ở trang **Create VPC**.
  - Ở trường **Name tag**, nhập **labVPC01**.
  - Ở trường **IPv4 CIDR**, nhập: **10.0.0.0/16**.
  - Bấm **Create VPC**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createvpc02.png)

Tiếp theo, chúng ta sẽ tạo ra mạng con công cộng.