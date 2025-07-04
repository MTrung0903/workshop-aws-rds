---
title : "Triển khai ứng dụng Spring Boot từ Docker Hub"
date: 2025-07-01
weight : 6
chapter : false
pre : " <b> 6. </b> "
---
### Triển khai ứng dụng Spring Boot từ Docker Hub

1. Kéo Docker image từ Docker Hub:
    docker pull trungho93/identity-service:0.9.0
- Nếu image là private, đăng nhập vào Docker Hub:
    docker login
    - Nhập tên người dùng và mật khẩu Docker Hub.

2. Cấu hình kết nối RDS:
- Truyền các biến môi trường tùy chỉnh (DBMS_*) để kết nối với RDS:
docker run -d -p 8080:8080 \
  -e DBMS_CONNECTION=jdbc:mysql://database-workshop.ctsk2qmig8wy.ap-southeast-2.rds.amazonaws.com:3306/database-workshop \
  -e DBMS_USERNAME=admin \
  -e DBMS_PASSWORD=trung09032003 \
  --name spring-boot-app trungho93/identity-service:0.9.0

3. Chạy container:
docker run -d -p 5000:5000 \
  -e DBMS_CONNECTION=jdbc:mysql://database-workshop.ctsk2qmig8wy.ap-southeast-2.rds.amazonaws.com:3306/database-workshop \
  -e DBMS_USERNAME=admin \
  -e DBMS_PASSWORD=trung09032003 \
  --name spring-boot-app trungho93/identity-service:0.9.0

4. Kiểm tra ứng dụng:
    http://3.25.221.88:8080/identity/auth/token

Kiểm tra log nếu có lỗi:
docker logs spring-boot-app