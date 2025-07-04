---
title : "Dọn dẹp tài nguyên"
date: 2025-07-01
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

### Dọn dẹp tài nguyên AWS
ℹ️ **Information**: Sau khi hoàn thành bài lab, việc dọn dẹp tài nguyên AWS là bước quan trọng để tránh phát sinh chi phí không mong muốn. Hãy làm theo các bước dưới đây để xóa tất cả tài nguyên đã tạo.

1. ##### Xóa RDS Database và Snapshots
###### Xóa DB Instance:
- 
    - Truy cập RDS Management Console
    - Trong thanh điều hướng bên trái, chọn Databases
    - Chọn tất cả DB Instance liên quan đến bài lab
    - Nhấp vào Actions, sau đó chọn Delete
    - Bỏ chọn Create final snapshot? và chọn ô xác nhận I acknowledge that upon instance deletion, automated backups, including system snapshots and point-in-time recovery, will no longer be available
    - Nhập delete me vào ô xác nhận
    - Nhấp vào Delete
⚠️ Warning: Việc xóa DB Instance là không thể hoàn tác. Đảm bảo bạn đã sao lưu dữ liệu quan trọng trước khi thực hiện bước này.

###### Xóa DB Snapshots:
- 
    - Truy cập RDS Management Console
    - Trong thanh điều hướng bên trái, chọn Snapshots
    - Chọn tất cả snapshot liên quan đến bài lab
    - Nhấp vào Actions
    - Chọn Delete snapshot
    - Nhấp vào Delete để xác nhận
###### Xóa DB Subnet Group:
- 
    - Mở Amazon RDS Console
    - Trong thanh điều hướng bên trái, chọn Subnet groups
    - Chọn DB subnet group liên quan đến bài lab
    - Nhấp vào Delete, sau đó chọn Delete trong cửa sổ xác nhận
2. ##### Terminate EC2 Instance
    1. Truy cập EC2 Management Console

    2. Trong thanh điều hướng bên trái, chọn Instances

    3. Chọn tất cả EC2 Instance liên quan đến bài lab

    4. Nhấp vào Actions

    5. Chọn Instance state, sau đó chọn Terminate instance

    6. Nhấp vào Terminate để xác nhận

💡 Pro Tip: Trước khi terminate instance, hãy đảm bảo bạn đã sao lưu tất cả dữ liệu quan trọng từ instance, vì dữ liệu trên instance sẽ bị xóa vĩnh viễn.

3. ##### Giải phóng Elastic IP Addresses
    1. Mở Amazon EC2 Console

    2. Chọn EC2 Dashboard, sau đó chọn Elastic IPs

    3. Chọn Elastic IP address liên quan đến bài lab

    4. Từ menu Actions, chọn Release Elastic IP addresses

    5. Trên trang xác nhận, nhấp vào Release

🔒 Security Note: Giải phóng Elastic IP sẽ ngăn chặn chi phí phát sinh cho các địa chỉ IP không được sử dụng. AWS tính phí cho Elastic IP không được liên kết với instance đang chạy.

4. ##### Xóa VPC và các tài nguyên liên quan
###### Xóa Security Groups:
- 
    - Mở Amazon VPC Console
    - Chọn Security Groups từ thanh điều hướng bên trái
    - Chọn security group liên quan đến bài lab
    - Nhấp vào Actions, chọn Delete security groups
    - Nhấp vào Delete để xác nhận
###### Xóa NAT Gateway:
- 
    - Mở Amazon VPC Console
    - Chọn NAT Gateways từ thanh điều hướng bên trái
    - Chọn NAT Gateway liên quan đến bài lab
    - Nhấp vào Actions, chọn Delete NAT gateway
    - Xác nhận xóa và nhấp vào Delete
ℹ️ Information: Việc xóa NAT Gateway không tự động giải phóng Elastic IP được liên kết với nó. Hãy đảm bảo bạn đã giải phóng Elastic IP ở bước trước.

###### Xóa VPC:
- 
    - Mở Amazon VPC Console
    - Chọn Your VPCs từ thanh điều hướng bên trái
    - Chọn VPC bạn muốn xóa
    - Từ menu Actions, chọn Delete VPC
    - Trên trang xác nhận, nhập delete, sau đó nhấp vào Delete
💡 Pro Tip: Khi xóa VPC, AWS sẽ tự động xóa các tài nguyên liên quan như subnets, route tables và internet gateways. Tuy nhiên, một số tài nguyên như security groups, NAT gateways và DB subnet groups cần được xóa thủ công trước.