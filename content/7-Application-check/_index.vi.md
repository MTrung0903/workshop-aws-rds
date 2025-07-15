---
title : "Kiểm tra ứng dụng"
date: 2025-07-01
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

## 8. Kiểm tra ứng dụng

1. **Truy cập ứng dụng**:
   - Mở trình duyệt hoặc Postman, truy cập:
     ```bash
     http://<EC2-Public-IP>/api/<endpoint>
     ```
     Ví dụ: Nếu Spring Boot có endpoint `/api/users`, truy cập `http://<EC2-Public-IP>/api/users`.

2. **Kiểm tra log nếu có lỗi**:
   - Log container Spring Boot:
     ```bash
     sudo docker logs <container-id-backend>
     ```
     Thay `<container-id-backend>` bằng ID của container `backend` (lấy từ `docker ps`).
   - Log Nginx:
     ```bash
     sudo tail -f /var/log/nginx/error.log
     ```

3. **Kiểm tra kết nối RDS**:
   - Trong terminal EC2:
     ```bash
     mysql -h <RDS Endpoint> -u admin -p
     ```
   - Nhập mật khẩu RDS.
   - Kiểm tra dữ liệu:
     ```sql
     USE first_cloud_users;
     SHOW TABLES;
     SELECT * FROM users;
     ```

4. **Xử lý sự cố**:
   - **Lỗi kết nối RDS**: Kiểm tra Security Group `rds-sg` có cho phép `ec2-sg` trên cổng 3306.
   - **Lỗi API**: Kiểm tra log container và đảm bảo `SPRING_DATASOURCE_URL` đúng.
   - **Lỗi Nginx**: Kiểm tra `nginx.conf` và log `/var/log/nginx/error.log`.

---