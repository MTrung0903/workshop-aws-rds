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
![image](/images/clean/screenshot_1752401672.png)
3. **Delete the EC2 Instance**:

- Go to **EC2 Console**, select `spring-boot-ec2` > **Actions** > **Instance State** > **Terminate instance**.
![image](/images/clean/screenshot_1752401691.png)
4. **Delete RDS Instance**:

- Go to **RDS Console**, select `spring-boot-rds` > **Actions** > **Delete**, enter `delete me`.
![image](/images/clean/screenshot_1752401728.png)
![image](/images/clean/screenshot_1752401743.png)
5. **Delete Security Groups**:

- Go to **VPC Console**, select `ec2-sg` and `rds-sg` > **Actions** > **Delete security group**.
![image](/images/clean/screenshot_1752401874.png)
6. **Delete IAM Role**:

- Go to **IAM Console**, select `CustomRWECRRole` > **Delete**.
![image](/images/clean/screenshot_1752401928.png)
7. **Delete VPC**:
- Go to **VPC Console**, select `spring-boot-vpc` > **Actions** > **Delete VPC**, make sure to delete all dependent resources.
![image](/images/clean/screenshot_1752402300.png)
![image](/images/clean/screenshot_1752402343.png)
---