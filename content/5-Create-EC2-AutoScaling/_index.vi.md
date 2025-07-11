---
title : "Tạo EC2 Auto Scaling Group"
date: 2025-07-01
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

1. Mở **EC2 Console** > **Launch Templates** > **Create launch template**.
2. Cấu hình:
    - **Name**: `ecommerce-spring-boot-template`.
    - **AMI**: Amazon Linux 2023 AMI (chọn từ danh sách AMI tại https://console.aws.amazon.com/ec2/).
    - **Instance type**: `t3.micro` (2 vCPU, 1 GB RAM) [AWS EC2 Pricing].
    - **Key pair**: Chọn cặp khóa SSH (.pem) đã tạo trước.
    - **Security Group**: Chọn `ecommerce-ec2-sg`.
    - **User Data**:
        
        ```bash
        #!/bin/bash
        dnf update -y
        dnf install -y docker
        systemctl start docker
        systemctl enable docker
        usermod -aG docker ec2-user
        docker pull trungho93/identity-service:0.9.0
        docker run -d -p 8080:8080 \
          -e DBMS_CONNECTION=jdbc:mysql://<RDS Endpoint>:3306/first_cloud_users \
          -e DBMS_USERNAME=admin \
          -e DBMS_PASSWORD=<RDS Password> \
          --name ecommerce-spring-boot-app trungho93/identity-service:0.9.0
        
        ```
        
        > Lưu ý: Thay <RDS Endpoint> và <RDS Password> bằng giá trị thực tế từ bước 4.
        > 
3. Chọn **Create launch template**.
4. Mở **Auto Scaling Groups** > **Create Auto Scaling group**.
5. Cấu hình:
    - **Name**: `ecommerce-spring-boot-asg`.
    - **Launch template**: `ecommerce-spring-boot-template`.
    - **VPC**: `ecommerce-vpc`.
    - **Subnets**: Chọn 2 public subnets (`ecommerce-vpc-public-us-east-1a`, `ecommerce-vpc-public-us-east-1b`).
    - **Desired capacity**: 2.
    - **Minimum capacity**: 2.
    - **Maximum capacity**: 4.
    - **Scaling policies**: Target tracking, CPU utilization 70% [AWS Case Studies].
    - **Target group**: Chọn `ecommerce-app-tg`.
6. Chọn **Create Auto Scaling group**.