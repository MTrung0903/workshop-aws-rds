---
title : "Tạo VPC"
date: 2025-07-01
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

#### Tạo VPC và các tài nguyên mạng
**Information** : Amazon Virtual Private Cloud (VPC) cho phép bạn khởi chạy tài nguyên AWS trong một mạng ảo được định nghĩa. Môi trường này cung cấp kiểm soát đầy đủ về cấu hình mạng, bao gồm dải địa chỉ IP, subnet, bảng định tuyến và gateway.

1. Tạo VPC sử dụng AWS Management Console
Mở giao diện điều khiển Amazon VPC tại https://console.aws.amazon.com/vpc/.


2. Trên bảng điều khiển VPC, chọn Create VPC.

3. Trong phần Resources to create, chọn VPC and more để tạo VPC cùng với các tài nguyên liên quan.



4. Cấu hình các tùy chọn cơ bản:

- Giữ nguyên tùy chọn Name tag auto-generation để tự động tạo nhãn cho các tài nguyên, hoặc bỏ chọn để tự đặt tên.
- Nhập dải địa chỉ IPv4 CIDR cho VPC (bắt buộc).
- (Tùy chọn) Để hỗ trợ IPv6, chọn IPv6 CIDR block, Amazon-provided IPv6 CIDR block.
- Chọn tùy chọn Tenancy phù hợp với nhu cầu của bạn.
5. Cấu hình Availability Zones (AZs):

- Đối với Number of Availability Zones, chọn ít nhất hai AZs cho môi trường sản xuất.
- Để chỉ định AZs cụ thể, mở rộng Customize AZs.


6. Cấu hình subnet:

- Chọn số lượng subnet công khai và riêng tư cần thiết.
- Để tùy chỉnh dải CIDR cho các subnet, mở rộng Customize subnets CIDR blocks.
7. Cấu hình kết nối internet:

- Đối với NAT gateways, chọn số lượng AZs cần triển khai NAT gateway.
- Đối với kết nối IPv6, chọn Egress only internet gateway nếu cần thiết.


8. (Tùy chọn) Để truy cập Amazon S3 trực tiếp từ VPC, chọn VPC endpoints, S3 Gateway.

9. Đối với tùy chọn DNS, mặc định cả hai tùy chọn về giải quyết tên miền đều được kích hoạt. Điều chỉnh nếu cần.

10. (Tùy chọn) Thêm nhãn cho VPC bằng cách mở rộng Additional tags.

11. Xem trước cấu trúc VPC trong bảng Preview:

- Đường liền nét thể hiện mối quan hệ giữa các tài nguyên.
- Đường đứt đoạn thể hiện luồng lưu lượng mạng.
- Khi hoàn tất cấu hình, chọn Create VPC.



#### Cấu hình địa chỉ IPv4 công khai cho subnet
ℹ️ **Information**: Mặc định, subnet không mặc định có thuộc tính tự động gán địa chỉ IPv4 công khai được đặt thành “false”, trong khi subnet mặc định có thuộc tính này được đặt thành “true”. Subnet không mặc định được tạo qua trình tạo EC2 instance sẽ có thuộc tính này được đặt thành “true”.

**Để thay đổi cài đặt địa chỉ IPv4 công khai của subnet:**

1. Mở giao diện Amazon VPC tại https://console.aws.amazon.com/vpc/.

2. Trong bảng điều hướng, chọn **Subnets**.



3. Chọn subnet cần cấu hình, sau đó chọn Actions, Edit subnet settings.


4. Đánh dấu hoặc bỏ đánh dấu tùy chọn Enable auto-assign public IPv4 address theo nhu cầu, sau đó chọn Save.

