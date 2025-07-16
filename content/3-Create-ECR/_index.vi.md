---
title : "Tạo ECR Repository"
date: 2025-07-01
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

### 2.1. Tạo ECR Repository

1. **Truy cập Amazon ECR Console**:
   - Mở: [https://console.aws.amazon.com/ecr/](https://console.aws.amazon.com/ecr/).
   - Chọn **Create repository**.
![image](/images/push_image/screenshot_1752393032.png)
2. **Cấu hình Repository**:
   - **Repository name**: `spring-boot-app`.
   - **Tag immutability**: Chọn **Mutable**.
   ![image](/images/push_image/screenshot_1752393109.png)
   - **Scan on push**: Bật để quét lỗ hổng bảo mật.
   - Nhấn **Create repository**.
![image](/images/push_image/screenshot_1752393166.png)
3. **Lưu URI**:
![image](/images/push_image/screenshot_1752393208.png)
   - Ghi lại URI của repository, ví dụ: `<account-id>.dkr.ecr.us-east-1.amazonaws.com/spring-boot-app`.

### 2.2. Đẩy Docker image lên ECR

1. **Đảm bảo Docker image cục bộ**:
   - Xác minh image Spring Boot cục bộ (ví dụ: `trungho93/identity-service:0.9.0`):
     ```bash
     docker images
     ```

2. **Đăng nhập vào ECR**:
   - Chạy:
     ```bash
     aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.us-east-1.amazonaws.com
     ```
   - Thay `<account-id>` bằng ID tài khoản AWS của bạn (ví dụ: `238702553701`).
   - Kết quả: `Login Succeeded`.

3. **Tag và đẩy image**:
   - Tag image:
     ```bash
     docker tag trungho93/identity-service:0.9.0 <account-id>.dkr.ecr.us-east-1.amazonaws.com/spring-boot-app:latest
     ```
     ![image](/images/push_image/screenshot_1752393376.png)
![image](/images/push_image/screenshot_1752393426.png)

   - Đẩy image:
     ```bash
     docker push <account-id>.dkr.ecr.us-east-1.amazonaws.com/spring-boot-app:latest
     ```
![image](/images/push_image/screenshot_1752393822.png)
![image](/images/push_image/screenshot_1752393914.png)
4. **Xác minh**:
   - Truy cập **ECR Console**, chọn repository `spring-boot-app`, kiểm tra image .
