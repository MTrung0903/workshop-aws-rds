---
title : "Tạo VPC"
date: 2025-07-01
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---
 ### Tạo VPC
1. Mở **Amazon VPC Console**: https://console.aws.amazon.com/vpc/.
2. Chọn **Create VPC** > **VPC and more**.
3. Cấu hình:
    - **Name tag auto-generation**: `ecommerce-vpc`.
    - **IPv4 CIDR block**: `10.0.0.0/16`.
    - **Tenancy**: Default.
    - **Availability Zones (AZs)**: Chọn 2 AZs (`us-east-1a`, `us-east-1b`).
    - **Subnets**:
        - 2 public subnets: `ecommerce-vpc-public-us-east-1a` (`10.0.1.0/24`), `ecommerce-vpc-public-us-east-1b` (`10.0.2.0/24`).
        - 2 private subnets: `ecommerce-vpc-private-us-east-1a` (`10.0.3.0/24`), `ecommerce-vpc-private-us-east-1b` (`10.0.4.0/24`).
    - **NAT Gateways**: 1 per AZ (2 tổng cộng).
    - **DNS options**: Kích hoạt **DNS hostnames** và **DNS resolution**.
4. Chọn **Create VPC**.

###  Cấu hình Địa chỉ IPv4 Công khai cho Subnet

1. Mở **VPC Console** > **Subnets**.
2. Chọn public subnet (ví dụ: `ecommerce-vpc-public-us-east-1a`).
3. Chọn **Actions** > **Edit subnet settings**.
4. Đánh dấu **Enable auto-assign public IPv4 address** > **Save**.