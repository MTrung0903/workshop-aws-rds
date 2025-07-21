---
title : "Các bước chuẩn bị"
date: 2025-07-01
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

## Các bước chuẩn bị hạ tầng AWS

**Thông tin:**  
Trước khi triển khai Amazon RDS và ứng dụng, bạn cần thiết lập môi trường mạng và bảo mật phù hợp. Các bước dưới đây sẽ giúp bạn chuẩn bị cơ sở hạ tầng cần thiết, đảm bảo an toàn và sẵn sàng cho các dịch vụ AWS.

---

### Checklist nhanh

- [ ] Đã có tài khoản AWS với quyền quản trị
- [ ] Đã xác định vùng (Region) triển khai (ví dụ: us-east-1)
- [ ] Đã chuẩn bị tên các tài nguyên (VPC, subnet, security group, v.v.) theo chuẩn đặt tên

---

### 1. Tạo VPC (Virtual Private Cloud)

**Mục đích:**  
Tạo một môi trường mạng ảo riêng biệt để cô lập tài nguyên AWS, tăng bảo mật và kiểm soát lưu lượng.

- Thực hiện theo hướng dẫn chi tiết tại [Tạo VPC](/2-Prerequisite-Steps/2-1-VPC/)
- **Lưu ý:** Chọn dải IP phù hợp, bật DNS hostnames và DNS resolution.

---

### 2. Tạo Subnet

**Mục đích:**  
Chia nhỏ VPC thành các subnet để triển khai đa vùng sẵn sàng (Multi-AZ), tách biệt subnet public (cho EC2) và private (cho RDS).

- Thực hiện theo hướng dẫn tại [Tạo VPC](/2-Prerequisite-Steps/2-1-VPC/)
- **Lưu ý:**  
  - Tạo ít nhất 2 public subnet (cho EC2) và 2 private subnet (cho RDS).
  - Bật auto-assign public IP cho các public subnet.

---

### 3. Tạo Security Group cho EC2

**Mục đích:**  
Kiểm soát lưu lượng mạng đến/đi từ máy chủ ứng dụng (EC2), đảm bảo chỉ cho phép các kết nối cần thiết.

- Thực hiện theo hướng dẫn tại [Tạo Security Group](/2-Prerequisite-Steps/2-2-Security-Group/)
- **Lưu ý:**  
  - Chỉ mở port 22 (SSH) cho IP của bạn.
  - Mở port 80 (HTTP), 443 (HTTPS) cho public.
  - Port 8080 chỉ mở cho Nginx hoặc để thử nghiệm.

---

### 4. Tạo Security Group cho RDS

**Mục đích:**  
Chỉ cho phép EC2 truy cập vào database, tăng bảo mật cho RDS.

- Thực hiện theo hướng dẫn tại [Tạo Security Group](/2-Prerequisite-Steps/2-2-Security-Group/)
- **Lưu ý:**  
  - Chỉ mở port 3306 (MySQL) cho security group của EC2.

---

### 5. Tạo DB Subnet Group

**Mục đích:**  
Chỉ định các subnet private mà Amazon RDS có thể sử dụng, đảm bảo database không public ra internet.

- Thực hiện theo hướng dẫn tại [Tạo DB Subnet Group](/2-Prerequisite-Steps/2-3-DB-Subnet/)
- **Lưu ý:**  
  - Chọn đúng 2 private subnet thuộc 2 AZ khác nhau.

---

### 6. Tạo IAM Role cho EC2 (để thao tác với ECR)

**Mục đích:**  
Cấp quyền cho EC2 instance có thể pull/push Docker image từ/to Amazon ECR.

- Thực hiện theo hướng dẫn tại [Tạo IAM Role cho ECR](/2-Prerequisite-Steps/2-4-Create-IAM/)
- **Lưu ý:**  
  - Gắn đủ policy Read/Write cho ECR.
  - Gán role này cho EC2 khi khởi tạo.

---

### Lỗi thường gặp & cách xử lý

- Không tạo đủ subnet hoặc chọn sai loại subnet → RDS/EC2 không khởi tạo được.
- Security group không mở đúng port → EC2 không SSH được, EC2 không kết nối được RDS.
- Không gán IAM role cho EC2 → Không pull/push được image từ ECR.

---

### Xác minh sau khi hoàn thành

- Vào từng console (VPC, EC2, RDS, IAM) kiểm tra lại tài nguyên đã tạo đúng tên, đúng cấu hình.
- Kiểm tra các subnet, security group, DB subnet group đã liên kết đúng VPC.
- Lưu lại ID các tài nguyên để sử dụng cho các bước tiếp theo.

---

### Tham khảo lệnh AWS CLI (nâng cao)

Nếu muốn tự động hóa, bạn có thể tham khảo các lệnh AWS CLI tương ứng trong từng bước chi tiết.

---
