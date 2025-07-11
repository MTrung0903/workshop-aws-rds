---
title : "Kiểm thử & Giám sát"
date: 2025-07-01
weight : 8
chapter : false
pre : " <b> 8. </b> "
---
### Kiểm tra Ứng dụng

1. Truy cập ứng dụng qua **ALB DNS name** (ví dụ: `https://ecommerce-app-alb-1234567890.us-east-1.elb.amazonaws.com`).
2. Kiểm tra endpoint:
    - `/health`: Đảm bảo trả về HTTP 200.
    - Các endpoint REST khác (ví dụ: `/api/users`) để xác minh kết nối RDS.
3. Kiểm tra logs:
    - **EC2**: SSH vào instance, chạy `docker logs ecommerce-spring-boot-app`.
    - **CloudWatch**: Mở **CloudWatch Console** > **Log groups** > `ecommerce-app-logs`, kiểm tra log stream theo instance ID.
4. Kiểm thử hiệu suất:
    - Sử dụng **JMeter** (https://jmeter.apache.org/) để mô phỏng 10,000 người dùng đồng thời, đảm bảo độ trễ <500ms [Google, "Speed Matters"].