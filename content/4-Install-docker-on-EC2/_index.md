---
title : "Install Docker on EC2"
date: 2025-07-01
weight : 4
chapter : false
pre : " <b> 4. </b> "
---
### Install Docker on EC2
1. Connect to EC2 via SSH:

- Use MobaXterm or terminal:

ssh -i <your-key.pem> ec2-user@3.25.221.88

2. Update the system:

sudo dnf update -y

3. Install Docker:

sudo dnf install -y docker
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ec2-user

4. Log out and log back in to apply the docker group:

ssh -i <your-key.pem> ec2-user@3.25.221.88

5. Check Docker: 

docker --version