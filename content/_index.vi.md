---
title : "Thiết lập Tài Khoản AWS"
date: 2025-07-01
weight : 1 
chapter : false
---

# Giới thiệu & Mục tiêu

Workshop này hướng dẫn triển khai ứng dụng **Spring Boot** (đóng gói Docker) trên AWS, sử dụng các dịch vụ: EC2 Auto Scaling, RDS (MySQL), Application Load Balancer (ALB), CloudWatch, và triển khai blue-green.  
Bài toán thực tế: Quản lý danh tính người dùng cho sàn thương mại điện tử, yêu cầu zero-downtime, xử lý 10,000 người dùng đồng thời, tăng tỷ lệ chuyển đổi 10%.

**Mục tiêu:**
- Triển khai ứng dụng Spring Boot từ Docker image trên EC2 Auto Scaling.
- Kết nối với RDS MySQL (Multi-AZ).
- Sử dụng ALB để phân phối lưu lượng, hỗ trợ blue-green deployment.
- Giám sát hiệu suất qua CloudWatch.
- Đảm bảo bảo mật, khả năng mở rộng, sẵn sàng cao.