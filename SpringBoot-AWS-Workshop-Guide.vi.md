# Hướng dẫn triển khai ứng dụng Spring Boot với Docker, RDS, Auto Scaling, ALB trên AWS

#aws  
#spring-boot  
#cloud-computing  
#docker  
#rds  
#auto-scaling  
#application-load-balancer  

---

## Giới thiệu

Bài hướng dẫn này sẽ giúp bạn từng bước triển khai một ứng dụng Spring Boot đóng gói Docker lên AWS, sử dụng Amazon EC2 Auto Scaling, RDS MySQL, Application Load Balancer (ALB), giám sát với CloudWatch và triển khai blue-green.  
Bạn sẽ thực hành trên AWS Console, đảm bảo ứng dụng có khả năng mở rộng, sẵn sàng cao, bảo mật và dễ dàng dọn dẹp tài nguyên sau khi hoàn thành.

---

## Yêu cầu trước khi bắt đầu

- Tài khoản AWS (đã xác thực, có quyền tạo EC2, RDS, VPC, IAM…)
- Kiến thức cơ bản về AWS Console, Docker, Spring Boot
- Đã build/push Docker image Spring Boot lên Docker Hub (ví dụ: `trungho93/identity-service:0.9.0`)
- Đã có SSH key pair để truy cập EC2 (nếu cần)

---

## 1. Chuẩn bị hạ tầng mạng (VPC, Subnet, Security Group)

### 1.1. Tạo VPC và Subnet

1. Vào **AWS Console** → **VPC** → **Create VPC**  
   - Name: `ecommerce-vpc`
   - IPv4 CIDR: `10.0.0.0/16`
   - Tenancy: Default
   - Chọn 2 AZs (ví dụ: `us-east-1a`, `us-east-1b`)
   - Tạo 2 public subnets: `10.0.1.0/24`, `10.0.2.0/24`
   - Tạo 2 private subnets: `10.0.3.0/24`, `10.0.4.0/24`
   - NAT Gateway: 1 per AZ
   - Enable DNS hostnames & resolution

2. Vào **Subnets** → chọn từng public subnet → **Edit subnet settings** → Enable auto-assign public IPv4 address.

### 1.2. Tạo Security Group

- **ALB**:  
  - Name: `ecommerce-alb-sg`
  - Inbound: HTTP (80), HTTPS (443) từ `0.0.0.0/0`
- **EC2**:  
  - Name: `ecommerce-ec2-sg`
  - Inbound: TCP 8080 từ ALB SG, SSH (22) từ IP cá nhân
- **RDS**:  
  - Name: `ecommerce-rds-sg`
  - Inbound: MySQL (3306) từ EC2 SG

### 1.3. Tạo DB Subnet Group

- Vào **RDS** → **Subnet groups** → **Create DB Subnet Group**
- Name: `ecommerce-rds-subnet-group`
- Chọn 2 private subnets

---

## 2. Tạo RDS MySQL Instance

1. Vào **RDS Console** → **Create database**
2. Chọn **Standard create** → Engine: MySQL 8.0
3. Template: Production (bật Multi-AZ)
4. Cấu hình:
   - DB instance identifier: `ecommerce-rds-instance`
   - Master username: `admin`
   - Master password: tự chọn hoặc auto-generate
   - DB instance class: `db.t3.micro`
   - Storage: 20GB, General Purpose SSD (gp2)
   - VPC: `ecommerce-vpc`
   - DB Subnet Group: `ecommerce-rds-subnet-group`
   - Security Group: `ecommerce-rds-sg`
   - Public access: No
   - Enable automated backups, encryption
5. Chọn **Create database**
6. Ghi lại Endpoint, Port, Username, Password

**Tạo database và bảng:**
- Kết nối MySQL:
  ```bash
  mysql -h <RDS Endpoint> -P 3306 -u admin -p
  ```
