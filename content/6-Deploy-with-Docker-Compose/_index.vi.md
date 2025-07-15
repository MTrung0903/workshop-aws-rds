---
title : "Triển khai ứng dụng Spring Boot với Docker Compose"
date: 2025-07-01
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

## 7. Triển khai ứng dụng Spring Boot với Docker Compose

### 7.1. Đăng nhập vào Amazon ECR từ EC2

1. Trong terminal MobaXterm, chạy:
   ```bash
   aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.us-east-1.amazonaws.com
   ```
   - Thay `<account-id>` bằng ID tài khoản AWS.
   - Kết quả: `Login Succeeded`.

### 7.2. Tạo file Docker Compose

1. **Tạo thư mục**:
   - Trong terminal EC2:
     ```bash
     mkdir spring-boot-app && cd spring-boot-app
     ```

2. **Tạo file `docker-compose.yml`**:
   - Chạy:
     ```bash
     nano docker-compose.yml
     ```
   - Dán nội dung sau, thay các giá trị `<account-id>`, `<region>`, `<RDS Endpoint>`, và `<RDS Password>`:
     ```yaml
     version: '3.8'
     services:
       nginx:
         image: nginx:latest
         ports:
           - "80:80"
         volumes:
           - ./nginx.conf:/etc/nginx/conf.d/app.conf
         depends_on:
           - backend
         networks:
           - app-network
       backend:
         image: <account-id>.dkr.ecr.<region>.amazonaws.com/spring-boot-app:latest
         ports:
           - "8080:8080"
         environment:
           - SPRING_DATASOURCE_URL=jdbc:mysql://<RDS Endpoint>:3306/first_cloud_users?useSSL=false&serverTimezone=UTC
           - SPRING_DATASOURCE_USERNAME=admin
           - SPRING_DATASOURCE_PASSWORD=<RDS Password>
           - SPRING_JPA_HIBERNATE_DDL_AUTO=update
         networks:
           - app-network
     networks:
       app-network:
         driver: bridge
     ```
   - Lưu file: Nhấn `Ctrl+O`, Enter, `Ctrl+X`.

### 7.3. Tạo file cấu hình Nginx

1. **Tạo file `nginx.conf`**:
   - Chạy:
     ```bash
     nano nginx.conf
     ```
   - Dán nội dung:
     ```nginx
     server {
         listen 80;
         server_name _;
         location / {
             proxy_pass http://backend:8080;
             proxy_set_header Host $host;
             proxy_set_header X-Real-IP $remote_addr;
             proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
             proxy_set_header X-Forwarded-Proto $scheme;
         }
     }
     ```
   - Lưu file: Nhấn `Ctrl+O`, Enter, `Ctrl+X`.

### 7.4. Chạy Docker Compose

1. **Kiểm tra file cấu hình**:
   - Đảm bảo `docker-compose.yml` và `nginx.conf` đã được tạo trong thư mục `spring-boot-app`.

2. **Chạy container**:
   - Chạy:
     ```bash
     sudo docker compose -f docker-compose.yml up -d
     ```

3. **Xác minh**:
   - Kiểm tra container:
     ```bash
     docker ps
     ```
   - Bạn sẽ thấy 2 container: `nginx` và `backend`.

---