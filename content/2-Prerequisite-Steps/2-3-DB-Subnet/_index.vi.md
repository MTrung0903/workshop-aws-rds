---
title : "Tạo DB Subnet Group"
date: 2025-07-01
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---
### 1.4. Tạo DB Subnet Group

1. **Truy cập Amazon RDS Console**:
   - Mở: [https://console.aws.amazon.com/rds/](https://console.aws.amazon.com/rds/).
   - Chọn **Subnet groups** > **Create DB Subnet Group**.
![image](/images/tao_db_subnet_group/screenshot_1752390108.png)
2. **Cấu hình DB Subnet Group**:
   - **Name**: `rds-subnet-group`.
   - **Description**: "DB Subnet Group cho Spring Boot".
   - **VPC**: Chọn `spring-boot-vpc`.
   ![image](/images/tao_db_subnet_group/screenshot_1752390165.png)
   - **Add subnets**: Chọn 2 private subnets (ví dụ: `spring-boot-vpc-private-us-east-1a`, `spring-boot-vpc-private-us-east-1b`).
   ![image](/images/tao_db_subnet_group/screenshot_1752390313.png)
   - Nhấn **Create**.
![image](/images/tao_db_subnet_group/screenshot_1752390329.png)
3. **Xác minh**:
   - Kiểm tra trong **RDS Console** để đảm bảo `rds-subnet-group` đã được tạo với 2 private subnets.