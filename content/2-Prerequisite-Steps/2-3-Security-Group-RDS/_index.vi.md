---
title : "Tạo RDS Security Group"
date: 2025-07-01
weight : 1
chapter : false
pre : " <b> 2.3 </b> "
---
## Tạo RDS Security Group
#### Tạo Security Group cho Amazon RDS
ℹ️ **Information**: Security Group cho Amazon RDS hoạt động như tường lửa ảo để kiểm soát lưu lượng mạng đến và đi từ cơ sở dữ liệu của bạn. Việc cấu hình đúng Security Group là bước quan trọng để bảo vệ dữ liệu của bạn trong AWS.

##### Các bước tạo Security Group cho RDS
1. Đăng nhập vào AWS Management Console.

2. Trong menu dịch vụ, chọn **VPC** trong phần **Networking & Content Delivery**.

3. Trong thanh điều hướng bên trái, dưới mục **Security**, chọn **Security Groups**.

4. Nhấp vào nút **Create security group** để bắt đầu quá trình tạo.



5. Trong phần Basic details, nhập thông tin cơ bản:

- Security group name: Nhập tên mô tả cho Security Group
- Description: Thêm mô tả chi tiết về mục đích của Security Group
- VPC: Chọn VPC nơi bạn sẽ triển khai cơ sở dữ liệu RDS
6. Trong phần Inbound rules, thêm quy tắc để cho phép lưu lượng truy cập đến cơ sở dữ liệu:
    - Chọn MySQL/Aurora từ danh sách loại (Type)
    - Cổng 3306 sẽ được tự động điền
    - Đối với Source, chọn Security Group của EC2 instance mà bạn đã tạo trước đó
🔒 **Security Note**: Chỉ cho phép kết nối từ các nguồn cụ thể thay vì mở cổng cơ sở dữ liệu cho tất cả địa chỉ IP (0.0.0.0/0). Điều này tuân theo nguyên tắc đặc quyền tối thiểu và tăng cường bảo mật.


7. (Tùy chọn) Cấu hình Outbound rules nếu bạn cần giới hạn lưu lượng đi ra. Mặc định, tất cả lưu lượng đi ra đều được cho phép.

8. Sau khi hoàn tất cấu hình, nhấp vào nút **Create security group**.


Security Group mới đã được tạo và sẵn sàng để gán cho DB instance RDS của bạn.

⚠️ **Warning**: Không nên sử dụng cùng một Security Group cho cả EC2 và RDS. Việc tách biệt Security Group giúp quản lý quyền truy cập chính xác hơn và tuân thủ các nguyên tắc bảo mật tốt nhất.

