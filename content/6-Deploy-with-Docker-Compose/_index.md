---
title : "Deploying Spring Boot Applications with Docker Compose"
date: 2025-07-01
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

## 7. Deploying Spring Boot Applications with Docker Compose

### 7.1. Logging in to Amazon ECR from EC2

1. In the MobaXterm terminal, run:
```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.us-east-1.amazonaws.com
```
- Replace `<account-id>` with your AWS account ID.
- Output: `Login Succeeded`.

### 7.2. Create Docker Compose file

1. **Create directory**:

- In EC2 terminal:
```bash
mkdir spring-boot-app && cd spring-boot-app
```

2. **Create `docker-compose.yml` file**:

Run:
```bash
nano docker-compose.yml
```
- Paste the following content, replacing the values `<account-id>`, `<region>`, `<RDS Endpoint>`, and `<RDS Password>`:
```yaml
version: '3.8'
services:
nginx:
image: nginx:latest
ports:
- "80:80"
volumes:
- ./nginx.conf:/etc/nginx/conf.d/app.conf
depends_on:
- backend
networks:
- app-network
backend:
image: <account-id>.dkr.ecr.<region>.amazonaws.com/spring-boot-app:latest 
ports: 
- "8080:8080" 
environment: 
- SPRING_DATASOURCE_URL=jdbc:mysql://<RDS Endpoint>:3306/first_cloud_users?useSSL=false&serverTimezone=UTC 
- SPRING_DATASOURCE_USERNAME=admin 
- SPRING_DATASOURCE_PASSWORD=<RDS Password> 
- SPRING_JPA_HIBERNATE_DDL_AUTO=update 
networks: 
- app-network 
networks: 
app-network: 
driver: bridge 
``` 
- Save file: Press `Ctrl+O`, Enter, `Ctrl+X`.

### 7.3. Create Nginx configuration file

1. **Create file `nginx.conf`**: 
- Run: 
```bash 
nano nginx.conf 
``` 
- Paste content: 
```nginx 
server { 
listen 80; 
server_name _; 
location / { 
proxy_pass http://backend:8080; 
proxy_set_header Host $host; 
proxy_set_header X-Real-IP $remote_addr; 
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; 
proxy_set_header X-Forwarded-Proto $scheme; 
} 
} 
``` 
- Save file: Press `Ctrl+O`, Enter, `Ctrl+X`.

### 7.4. Run Docker Compose

1. **Check the configuration files**:

- Make sure `docker-compose.yml` and `nginx.conf` are created in the `spring-boot-app` directory.

2. **Run the container**:

- Run:
```bash
sudo docker compose -f docker-compose.yml up -d
```

3. **Verify**:

- Check the container:
```bash
docker ps
```
- You should see 2 containers: `nginx` and `backend`.

---