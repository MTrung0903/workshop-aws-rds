---
title : "Create RDS database"
date: 2025-07-01
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

## 6. Tạo RDS Database Instance

1. **Truy cập Amazon RDS Console**:
   - Mở: [https://console.aws.amazon.com/rds/](https://console.aws.amazon.com/rds/).
   - Chọn **Create database**.

2. **Cấu hình RDS**:
   - **Method**: Standard create.
   - **Engine**: MySQL.
   - **Version**: MySQL 8.0 (mới nhất).
   - **Template**: Dev/Test.
   - **Multi-AZ**: DB instance (cho khả năng sẵn sàng cao).
   - **DB instance identifier**: `spring-boot-rds`.
   - **Master username**: `admin`.
   - **Master password**: Nhập mật khẩu an toàn (ví dụ: `SecurePass123!`) hoặc chọn auto-generate.
   - **Instance class**: `db.t3.micro` (Free Tier eligible).
   - **Storage**: 20 GB, General Purpose SSD.
   - **VPC**: Chọn `spring-boot-vpc`.
   - **DB Subnet Group**: Chọn `rds-subnet-group`.
   - **Security Group**: Chọn `rds-sg`.
   - Nhấn **Create database**.

3. **Lưu thông tin RDS**:
   - Ghi lại:
     - **Endpoint**: Ví dụ `spring-boot-rds.cghg6wmuybac.us-east-1.rds.amazonaws.com`.
     - **Port**: 3306.
     - **Username**: `admin`.
     - **Password**: Mật khẩu đã thiết lập.

4. **Kiểm tra kết nối RDS từ EC2**:
   - Trong MobaXterm, chạy:
     ```bash
     mysql -h spring-boot-rds.cghg6wmuybac.us-east-1.rds.amazonaws.com -u admin -p
     ```
   - Nhập mật khẩu RDS.
   - Tạo và kiểm tra database:
     ```sql
     SHOW DATABASES;
     CREATE DATABASE first_cloud_users;
     USE first_cloud_users;
     ```

---