- Tạo database và bảng:
  ```sql
  CREATE DATABASE IF NOT EXISTS first_cloud_users;
  USE first_cloud_users;
  CREATE TABLE `user` (
      `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
      `first_name` VARCHAR(45) NOT NULL,
      `last_name` VARCHAR(45) NOT NULL,
      `email` VARCHAR(100) NOT NULL UNIQUE,
      `phone` VARCHAR(15) NOT NULL,
      `comments` TEXT NOT NULL,
      `status` ENUM('active', 'inactive') NOT NULL DEFAULT 'active'
  ) ENGINE = InnoDB;
  ```

---

## 3. Tạo Application Load Balancer (ALB) và Target Group

### 3.1. Tạo Target Group

1. Vào **EC2 Console** → **Load Balancing** → **Target Groups**
2. Nhấn **Create target group**
   - Target type: Instance
   - Name: `ecommerce-app-tg`
   - Protocol: HTTP
   - Port: 8080
   - VPC: `ecommerce-vpc`
   - Health check protocol: HTTP
   - Health check path: `/health`
   - Healthy threshold: 5, Unhealthy threshold: 2, Timeout: 5, Interval: 30, Success codes: 200

### 3.2. Tạo Application Load Balancer

1. Vào **EC2 Console** → **Load Balancers** → **Create Load Balancer** → Application Load Balancer
2. Basic configuration:
   - Name: `ecommerce-app-alb`
   - Scheme: Internet-facing
   - IP address type: IPv4
3. Network mapping:
   - VPC: `ecommerce-vpc`
   - Availability Zones: Chọn cả 2 public subnets
4. Security groups: Chọn `ecommerce-alb-sg`
5. Listeners and routing:
   - Protocol: HTTP, Port: 80
   - Default action: Gán Target Group vừa tạo (`ecommerce-app-tg`)
   - (Có thể thêm HTTPS nếu đã có SSL certificate)
6. Nhấn **Create load balancer**
7. Ghi lại DNS name của ALB

---

## 4. Tạo EC2 Launch Template & Auto Scaling Group

### 4.1. Tạo Launch Template

1. Vào **EC2 Console** → **Launch Templates** → **Create launch template**
2. Name: `ecommerce-spring-boot-template`
3. AMI: Amazon Linux 2023
4. Instance type: `t3.micro`
5. Key pair: Chọn SSH key
6. Security Group: `ecommerce-ec2-sg`
7. User Data:
   ```bash
   #!/bin/bash
   dnf update -y
   dnf install -y docker amazon-cloudwatch-agent
   systemctl start docker
   systemctl enable docker
   usermod -aG docker ec2-user
   docker pull trungho93/identity-service:0.9.0
   docker run -d -p 8080:8080 \
     -e DBMS_CONNECTION=jdbc:mysql://<RDS Endpoint>:3306/first_cloud_users \
     -e DBMS_USERNAME=admin \
     -e DBMS_PASSWORD=<RDS Password> \
     --name ecommerce-spring-boot-app trungho93/identity-service:0.9.0
   ```
   > Thay `<RDS Endpoint>` và `<RDS Password>` bằng giá trị thực tế.

### 4.2. Tạo Auto Scaling Group

1. Vào **Auto Scaling Groups** → **Create Auto Scaling group**
2. Name: `ecommerce-spring-boot-asg`
3. Launch template: `ecommerce-spring-boot-template`
4. VPC: `ecommerce-vpc`
5. Subnets: 2 public subnets
6. Desired/Min/Max capacity: 2/2/4
7. Scaling policy: Target tracking, CPU 70%
8. Target group: `ecommerce-app-tg`
9. Nhấn **Create Auto Scaling group**

---

## 5. Cấu hình CloudWatch Monitoring

### 5.1. Cài CloudWatch Agent trên EC2 (thêm vào User Data ở trên)

```bash
dnf install -y amazon-cloudwatch-agent
cat <<EOF > /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json
{
  "agent": { "metrics_collection_interval": 60 },
  "metrics": {
    "namespace": "EcommerceIdentityApp",
    "metrics_collected": {
      "cpu": { "measurement": ["cpu_usage_active"] },
      "mem": { "measurement": ["mem_used_percent"] }
    }
  },
  "logs": {
    "logs_collected": {
      "files": {
        "collect_list": [
          {
            "file_path": "/var/log/docker",
            "log_group_name": "ecommerce-app-logs",
            "log_stream_name": "{instance_id}"
          }
        ]
      }
    }
  }
}
EOF
/opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -s -c file:/opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json
```

### 5.2. Tạo IAM Role cho EC2

- Vào **IAM Console** → **Roles** → **Create role** → **AWS service** → **EC2**
- Gắn policy: `CloudWatchAgentServerPolicy`
- Name: `ecommerce-ec2-cloudwatch-role`
- Gắn role này vào Launch Template

### 5.3. Tạo Alarm & Dashboard

- **Alarm**: CPUUtilization > 70% trong 5 phút, gửi SNS hoặc trigger scaling
- **Dashboard**: Thêm widget CPU, memory, request count, latency

---

## 6. Triển khai Blue-Green Deployment (Nâng cao)

1. Tạo target group mới: `ecommerce-app-tg-green` (HTTP, port 8080, health check `/health`)
2. Tạo phiên bản mới của Launch Template với Docker image mới (ví dụ: `trungho93/identity-service:0.9.1`)
3. Tạo Auto Scaling Group mới: `ecommerce-spring-boot-asg-green`, gắn với `ecommerce-app-tg-green`
4. Chuyển lưu lượng sang target group mới:
   ```bash
   aws elbv2 modify-listener --listener-arn <listener-arn> --default-actions Type=forward,TargetGroupArn=<green-tg-arn>
   ```
5. Sau khi kiểm tra health checks, terminate Auto Scaling Group cũ.

---

## 7. Kiểm thử & Giám sát

1. Truy cập ứng dụng qua **ALB DNS name** (ví dụ: `http://ecommerce-app-alb-xxxx.elb.amazonaws.com`)
2. Kiểm tra endpoint `/health` và các endpoint REST khác
3. SSH vào EC2, kiểm tra log:  
   ```bash
   docker logs ecommerce-spring-boot-app
   ```
4. Vào **CloudWatch Console** → **Log groups** → `ecommerce-app-logs`, kiểm tra log stream theo instance ID
5. Kiểm thử hiệu suất: Dùng **JMeter** để mô phỏng 10,000 người dùng đồng thời, đảm bảo độ trễ <500ms

---

## 8. Dọn dẹp tài nguyên

1. Xóa Auto Scaling Group: `ecommerce-spring-boot-asg`, `ecommerce-spring-boot-asg-green`
2. Xóa ALB, target groups
3. Xóa RDS instance, subnet group
4. Xóa VPC, NAT Gateway, security groups
5. Xóa CloudWatch log group, alarm, dashboard
6. Xóa IAM Role: `ecommerce-ec2-cloudwatch-role`

**Lưu ý:** Sao lưu dữ liệu RDS trước khi xóa!

---

## Kết luận

Bạn đã hoàn thành quy trình triển khai, vận hành, giám sát và dọn dẹp một ứng dụng Spring Boot hiện đại trên AWS với các best practices về bảo mật, sẵn sàng cao và tự động hóa.  
Chúc mừng bạn đã hoàn thành workshop! 