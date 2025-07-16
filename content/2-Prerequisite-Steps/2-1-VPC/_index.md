---
title : "Create VPC"
date: 2025-07-01
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---
### 1.1. Create VPC

1. **Access Amazon VPC Console**:
- Open a browser and access: [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).
- Select **Create VPC** > **VPC and more**.

2. **VPC configuration**:
- **Name tag auto-generation**: `spring-boot-vpc`.
- **IPv4 CIDR block**: `10.0.0.0/16`.
![image](/images/tao_vpc/screenshot_1752388342.png)
- **Availability Zones (AZs)**: Select at least 2 AZs (e.g. `us-east-1a`, `us-east-1b`).

- **Subnets**:
- 2 public subnets (for EC2).

- 2 private subnets (for RDS).

- **NAT Gateways**: 1 per AZ (for private subnets to access the internet).
   ![image](/images/tao_vpc/screenshot_1752388383.png)
- **VPC endpoints**: None (or select **S3 Gateway** if needed).

- **DNS options**: Enable **Enable DNS hostnames** and **Enable DNS resolution**.
   ![image](/images/tao_vpc/screenshot_1752388459.png)
   - Nhấn **Create VPC**.
- Click **Create VPC**.
   ![image](/images/tao_vpc/screenshot_1752388666.png)
3. **Verify**:

- Check in **VPC Console** to make sure the VPC `spring-boot-vpc` has been created with 4 subnets (2 public, 2 private) and related resources (Internet Gateway, Route Tables, NAT Gateways).

### 1.2. Configure Public Subnets

1. **Access Subnets**:

- In **Amazon VPC Console**, select **Subnets**.

- Make sure the public subnets are named like: `spring-boot-vpc-public-us-east-1a`, `spring-boot-vpc-public-us-east-1b`.
   ![image](/images/cau_hinh_public_subnets/screenshot_1752388960.png)
2. **Enable Public IP**:

- Select each public subnet, click **Actions** > **Edit subnet settings**.

- Turn on **Enable auto-assign public IPv4 address**.

- Click **Save**.
   ![image](/images/cau_hinh_public_subnets/screenshot_1752388997.png)
3. **Verify**:

- Check that both public subnets have auto-assign Public IP enabled.
   ![image](/images/cau_hinh_public_subnets/screenshot_1752389021.png)
4. **Repeat for the second public subnet.**
   ![image](/images/cau_hinh_public_subnets/screenshot_1752389143.png)
   ![image](/images/cau_hinh_public_subnets/screenshot_1752389179.png)
