---
title : "Clean up resources"
date: 2025-07-01
weight : 8
chapter : false
pre : " <b> 8. </b> "
---

## 9. Clean up resources

To avoid incurring costs:

1. **Stop and delete the container**:

- In the EC2 terminal:
```bash
cd spring-boot-app
sudo docker compose -f docker-compose.yml down
```

2. **Delete the ECR Repository**:

- Go to **ECR Console**, select `spring-boot-app` > **Delete**.

3. **Delete the EC2 Instance**:

- Go to **EC2 Console**, select `spring-boot-ec2` > **Actions** > **Instance State** > **Terminate instance**.

4. **Delete RDS Instance**:

- Go to **RDS Console**, select `spring-boot-rds` > **Actions** > **Delete**, enter `delete me`.

5. **Delete Security Groups**:

- Go to **VPC Console**, select `ec2-sg` and `rds-sg` > **Actions** > **Delete security group**.

6. **Delete IAM Role**:

- Go to **IAM Console**, select `CustomRWECRRole` > **Delete**.

7. **Delete VPC**:
- Go to **VPC Console**, select `spring-boot-vpc` > **Actions** > **Delete VPC**, make sure to delete all dependent resources.

---