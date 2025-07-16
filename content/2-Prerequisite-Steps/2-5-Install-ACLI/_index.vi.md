---
title : "Cài đặt AWS CLI trên máy cục bộ"
date: 2025-07-01
weight : 5
chapter : false
pre : " <b> 2.5 </b> "
---

### 1.6. Cài đặt AWS CLI trên máy cục bộ

1. **Tải file cài đặt**:
   - Truy cập: [https://awscli.amazonaws.com/AWSCLIV2.msi](https://awscli.amazonaws.com/AWSCLIV2.msi).
   - Tải file `AWSCLIV2.msi` (cho Windows) vào thư mục mặc định (ví dụ: `C:\Users\<YourUser>\Downloads`).

2. **Chạy trình cài đặt**:
   - Tìm file `AWSCLIV2.msi`, nhấp đúp để chạy.
   - Làm theo hướng dẫn:
     - Nhấn **Next** để tiếp tục.
     - Chấp nhận **License Agreement** và nhấn **Next**.
     - Giữ mặc định thư mục cài đặt (`C:\Program Files\Amazon\AWSCLIV2`) và nhấn **Next**.
     - Nhấn **Install**, cấp quyền Administrator nếu được yêu cầu.
     - Nhấn **Finish** để hoàn tất.

3. **Kiểm tra cài đặt**:
   - Mở **Command Prompt** hoặc **PowerShell** (Win + R, gõ `cmd` hoặc `powershell`).
   - Chạy:
     ```bash
     aws --version
     ```
   - Kết quả ví dụ: `aws-cli/2.27.50 Python/3.13.4 Windows/11 exe/AMD64`.
   ![image](/images/tao_aws_cli_local/Screenshot%202025-07-13%20144159.png)
   - Nếu báo lỗi `aws is not recognized`, kiểm tra biến PATH:
     - Nhấn Win + R, gõ `sysdm.cpl`, vào tab **Advanced** > **Environment Variables**.
     - Trong **System Variables**, tìm **Path**, thêm `C:\Program Files\Amazon\AWSCLIV2` nếu chưa có.
     - Mở lại Command Prompt/PowerShell và thử lại.

4. **Cấu hình AWS CLI**:
   - Chạy:
     ```bash
     aws configure
     ```
   - Nhập thông tin:
     - **AWS Access Key ID**: Lấy từ AWS Management Console:
       - Đăng nhập: [https://console.aws.amazon.com/iam/](https://console.aws.amazon.com/iam/).
       ![image](/images/tao_aws_cli_local/screenshot_1752392631.png)
       - Vào **Users** > Chọn user IAM > **Security credentials** > **Create access key**.
       ![image](/images/tao_aws_cli_local/screenshot_1752392649.png)
       - Chọn **Command Line Interface (CLI)**, tải file CSV chứa **Access Key ID** và **Secret Access Key**.
       ![image](/images/tao_aws_cli_local/screenshot_1752392694.png)
       ![image](/images/tao_aws_cli_local/screenshot_1752392743.png)
       ![image](/images/tao_aws_cli_local/screenshot_1752392760.png)
     - **AWS Secret Access Key**: Nhập từ file CSV.
     ![image](/images/tao_aws_cli_local/screenshot_1752392995.png)
     - **Default region name**: Nhập `us-east-1` (hoặc vùng bạn chọn).
     - **Default output format**: Nhập `json` hoặc nhấn Enter để dùng mặc định.
   - Thông tin được lưu vào:
     - `C:\Users\<YourUser>\.aws\credentials`
     - `C:\Users\<YourUser>\.aws\config`
