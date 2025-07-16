---
title : "Tạo EC2"
date: 2025-07-01
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

## 3. Tạo EC2 Instance

1. **Truy cập Amazon EC2 Console**:
   - Mở: [https://console.aws.amazon.com/ec2/](https://console.aws.amazon.com/ec2/).
   - Chọn **Launch instance**.
![image](/images/tao_ket_noi_ec2/screenshot_1752394076.png)
2. **Cấu hình EC2**:
   - **Name**: `spring-boot-ec2`.
   - **OS Image**: Chọn **Ubuntu Server 24.04 LTS**.
   ![image](/images/tao_ket_noi_ec2/screenshot_1752394125.png)
   - **Instance type**: `t3.medium` (2 vCPU, 4 GB RAM, Free Tier eligible).
   ![image](/images/tao_ket_noi_ec2/screenshot_1752394221.png)
   - **Key pair**: Tạo mới (`spring-boot-key`) hoặc chọn cặp khóa `.pem` hiện có.
   ![image](/images/tao_ket_noi_ec2/screenshot_1752394174.png)
   - **Network settings**:
     - **VPC**: Chọn `spring-boot-vpc`.
     - **Subnet**: Chọn public subnet (ví dụ: `spring-boot-vpc-public-us-east-1a`).
     - **Auto-assign public IP**: Bật **Enable**.
     - **Security Group**: Chọn `ec2-sg`.
     ![image](/images/tao_ket_noi_ec2/screenshot_1752394320.png)
   - Nhấn **Launch instance**.
![image](/images/tao_ket_noi_ec2/screenshot_1752394473.png)
![image](/images/tao_ket_noi_ec2/screenshot_1752401505.png)
3. **Gắn IAM Role**:
   - Trong **EC2 Console**, chọn instance `spring-boot-ec2`.
   - Nhấn **Actions** > **Security** > **Modify IAM role**.
   ![image](/images/tao_ket_noi_ec2/screenshot_1752394572.png)
   - Chọn role `CustomRWECRRole`.
   - Nhấn **Update IAM role**.
![image](/images/tao_ket_noi_ec2/screenshot_1752394609.png)
![image](/images/tao_ket_noi_ec2/screenshot_1752394625.png)
4. **Xác minh**:
   - Kiểm tra instance `spring-boot-ec2` trong trạng thái **Running** và có Public IP.

---

## 4. Kết nối SSH vào EC2 Instance bằng MobaXterm

### 4.1. Cài đặt MobaXterm

1. **Tải MobaXterm**:
   - Truy cập: [https://mobaxterm.mobatek.net/](https://mobaxterm.mobatek.net/).
   - Tải và cài đặt phiên bản mới nhất (Portable hoặc Installer).

### 4.2. Tạo phiên SSH

1. Mở **MobaXterm**, nhấn **Session** > **SSH**.
2. **Cấu hình**:
   - **Remote host**: Nhập Public IP hoặc Public DNS của EC2 (ví dụ: `ec2-54-123-45-67.compute-1.amazonaws.com`).
   - **Specify username**: Nhập `ubuntu` (cho Ubuntu AMI).
   - **Use private key**: Trong **Advanced SSH settings**, bật **Use private key**, chọn file `.pem` (ví dụ: `spring-boot-key.pem`).
3. Nhấn **OK** để kết nối.
![image](/images/tao_ket_noi_ec2/screenshot_1752394859.png)
### 4.3. Xác minh kết nối

- Nếu kết nối thành công, bạn sẽ thấy terminal EC2 trong MobaXterm.
![image](/images/tao_ket_noi_ec2/screenshot_1752394895.png)


## 5. Cài đặt Docker, Nginx, và MySQL Client trên EC2

1. **SSH vào EC2**:
   - Sử dụng MobaXterm để kết nối vào EC2.

2. **Cài đặt Docker**:
   - Chạy:
     ```bash
     sudo apt update -y
     sudo apt upgrade -y
     sudo apt install -y ca-certificates curl
     sudo install -m 0755 -d /etc/apt/keyrings
     sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
     sudo chmod a+r /etc/apt/keyrings/docker.asc
     echo \
       "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
       $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
       sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
     sudo apt update
     sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
     sudo usermod -aG docker ubuntu
     ```
   - Đăng xuất và đăng nhập lại SSH:
     ```bash
     exit
     ```
     Kết nối lại qua MobaXterm.
   - Kiểm tra Docker:
     ```bash
     docker --version
     ```
![image](/images/tao_ket_noi_ec2/screenshot_1752396889.png)
![image](/images/tao_ket_noi_ec2/screenshot_1752397133.png)
3. **Cài đặt Nginx**:
   - Chạy:
     ```bash
     sudo apt install -y nginx
     sudo systemctl start nginx
     sudo systemctl enable nginx
     ```
   - Kiểm tra trạng thái:
     ```bash
     sudo systemctl status nginx
     ```

4. **Cài đặt MySQL Client**:
   - Chạy:
     ```bash
     sudo apt install -y mysql-client
     ```
   - Kiểm tra:
     ```bash
     mysql --version
     ```

5. **Cài đặt AWS CLI trên EC2**:
   - Chạy:
     ```bash
     sudo apt update
     sudo apt install -y unzip
     curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
     unzip awscliv2.zip
     sudo ./aws/install
     ```
   - Kiểm tra:
     ```bash
     aws --version
     ```

---