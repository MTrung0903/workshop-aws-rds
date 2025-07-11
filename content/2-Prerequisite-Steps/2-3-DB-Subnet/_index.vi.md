---
title : "Tạo DB Subnet Group"
date: 2025-07-01
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---
### Tạo DB Subnet Group

1. Mở **RDS Console** > **Subnet groups** > **Create DB Subnet Group**.
2. Cấu hình:
    - **Name**: `ecommerce-rds-subnet-group`.
    - **Description**: "DB Subnet Group for E-commerce RDS".
    - **VPC**: `ecommerce-vpc`.
3. **Add subnets**: Chọn 2 private subnets (`ecommerce-vpc-private-us-east-1a`, `ecommerce-vpc-private-us-east-1b`).
4. Chọn **Create**.