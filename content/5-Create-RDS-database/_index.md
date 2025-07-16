---
title : "Create RDS database"
date: 2025-07-01
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

## 6. Create RDS Database Instance

1. **Access Amazon RDS Console**:

- Open: [https://console.aws.amazon.com/rds/](https://console.aws.amazon.com/rds/).

- Select **Create database**.
![image](/images/tao_rds/screenshot_1752395315.png)

2. **RDS configuration**:

- **Method**: Standard create.
- **Engine**: MySQL.
- **Version**: MySQL 8.0 (latest).
- **Template**: Free tier.
![image](/images/tao_rds/screenshot_1752395542.png)
![image](/images/tao_rds/screenshot_1752395567.png)
- **Multi-AZ**: DB instance (for high availability).
- **DB instance identifier**: `spring-boot-rds`.
- **Master username**: `admin`.
- **Master password**: Enter a secure password (eg: `SecurePass123!`) or select auto-generate.
![image](/images/tao_rds/screenshot_1752395643.png)
![image](/images/tao_rds/screenshot_1752395666.png)
- **Instance class**: `db.t3.micro` (Free Tier eligible).
- **Storage**: 20 GB, General Purpose SSD.
- **VPC**: Select `spring-boot-vpc`.
- **DB Subnet Group**: Select `rds-subnet-group`.
- **Security Group**: Select `rds-sg`.
![image](/images/tao_rds/screenshot_1752395689.png)
![image](/images/tao_rds/screenshot_1752395723.png)
- Click **Create database**.
![image](/images/tao_rds/screenshot_1752396030.png)
![image](/images/tao_rds/screenshot_1752396067.png)
3. **Save RDS information**:

- Note:

- **Endpoint**: Example `spring-boot-rds.cghg6wmuybac.us-east-1.rds.amazonaws.com`.

- **Port**: 3306.

- **Username**: `admin`.
- **Password**: The password you set.

4. **Test RDS connection from EC2**:

- In MobaXterm, run:
```bash
mysql -h spring-boot-rds.cghg6wmuybac.us-east-1.rds.amazonaws.com -u admin -p
```
![image](/images/tao_rds/screenshot_1752396540.png)
- Enter the RDS password.
- Create and check the database:
```sql
SHOW DATABASES;

```
![image](/images/tao_rds/screenshot_1752396596.png)
---