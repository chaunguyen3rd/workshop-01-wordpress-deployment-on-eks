---
title : "Chuẩn bị "
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

{{% notice info %}}
Bạn cần tạo một máy Linux trên mạng con công cộng để truy cập vào cụm EKS trong mạng con riêng tư.
{{% /notice %}}

Để tìm hiểu cách tạo các phiên bản EC2 và VPC với mạng con công khai/riêng tư, bạn có thể tham khảo các bài lab sau:
- [Về Amazon EC2](https://000004.awsstudygroup.com/en/)
- [Về VPC](https://000003.awsstudygroup.com/en/)

Để triển khai ứng dụng Wordpress trên cụm EKS, chúng ta cần cấp quyền cho Bastion host để có thể tạo và vận hành ứng dụng Wordpress trên cụm EKS. Trong phần chuẩn bị này, chúng ta sẽ tạo VPC, IAM role, EC2 Bastion host, EFS, ... để có thể hoàn thành bài lab này.

### Content
- [Chuẩn bị VPC và EC2](2.1-createec2/)
- [Tạo IAM Role](2.2-createiamrole/)