---
title : "Dọn dẹp tài nguyên"
date: 2025-07-01
weight : 8
chapter : false
pre : " <b> 8. </b> "
---

## 9. Dọn dẹp tài nguyên

Để tránh phát sinh chi phí:

1. **Dừng và xóa container**:
   - Trong terminal EC2:
     ```bash
     cd spring-boot-app
     sudo docker compose -f docker-compose.yml down
     ```

2. **Xóa ECR Repository**:
   - Truy cập **ECR Console**, chọn `spring-boot-app` > **Delete**.
![image](/images/clean/screenshot_1752401672.png)
3. **Xóa EC2 Instance**:
   - Truy cập **EC2 Console**, chọn `spring-boot-ec2` > **Actions** > **Instance State** > **Terminate instance**.
![image](/images/clean/screenshot_1752401691.png)
4. **Xóa RDS Instance**:
   - Truy cập **RDS Console**, chọn `spring-boot-rds` > **Actions** > **Delete**, nhập `delete me`.
![image](/images/clean/screenshot_1752401728.png)
![image](/images/clean/screenshot_1752401743.png)
5. **Xóa Security Groups**:
   - Truy cập **VPC Console**, chọn `ec2-sg` và `rds-sg` > **Actions** > **Delete security group**.
![image](/images/clean/screenshot_1752401874.png)
6. **Xóa IAM Role**:
   - Truy cập **IAM Console**, chọn `CustomRWECRRole` > **Delete**.
![image](/images/clean/screenshot_1752401928.png)
7. **Xóa VPC**:
   - Truy cập **VPC Console**, chọn `spring-boot-vpc` > **Actions** > **Delete VPC**, đảm bảo xóa hết tài nguyên phụ thuộc.
![image](/images/clean/screenshot_1752402300.png)
![image](/images/clean/screenshot_1752402343.png)
---