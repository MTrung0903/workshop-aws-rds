---
title : "Các bước chuẩn bị"
date: 2025-07-01
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

#### Các bước chuẩn bị
**Information**: Trước khi triển khai Amazon RDS, bạn cần thiết lập môi trường mạng và bảo mật phù hợp. Các bước dưới đây sẽ giúp bạn chuẩn bị cơ sở hạ tầng cần thiết.

1. Tạo VPC - Môi trường mạng ảo riêng biệt cho tài nguyên AWS của bạn
2. Tạo subnet - Phân đoạn mạng trong VPC cho việc triển khai đa vùng sẵn sàng (Multi-AZ)
3. Tạo Security Group cho Amazon EC2 - Kiểm soát lưu lượng mạng đến và đi từ máy chủ ứng dụng
4. Tạo Security Group cho DB instance - Kiểm soát quyền truy cập mạng đến cơ sở dữ liệu RDS
5. Tạo DB Subnet group - Xác định các subnet mà Amazon RDS có thể sử dụng trong VPC của bạn
