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

3. **Xóa EC2 Instance**:
   - Truy cập **EC2 Console**, chọn `spring-boot-ec2` > **Actions** > **Instance State** > **Terminate instance**.

4. **Xóa RDS Instance**:
   - Truy cập **RDS Console**, chọn `spring-boot-rds` > **Actions** > **Delete**, nhập `delete me`.

5. **Xóa Security Groups**:
   - Truy cập **VPC Console**, chọn `ec2-sg` và `rds-sg` > **Actions** > **Delete security group**.

6. **Xóa IAM Role**:
   - Truy cập **IAM Console**, chọn `CustomRWECRRole` > **Delete**.

7. **Xóa VPC**:
   - Truy cập **VPC Console**, chọn `spring-boot-vpc` > **Actions** > **Delete VPC**, đảm bảo xóa hết tài nguyên phụ thuộc.

---