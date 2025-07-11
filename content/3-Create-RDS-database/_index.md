---
title : "Create RDS database"
date: 2025-07-01
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

### Create RDS Database Instance
1. Open Amazon RDS Console > Create database.
2. Select Standard create > Engine type: MySQL.
3. Version: Select the latest version (for example, MySQL 8.0.41).
4. Templates: Select Production to enable Multi-AZ and deletion protection.
5. Settings:
- DB instance identifier: database-workshop.
- Master username: admin.
- Master password: trung09032003 (or select Auto generate a password).
6. DB instance class: Select db.t3.micro.
7. Storage: Keep default or customize (for example, 20 GB).
8. Connectivity:

- VPC: Select workshop-aws-rds-vpc.

- DB Subnet Group: Select rds-subnet-group.

- VPC security group: Select rds-sg.

9. Select Create database.

10. If automatic password is selected, view credentials via View credential details.

11. Wait for the instance to move to Available state.

12. Note down Endpoint: database-workshop.ctsk2qmig8wy.ap-southeast-2.rds.amazonaws.com, Port: 3306, Username: admin, and Password: trung09032003.