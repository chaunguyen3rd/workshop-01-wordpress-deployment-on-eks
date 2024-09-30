---
title : "Chuẩn bị VPC và EC2"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

Ở bước này, chúng ta sẽ cần tạo một VPC với 3 mạng con công cộng và 2 mạng con riêng tư. Sau đó tạo 1 EC2 Linux nằm trong mạng con công cộng.

Tổng quan về kiến ​​trúc sau khi bạn hoàn tất bước này sẽ như sau:

![VPC](/images/2.prerequisite/ws01-prep01.png)

Để tìm hiểu cách tạo các phiên bản EC2 và VPC với mạng con công khai/riêng tư, bạn có thể tham khảo các bài lab sau:
- [Về Amazon EC2](https://000004.awsstudygroup.com/en/)
- [Về VPC](https://000003.awsstudygroup.com/en/)

### Nội dung
- [Tạo VPC](2.1.1-createvpc/)
- [Tạo mạng con công khai](2.1.2-createpublicsubnet/)
- [Tạo mạng con riêng tư](2.1.3-createprivatesubnet/)
- [Tạo security group](2.1.4-createsecgroup/)
- [Tạo máy chủ Linux công khai](2.1.5-createec2linux/)
- [Cấu hình máy chủ Linux công khai](2.1.6-configureec2linux/)