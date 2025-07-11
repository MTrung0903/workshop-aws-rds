---
title : "Tạo DB Subnet Group"
date: 2025-07-01
weight : 4
chapter : false
pre : " <b> 2.4 </b> "
---
## Tạo DB Subnet Group
#### Tạo DB Subnet Group
ℹ️ **Information**: DB Subnet Group là tập hợp các subnet trong VPC được chỉ định cho cơ sở dữ liệu RDS của bạn. DB Subnet Group cho phép Amazon RDS triển khai instance cơ sở dữ liệu trong nhiều Availability Zone để đảm bảo tính sẵn sàng cao và khả năng chịu lỗi.

##### Các bước tạo DB Subnet Group
1. Đăng nhập vào AWS Management Console.

2. Trong menu dịch vụ, tìm và chọn **Amazon RDS**.

3. Trong thanh điều hướng bên trái, chọn **Subnet groups**.

4. Nhấp vào nút **Create DB Subnet Group**.


5. Trong giao diện Create DB Subnet Group, nhập thông tin cơ bản:

- **Name**: Nhập tên mô tả cho DB Subnet Group
- **Description**: Thêm mô tả chi tiết về mục đích của DB Subnet Group
- **VPC**: Chọn VPC nơi bạn sẽ triển khai cơ sở dữ liệu RDS


6. Trong phần **Add subnets**:
- Chọn các **Availability Zones** (AZ) mà bạn muốn triển khai cơ sở dữ liệu
- Chọn các **Subnets** tương ứng trong mỗi AZ đã chọn
⚠️ Warning: Để triển khai Multi-AZ, bạn cần chọn ít nhất hai subnet trong các Availability Zone khác nhau. Điều này đảm bảo khả năng chịu lỗi cao cho cơ sở dữ liệu RDS của bạn.

7. Sau khi hoàn tất cấu hình, nhấp vào nút Create để tạo DB Subnet Group.


