---
title : "Tạo cụm EKS"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

### Tổng quan
**Một cụm Amazon EKS (Elastic Kubernetes Service)** là dịch vụ Kubernetes được quản lý giúp dễ dàng triển khai, quản lý và mở rộng quy mô các ứng dụng được chứa trong container bằng Kubernetes trên AWS. Với EKS, AWS xử lý việc quản lý và vận hành mặt phẳng điều khiển Kubernetes, bao gồm vá lỗi, nâng cấp và mở rộng quy mô, cho phép bạn tập trung vào việc triển khai và quản lý các ứng dụng của mình.

Các tính năng chính của cụm EKS bao gồm:

- **Managed Kubernetes Control Plane**: AWS quản lý Kubernetes control plane có tính khả dụng cao, bao gồm máy chủ API, etcd và các thành phần quan trọng khác.
- **Worker Nodes**: EKS hỗ trợ cả các worker node được quản lý và tự quản lý, nơi các container chạy. Các node này có thể là các phiên bản EC2 hoặc AWS Fargate, một công cụ tính toán không có máy chủ dành cho container.
Tích hợp với AWS Services: EKS tích hợp liền mạch với các dịch vụ AWS khác như IAM, VPC, ECR và CloudWatch, cung cấp khả năng bảo mật, kết nối mạng và giám sát nâng cao.
- **Tính khả dụng và khả năng mở rộng cao**: EKS tự động phân phối và sao chép control plane trên nhiều Vùng khả dụng, đảm bảo tính khả dụng cao. Nó cũng hỗ trợ khả năng tự động mở rộng các worker node.

**EKS** lý tưởng để chạy khối lượng công việc Kubernetes cấp sản xuất trên AWS, cung cấp môi trường an toàn, đáng tin cậy và có khả năng mở rộng cho các ứng dụng được chứa trong container.

{{% notice info %}}
Đọc thêm: https://aws.amazon.com/eks/
{{% /notice %}}

Ở bước này, chúng ta sẽ tạo Cụm EKS, nằm trong các mạng con riêng tư.

### Content
3.1. [Tạo cụm EKS](3.1-createekscluster/) \
3.2. [Tạo Node groups](3.2-createnodegroups/) \
3.3. [Cấu hình cụm EKS](3.3-configureekscluster/) 