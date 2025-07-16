---
title : "Tạo Security Group"
date: 2025-07-01
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

### 1.3. Tạo Security Groups

#### Security Group cho EC2

1. **Truy cập Amazon EC2 Console**:
   - Mở: [https://console.aws.amazon.com/ec2/](https://console.aws.amazon.com/ec2/).
   - Chọn **Security Groups** > **Create Security Group**.
   ![image](/images/tao_sg_ec2/screenshot_1752389310.png)
2. **Cấu hình Security Group**:
   - **Name**: `ec2-sg`.
   - **Description**: "Security Group cho EC2 chạy Spring Boot và Nginx".
   - **VPC**: Chọn `spring-boot-vpc`.
      ![image](/images/tao_sg_ec2/screenshot_1752389486.png)
   - **Inbound Rules**:
     - **HTTP (80)**: Source `0.0.0.0/0` (cho phép tất cả để truy cập qua Nginx).
     - **HTTPS (443)**: Source `0.0.0.0/0` (cho môi trường sản xuất).
     - **Custom TCP (8080)**: Source `0.0.0.0/0` (chỉ để thử nghiệm, giới hạn từ Nginx trong sản xuất).
     - **SSH (22)**: Source `<your-ip>/32` (thay `<your-ip>` bằng địa chỉ IP của bạn, ví dụ: `203.0.113.1/32`).
      ![image](/images/tao_sg_ec2/screenshot_1752389534.png)
   - **Outbound Rules**: Mặc định (cho phép tất cả).
   - Nhấn **Create security group**.
      ![image](/images/tao_sg_ec2/screenshot_1752389562.png)
      ![image](/images/tao_sg_ec2/screenshot_1752389644.png)
3. **Xác minh**:
   - Kiểm tra Security Group `ec2-sg` trong **EC2 Console** để đảm bảo các quy tắc đã được áp dụng đúng.


#### Security Group cho RDS

1. **Truy cập Amazon VPC Console**:
   - Chọn **Security Groups** > **Create security group**.
2. **Cấu hình Security Group**:
   - **Name**: `rds-sg`.
   - **Description**: "Security Group cho RDS MySQL".
   - **VPC**: Chọn `spring-boot-vpc`.
   - **Inbound Rule**:
     - **Type**: MySQL/Aurora.
     - **Port**: 3306.
     - **Source**: Chọn Security Group `ec2-sg` (cho phép EC2 truy cập RDS).
![image](/images/tao_sg_rds/screenshot_1752389783.png)
   - **Outbound Rules**: Mặc định (cho phép tất cả).
   - Nhấn **Create security group**.
![image](/images/tao_sg_rds/screenshot_1752389842.png)
3. **Xác minh**:
   - Kiểm tra Security Group `rds-sg` để đảm bảo chỉ cho phép kết nối từ `ec2-sg` trên cổng 3306.
