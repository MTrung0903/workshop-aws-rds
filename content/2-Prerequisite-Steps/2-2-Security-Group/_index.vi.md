---
title : "Tạo Security Group"
date: 2025-07-01
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

#### **Security Group cho ALB**:

1. Mở **EC2 Console** > **Security Groups** > **Create Security Group**.
2. Cấu hình:
    - **Name**: `ecommerce-alb-sg`.
    - **Description**: "Security Group for ALB of E-commerce Identity Service".
    - **VPC**: `ecommerce-vpc`.
3. **Inbound rules**:
    - HTTP (80): Source `0.0.0.0/0`.
    - HTTPS (443): Source `0.0.0.0/0`.
4. **Outbound rules**: Mặc định (cho phép tất cả).
5. Chọn **Create security group**.

#### **Security Group cho EC2**:

1. Tạo Security Group:
    - **Name**: `ecommerce-ec2-sg`.
    - **Description**: "Security Group for EC2 hosting Spring Boot app".
    - **VPC**: `ecommerce-vpc`.
2. **Inbound rules**:
    - Custom TCP (8080): Source `ecommerce-alb-sg` (Security Group ID của ALB).
    - SSH (22): Source `<your-ip>/32` (ví dụ: `203.0.113.1/32`, kiểm tra IP của bạn tại [https://whatismyipaddress.com](https://whatismyipaddress.com/)).
3. **Outbound rules**: Mặc định.
4. Chọn **Create security group**.

#### **Security Group cho RDS**:

1. Tạo Security Group:
    - **Name**: `ecommerce-rds-sg`.
    - **Description**: "Security Group for RDS MySQL".
    - **VPC**: `ecommerce-vpc`.
2. **Inbound rule**:
    - MySQL/Aurora (3306): Source `ecommerce-ec2-sg`.
3. **Outbound rules**: Mặc định.
4. Chọn **Create security group**.

**⚠️ Lưu ý Bảo mật**:

- Hạn chế truy cập SSH chỉ từ IP của bạn.
- Chỉ cho phép ALB truy cập EC2 (cổng 8080) và EC2 truy cập RDS (cổng 3306) [AWS Well-Architected Framework, Security Pillar].
