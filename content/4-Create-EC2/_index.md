---
title : "Create EC2"
date: 2025-07-01
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

## 3. Create EC2 Instance

1. **Access Amazon EC2 Console**: 
- Open: [https://console.aws.amazon.com/ec2/](https://console.aws.amazon.com/ec2/). 
- Select **Launch instance**.
![image](/images/tao_ket_noi_ec2/screenshot_1752394076.png)
2. **EC2 configuration**: 
- **Name**: `spring-boot-ec2`. 
- **OS Image**: Select **Ubuntu Server 24.04 LTS**. 
![image](/images/tao_ket_noi_ec2/screenshot_1752394125.png)
- **Instance type**: `t3.medium` (2 vCPU, 4 GB RAM, Free Tier eligible). 
![image](/images/tao_ket_noi_ec2/screenshot_1752394221.png)
- **Key pair**: Create a new one (`spring-boot-key`) or select an existing `.pem` key pair.
![image](/images/tao_ket_noi_ec2/screenshot_1752394174.png)
- **Network settings**:
- **VPC**: Select `spring-boot-vpc`.

- **Subnet**: Select public subnet (eg: `spring-boot-vpc-public-us-east-1a`).

- **Auto-assign public IP**: Turn on **Enable**.

- **Security Group**: Select `ec2-sg`.
![image](/images/tao_ket_noi_ec2/screenshot_1752394320.png)
- Click **Launch instance**.
![image](/images/tao_ket_noi_ec2/screenshot_1752394473.png)
![image](/images/tao_ket_noi_ec2/screenshot_1752401505.png)
3. **Assign IAM Role**:

- In **EC2 Console**, select the `spring-boot-ec2` instance.

- Click **Actions** > **Security** > **Modify IAM role**.
![image](/images/tao_ket_noi_ec2/screenshot_1752394572.png)
- Select the `CustomRWECRRole` role.

- Click **Update IAM role**.
![image](/images/tao_ket_noi_ec2/screenshot_1752394609.png)
![image](/images/tao_ket_noi_ec2/screenshot_1752394625.png)
4. **Verification**:

- Check the `spring-boot-ec2` instance is in **Running** state and has Public IP.

---

## 4. Connect SSH to EC2 Instance using MobaXterm

### 4.1. Install MobaXterm

1. **Download MobaXterm**:

- Visit: [https://mobaxterm.mobatek.net/](https://mobaxterm.mobatek.net/).
- Download and install the latest version (Portable or Installer).

### 4.2. Create SSH session

1. Open **MobaXterm**, click **Session** > **SSH**.

2. **Configuration**:
- **Remote host**: Enter the Public IP or Public DNS of EC2 (for example: `ec2-54-123-45-67.compute-1.amazonaws.com`).
- **Specify username**: Enter `ubuntu` (for Ubuntu AMI).
- **Use private key**: In **Advanced SSH settings**, enable **Use private key**, select the `.pem` file (e.g. `spring-boot-key.pem`).

3. Click **OK** to connect.
![image](/images/tao_ket_noi_ec2/screenshot_1752394859.png)
### 4.3. Verify connection

- If the connection is successful, you will see the EC2 terminal in MobaXterm.
![image](/images/tao_ket_noi_ec2/screenshot_1752394895.png)


## 5. Install Docker, Nginx, and MySQL Client on EC2

1. **SSH into EC2**:
- Use MobaXterm to connect to EC2.

2. **Install Docker**: 
- Run: 
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
- Log out and log back in to SSH:
```bash
exit
```
Reconnect via MobaXterm.
- Check Docker:
```bash
docker --version
```
![image](/images/tao_ket_noi_ec2/screenshot_1752396889.png)
![image](/images/tao_ket_noi_ec2/screenshot_1752397133.png)
3. **Install Nginx**:
- Run:
```bash
sudo apt install -y nginx
sudo systemctl start nginx
sudo systemctl enable nginx
```
- Check status:
```bash
sudo systemctl status nginx
```

4. **Install MySQL Client**:
- Run:
```bash
sudo apt install -y mysql-client
```
- Check:
```bash
mysql --version
```

5. **Install AWS CLI on EC2**:
- Run:
```bash
sudo apt update
sudo apt install -y unzip
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" 
unzip awscliv2.zip 
sudo ./aws/install 
``` 
- Check: 
```bash 
aws --version 
```

---