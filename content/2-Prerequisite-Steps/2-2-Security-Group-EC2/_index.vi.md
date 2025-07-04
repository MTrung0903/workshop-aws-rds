---
title : "Tạo EC2 Security Group"
date: 2025-07-01
weight : 1
chapter : false
pre : " <b> 2.2 </b> "
---

#### Tạo Security Group cho Amazon EC2
**Information**: Security Group hoạt động như tường lửa ảo để kiểm soát lưu lượng truy cập vào và ra khỏi các tài nguyên AWS của bạn. Mỗi Security Group chứa một tập hợp các quy tắc cho phép lưu lượng mạng đến các tài nguyên được liên kết.

##### Các bước tạo Security Group cho EC2

1. Đăng nhập vào AWS Management Console.

2. Trong menu dịch vụ, chọn **EC2 trong phần **Compute**.

3. Trong thanh điều hướng bên trái, dưới mục **Network & Security**, chọn **Security Groups**.

4. Nhấp vào nút **Create Security Group** để bắt đầu quá trình tạo.

5. Trong phần Basic details, nhập thông tin cơ bản:
- Security group name: Nhập tên mô tả cho Security Group
- Description: Thêm mô tả chi tiết về mục đích của Security Group
- VPC: Chọn VPC nơi bạn muốn áp dụng Security Group này


6. Trong phần Inbound rules, thêm các quy tắc sau để cho phép lưu lượng truy cập đến:
- HTTP (80): Cho phép lưu lượng web HTTP tiêu chuẩn
- HTTPS (443): Cho phép lưu lượng web bảo mật HTTPS
- Custom TCP (8080): Cho phép lưu lượng đến cổng ứng dụng 8080
- SSH (22): Cho phép kết nối SSH để quản trị máy chủ
🔒 **Security Note:** Đối với môi trường sản xuất, nên giới hạn quyền truy cập SSH chỉ từ các địa chỉ IP đáng tin cậy thay vì mở cho tất cả (0.0.0.0/0).

7. (Tùy chọn) Cấu hình **Outbound rules** nếu bạn cần giới hạn lưu lượng đi ra. Mặc định, tất cả lưu lượng đi ra đều được cho phép.

8. (Tùy chọn) Thêm thẻ để dễ dàng quản lý và phân loại Security Group của bạn.

9. Sau khi hoàn tất cấu hình, nhấp vào nút **Create security group**.

Security Group mới đã được tạo và sẵn sàng để gán cho các instance EC2 của bạn.
Security Group Created

