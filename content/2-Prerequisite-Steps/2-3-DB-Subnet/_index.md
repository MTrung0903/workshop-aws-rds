---
title : "Create DB Subnet Group"
date: 2025-07-01
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---
### 1.4. Create DB Subnet Group

1. **Go to Amazon RDS Console**: 
- Open: [https://console.aws.amazon.com/rds/](https://console.aws.amazon.com/rds/). 
- Select **Subnet groups** > **Create DB Subnet Group**.
![image](../../../static/images/tao_db_subnet_group/screenshot_1752390108.png)
2. **Configure DB Subnet Group**: 
- **Name**: `rds-subnet-group`. 
- **Description**: "DB Subnet Group for Spring Boot". 
- **VPC**: Select `spring-boot-vpc`. 
![image](../../../static/images/tao_db_subnet_group/screenshot_1752390165.png)
- **Add subnets**: Select 2 private subnets (eg: `spring-boot-vpc-private-us-east-1a`, `spring-boot-vpc-private-us-east-1b`).
![image](../../../static/images/tao_db_subnet_group/screenshot_1752390313.png)
- Click **Create**.
![image](../../../static/images/tao_db_subnet_group/screenshot_1752390329.png)
3. **Verify**:

- Check in **RDS Console** to make sure `rds-subnet-group` has been created with 2 private subnets.