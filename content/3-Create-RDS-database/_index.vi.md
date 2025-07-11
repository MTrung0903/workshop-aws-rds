---
title : "Tạo RDS database"
date: 2025-07-01
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

### Tạo RDS Database Instance
1. Mở **RDS Console** > **Create database**.

2. Chọn **Standard create** > **Engine type**: MySQL 8.0.

3. **Templates**: Production (bật Multi-AZ) [AWS RDS Pricing].

4. **Settings**:
    - **DB instance identifier**: `ecommerce-rds-instance`.
    - **Master username**: `admin`.
    - **Master password**: Auto-generate hoặc tùy chỉnh (lưu ý: sử dụng mật khẩu mạnh, ví dụ: `P@ssw0rd123!`).

5. **DB instance class**: `db.t3.micro` (1 vCPU, 1 GB RAM).

6. **Storage**: 20 GB, General Purpose SSD (gp2).

7. **Connectivity**:
    - **VPC**: `ecommerce-vpc`.
    - **DB Subnet Group**: `ecommerce-rds-subnet-group`.
    - **Security Group**: `ecommerce-rds-sg`.
    - **Public access**: No.

8. **Additional configuration**:
    - Kích hoạt **Automated backups** (7-day retention).
    - Kích hoạt **Encryption** (AES-256).

9. Chọn **Create database**.

10. Ghi lại **Endpoint** (ví dụ: `ecommerce-rds-instance.abc123.us-east-1.rds.amazonaws.com`), **Port** (3306), **Username**, **Password** (xem qua **View credential details** nếu auto-generate).

