---
title : " Hướng dẫn triển khai ứng dụng Spring Boot trên AWS với Docker"
date: 2025-07-01
weight : 1 
chapter : false
---

# Hướng dẫn triển khai ứng dụng Spring Boot trên AWS với Docker

## Thông tin chung

Tài liệu này hướng dẫn triển khai một ứng dụng Spring Boot (backend API) sử dụng Docker trên Amazon EC2, tích hợp với Amazon ECR để lưu trữ Docker image, Amazon RDS cho cơ sở dữ liệu MySQL, và Nginx làm reverse proxy. Hướng dẫn được cập nhật với các tính năng AWS mới nhất (tính đến tháng 7/2025) và tối ưu hóa cho môi trường sản xuất, đồng thời tận dụng AWS Free Tier để giảm thiểu chi phí.

---

## Mục tiêu

- Tạo và đẩy Docker image của ứng dụng Spring Boot lên Amazon ECR.
- Triển khai ứng dụng trên Amazon EC2 sử dụng Docker Compose.
- Sử dụng Nginx làm reverse proxy để điều hướng lưu lượng từ cổng 80 đến Spring Boot trên cổng 8080.
- Kết nối ứng dụng với cơ sở dữ liệu MySQL trên Amazon RDS (database `first_cloud_users`).
- Đảm bảo bảo mật, khả năng sẵn sàng cao (Multi-AZ), và dễ dàng dọn dẹp tài nguyên.

---

## Giả định

- Bạn đã có một **Docker image Spring Boot** (ví dụ: `trungho93/identity-service:0.9.0`) đã được kiểm tra hoạt động tốt trên môi trường cục bộ hoặc Docker Hub.
- Ứng dụng Spring Boot có cấu hình database trong file `application.yml` hoặc `application.properties` như sau:

```yaml
spring:
  datasource:
    url: ${DBMS_CONNECTION:jdbc:mysql://localhost:3306/first_cloud_users?useSSL=false&serverTimezone=UTC}
    driverClassName: com.mysql.cj.jdbc.Driver
    username: ${DBMS_USERNAME:root}
    password: ${DBMS_PASSWORD:09032003}
  jpa:
    hibernate:
      ddl-auto: update
```

- Ứng dụng sử dụng cổng **8080** (mặc định của Spring Boot).
- Bạn có quyền truy cập vào:
  - **AWS Management Console**.
  - **AWS CLI** (phiên bản 2.x).
  - **Docker CLI** (phiên bản mới nhất).
  - Cặp khóa SSH (file `.pem`) để truy cập EC2.
- Máy cục bộ có quyền root hoặc sudo để cài đặt công cụ.
- Bạn đã cài đặt **MobaXterm** để kết nối SSH vào EC2.

---

## Nội dung chính

1. Chuẩn bị hạ tầng (VPC, Security Groups, IAM Role, DB Subnet Group).
2. Tạo và đẩy Docker image lên Amazon ECR.
3. Tạo EC2 instance.
4. Cài đặt Docker, Nginx, và MySQL Client trên EC2.
5. Tạo RDS database instance.
6. Triển khai ứng dụng với Docker Compose.
7. Kiểm tra ứng dụng.
8. Dọn dẹp tài nguyên.

---

## Lưu ý quan trọng

- **Mẹo hữu ích**: Xem xét sử dụng Amazon ECS hoặc EKS để quản lý container trong môi trường sản xuất, thay vì chạy trực tiếp trên EC2.
- **Bảo mật**: Cấu hình Security Groups và VPC đúng cách, sử dụng AWS Secrets Manager để quản lý thông tin nhạy cảm.
- **Chi phí**: Theo dõi chi phí qua **AWS Cost Explorer** và dọn dẹp tài nguyên sau workshop để tránh phát sinh chi phí.

---