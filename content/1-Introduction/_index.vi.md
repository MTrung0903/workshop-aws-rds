---
title : "Giới thiệu"
date: 2025-07-01
weight : 1
chapter : false
pre : " <b> 1. </b> "
---
# Hướng dẫn triển khai ứng dụng Spring Boot trên AWS với Docker

ℹ️ **Thông tin**: Tài liệu này hướng dẫn triển khai ứng dụng Spring Boot (Backend) trên Docker, sử dụng các dịch vụ AWS như EC2, RDS, và ECR, tích hợp Nginx làm reverse proxy. Hướng dẫn được cập nhật với các tính năng AWS mới nhất (tính đến năm 2025) và tối ưu hóa cho môi trường sản xuất.

## Mục tiêu

- Triển khai ứng dụng Spring Boot từ Docker image trên Amazon ECR.
- Sử dụng Nginx làm reverse proxy để điều phối lưu lượng đến Backend.
- Kết nối ứng dụng với cơ sở dữ liệu MySQL trên Amazon RDS .
- Đảm bảo bảo mật, khả năng sẵn sàng cao (Multi-AZ), và dễ dàng dọn dẹp tài nguyên.

## Nội dung chính

1. Chuẩn bị cơ sở hạ tầng
2. Tạo và đẩy image lên Amazon ECR
3. Tạo EC2 Instance
4. Cài đặt Docker, Nginx, và MySQL Client trên EC2
5. Tạo RDS Database Instance
6. Triển khai ứng dụng Spring Boot với Docker Compose
7. Kiểm tra ứng dụng
8. Dọn dẹp tài nguyên

💡 **Mẹo hữu ích**: Sử dụng **Amazon ECS** hoặc **EKS** thay vì chạy Docker trực tiếp trên EC2 để quản lý container hiệu quả hơn trong môi trường sản xuất.

🔒 **Lưu ý bảo mật**: Đảm bảo cấu hình Security Groups và VPC đúng cách, hạn chế quyền truy cập, và sử dụng AWS Secrets Manager để quản lý thông tin nhạy cảm.

⚠️ **Cảnh báo**: Theo dõi chi phí AWS qua **AWS Cost Explorer** và dọn dẹp tài nguyên sau khi hoàn thành để tránh phát sinh chi phí không cần thiết.