---
title : "Cài đặt docker trên EC2"
date: 2025-07-01
weight : 4
chapter : false
pre : " <b> 4. </b> "
---
### Cài đặt Docker trên EC2
1. Kết nối vào EC2 qua SSH:

- Sử dụng MobaXterm hoặc terminal:

    ssh -i <your-key.pem> ec2-user@3.25.221.88

2. Cập nhật hệ thống:

    sudo dnf update -y
    
3. Cài đặt Docker:

    sudo dnf install -y docker
    sudo systemctl start docker
    sudo systemctl enable docker
    sudo usermod -aG docker ec2-user

4. Đăng xuất và đăng nhập lại để áp dụng nhóm docker:

    ssh -i <your-key.pem> ec2-user@3.25.221.88

5. Kiểm tra Docker:

    docker --version