---
title : "Create Security Group"
date: 2025-07-01
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

### 1.3. Create Security Groups

#### Security Group for EC2

1. **Access Amazon EC2 Console**:

- Open: [https://console.aws.amazon.com/ec2/](https://console.aws.amazon.com/ec2/).

- Select **Security Groups** > **Create Security Group**.
   ![image](/images/tao_sg_ec2/screenshot_1752389310.png)
2. **Configure Security Group**:

- **Name**: `ec2-sg`.

- **Description**: "Security Group for EC2 running Spring Boot and Nginx".

- **VPC**: Select `spring-boot-vpc`.
      ![image](/images/tao_sg_ec2/screenshot_1752389486.png)
- **Inbound Rules**:
- **HTTP (80)**: Source `0.0.0.0/0` (allow all to access via Nginx).
- **HTTPS (443)**: Source `0.0.0.0/0` (for production environment).
- **Custom TCP (8080)**: Source `0.0.0.0/0` (for testing only, limited from Nginx in production).
- **SSH (22)**: Source `<your-ip>/32` (replace `<your-ip>` with your IP address, e.g. `203.0.113.1/32`).
![image](/images/tao_sg_ec2/screenshot_1752389534.png)
- **Outbound Rules**: Default (allow all).
- Click **Create security group**.
    ![image](/images/tao_sg_ec2/screenshot_1752389562.png)
    ![image](/images/tao_sg_ec2/screenshot_1752389644.png)
3. **Verify**:

- Check the Security Group `ec2-sg` in **EC2 Console** to make sure the rules are applied correctly.


#### Security Group for RDS

1. **Go to Amazon VPC Console**:
- Select **Security Groups** > **Create security group**.
2. **Configure Security Group**:
- **Name**: `rds-sg`.
- **Description**: "Security Group for RDS MySQL".

- **VPC**: Select `spring-boot-vpc`.

- **Inbound Rule**:
- **Type**: MySQL/Aurora.

- **Port**: 3306.

- **Source**: Select Security Group `ec2-sg` (allow EC2 to access RDS).
![image](/images/tao_sg_rds/screenshot_1752389783.png)

- **Outbound Rules**: Default (allow all).

- Click **Create security group**.
![image](/images/tao_sg_rds/screenshot_1752389842.png)
3. **Verification**:
- Check Security Group `rds-sg` to ensure only connections from `ec2-sg` are allowed on port 3306.