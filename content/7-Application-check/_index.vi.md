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
![image](/images/test/screenshot_1752401348.png)
2. **Kiểm tra log nếu có lỗi**:
   - Log container Spring Boot:
     ```bash
     sudo docker logs <container-id-backend>
     ```
     Thay `<container-id-backend>` bằng ID của container `backend` (lấy từ `docker ps`).
     ![image](/images/test/screenshot_1752400820.png)
   - Log Nginx:
     ```bash
     sudo tail -f /var/log/nginx/error.log
     ```

