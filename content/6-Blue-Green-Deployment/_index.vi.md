---
title : "Triển khai Blue-Green Deployment"
date: 2025-07-01
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

Sử dụng ALB và Auto Scaling Group để triển khai blue-green, đảm bảo zero-downtime.

1. Tạo target group thứ hai:
    - Mở **EC2 Console** > **Target Groups** > **Create target group**.
    - **Name**: `ecommerce-app-tg-green`.
    - Cấu hình tương tự `ecommerce-app-tg` (HTTP, port 8080, health check `/health`).
2. Cập nhật Launch Template:
    - Tạo phiên bản mới của `ecommerce-spring-boot-template` với Docker image mới (ví dụ: `trungho93/identity-service:0.9.1`).
3. Tạo Auto Scaling Group thứ hai:
    - **Name**: `ecommerce-spring-boot-asg-green`.
    - Sử dụng Launch Template mới, gắn với `ecommerce-app-tg-green`.
    - Cấu hình tương tự bước 3 (2-4 instance, CPU 70%).
4. Chuyển lưu lượng sang target group mới:
    
    ```bash
    aws elbv2 modify-listener --listener-arn <listener-arn> --default-actions Type=forward,TargetGroupArn=<green-tg-arn>
    
    ```
    
    > Lưu ý: Thay <listener-arn> và <green-tg-arn> bằng ARN thực tế (tìm trong EC2 Console > Load Balancers > Listeners và Target Groups).
    > 
5. Sau khi kiểm tra health checks (xem trong **Target Groups** > `ecommerce-app-tg-green`), terminate Auto Scaling Group cũ: