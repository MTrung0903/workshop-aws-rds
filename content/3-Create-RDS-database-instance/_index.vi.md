---
title : "Tạo RDS database instance"
date: 2025-07-01
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

### Tạo RDS Database Instance
1. Mở Amazon RDS Console > Create database.
2. Chọn Standard create > Engine type: MySQL.
3. Version: Chọn phiên bản mới nhất (ví dụ, MySQL 8.0.41).
4. Templates: Chọn Production để bật Multi-AZ và bảo vệ xóa.
5. Settings:
    - DB instance identifier: database-workshop.
    - Master username: admin.
    - Master password: trung09032003 (hoặc chọn Auto generate a password).
6. DB instance class: Chọn db.t3.micro.
7. Storage: Giữ mặc định hoặc tùy chỉnh (ví dụ, 20 GB).
8. Connectivity:
    - VPC: Chọn workshop-aws-rds-vpc.
    - DB Subnet Group: Chọn rds-subnet-group.
    - VPC security group: Chọn rds-sg.
9. Chọn Create database.
10. Nếu chọn mật khẩu tự động, xem thông tin xác thực qua View credential details.
11. Chờ instance chuyển sang trạng thái Available.
12. Ghi lại Endpoint: database-workshop.ctsk2qmig8wy.ap-southeast-2.rds.amazonaws.com, Port: 3306, Username: admin, và Password: trung09032003.