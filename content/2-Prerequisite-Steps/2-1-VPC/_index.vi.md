---
title : "Tạo VPC"
date: 2025-07-01
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---
### 1.1. Tạo VPC

1. **Truy cập Amazon VPC Console**:
   - Mở trình duyệt và truy cập: [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).
   ![image](/images/tao_vpc/screenshot_1752387940.png)
   - Chọn **Create VPC** > **VPC and more**.
   ![image](/images/tao_vpc/screenshot_1752387940.png)
2. **Cấu hình VPC**:
   - **Name tag auto-generation**: `spring-boot-vpc`.
   - **IPv4 CIDR block**: `10.0.0.0/16`.
   ![image](/images/tao_vpc/screenshot_1752388342.png)
   - **Availability Zones (AZs)**: Chọn ít nhất 2 AZs (ví dụ: `us-east-1a`, `us-east-1b`).
   - **Subnets**: 
     - 2 public subnets (cho EC2).
     - 2 private subnets (cho RDS).
   - **NAT Gateways**: 1 per AZ (để private subnets truy cập internet).
   ![image](/images/tao_vpc/screenshot_1752388383.png)
   - **VPC endpoints**: None (hoặc chọn **S3 Gateway** nếu cần).
   - **DNS options**: Bật **Enable DNS hostnames** và **Enable DNS resolution**.
   ![image](/images/tao_vpc/screenshot_1752388459.png)
   - Nhấn **Create VPC**.
   ![image](/images/tao_vpc/screenshot_1752388666.png)

3. **Xác minh**:
   - Kiểm tra trong **VPC Console** để đảm bảo VPC `spring-boot-vpc` đã được tạo với 4 subnets (2 public, 2 private) và các tài nguyên liên quan (Internet Gateway, Route Tables, NAT Gateways).

### 1.2. Cấu hình Public Subnets

1. **Truy cập Subnets**:
   - Trong **Amazon VPC Console**, chọn **Subnets**.
   - Đảm bảo các public subnets được đặt tên như: `spring-boot-vpc-public-us-east-1a`, `spring-boot-vpc-public-us-east-1b`.
   ![image](/images/cau_hinh_public_subnets/screenshot_1752388960.png)
2. **Bật Public IP**:
   - Chọn từng public subnet, nhấn **Actions** > **Edit subnet settings**.
   - Bật **Enable auto-assign public IPv4 address**.
   - Nhấn **Save**.
   ![image](/images/cau_hinh_public_subnets/screenshot_1752388997.png)

3. **Xác minh**:
   - Kiểm tra cả hai public subnets đã bật auto-assign Public IP.
   ![image](/images/cau_hinh_public_subnets/screenshot_1752389021.png)
4. **Lặp lại cho public subnet thứ hai.**
   ![image](/images/cau_hinh_public_subnets/screenshot_1752389143.png)
   ![image](/images/cau_hinh_public_subnets/screenshot_1752389179.png)