---
title : "Tạo Application Load Balancer (ALB)"
date: 2025-07-01
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

1. Mở **EC2 Console** > **Load Balancers** > **Create Load Balancer** > **Application Load Balancer**.

2. Cấu hình:
    - **Name**: `ecommerce-app-alb`.
    - **Scheme**: Internet-facing.
    - **IP address type**: IPv4.
    - **Listeners**:
        - HTTPS (443): Sử dụng SSL certificate từ AWS Certificate Manager (ACM). Nếu chưa có, tạo chứng chỉ tại https://console.aws.amazon.com/acm/ [Module 24].
        - HTTP (80): Redirect to HTTPS.
    - **VPC**: `ecommerce-vpc`.
    - **Subnets**: Chọn 2 public subnets (`ecommerce-vpc-public-us-east-1a`, `ecommerce-vpc-public-us-east-1b`).
    - **Security Group**: Chọn `ecommerce-alb-sg`.


3. **Target Group**:
    - **Name**: `ecommerce-app-tg`.
    - **Target type**: Instance.
    - **Protocol**: HTTP.
    - **Port**: 8080.
    - **Health check**: Path `/health`, HTTP 200, interval 30s, timeout 5s, healthy threshold 5, unhealthy threshold 2.


4. Chọn **Create**.

5. Ghi lại **DNS name** của ALB (ví dụ: `ecommerce-app-alb-1234567890.us-east-1.elb.amazonaws.com`).