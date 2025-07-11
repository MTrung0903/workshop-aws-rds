---
title : "Dọn dẹp tài nguyên"
date: 2025-07-01
weight : 9
chapter : false
pre : " <b> 9. </b> "
---

### Dọn dẹp Tài nguyên

Để tránh chi phí không cần thiết, dọn dẹp tài nguyên sau khi hoàn thành [AWS Pricing Calculator]:

1. **Dọn dẹp Auto Scaling Group**:
    - Mở **EC2 Console** > **Auto Scaling Groups** > Chọn `ecommerce-spring-boot-asg` > **Delete**.
2. **Dọn dẹp ALB**:
    - Mở **EC2 Console** > **Load Balancers** > Chọn `ecommerce-app-alb` > **Delete**.
    - Xóa target groups: `ecommerce-app-tg`, `ecommerce-app-tg-green`.
3. **Dọn dẹp RDS**:
    - Mở **RDS Console** > **Databases** > Chọn `ecommerce-rds-instance` > **Delete** (bỏ chọn **Create final snapshot**, nhập `delete me`).
    - Xóa **Subnet groups** > `ecommerce-rds-subnet-group`.
4. **Dọn dẹp VPC**:
    - Mở **VPC Console** > **Security Groups** > Xóa `ecommerce-alb-sg`, `ecommerce-ec2-sg`, `ecommerce-rds-sg`.
    - Xóa **NAT Gateways** và **VPC** (`ecommerce-vpc`).
5. **Dọn dẹp CloudWatch**:
    - Mở **CloudWatch Console** > **Log groups** > Xóa `ecommerce-app-logs`.
    - Xóa **Alarms** (`EcommerceHighCPU`) và **Dashboards** (`EcommerceApp-Dashboard`).
6. **Dọn dẹp IAM Role**:
    - Mở **IAM Console** > **Roles** > Xóa `ecommerce-ec2-cloudwatch-role`.

**⚠️ Cảnh báo**: Sao lưu dữ liệu RDS trước khi xóa (export qua MySQL Workbench), vì các hành động này không thể hoàn tác.
