---
title : "Create ECR Repository"
date: 2025-07-01
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

### 2.1. Create ECR Repository

1. **Access Amazon ECR Console**:

- Open: [https://console.aws.amazon.com/ecr/](https://console.aws.amazon.com/ecr/).

- Select **Create repository**.

2. **Configure Repository**:

- **Repository name**: `spring-boot-app`.

- **Tag immutability**: Select **Mutable**.

- **Scan on push**: Enable to scan for security vulnerabilities.

- Click **Create repository**.

3. **Save URI**:

- Note down the repository URI, e.g. `<account-id>.dkr.ecr.us-east-1.amazonaws.com/spring-boot-app`.

### 2.2. Push Docker image to ECR

1. **Ensure local Docker image**:

- Verify local Spring Boot image (e.g. `trungho93/identity-service:0.9.0`):
```bash
docker images
```

2. **Log in to ECR**:

- Run:
```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.us-east-1.amazonaws.com
```
- Replace `<account-id>` with your AWS account ID (e.g. `238702553701`).

- Output: `Login Succeeded`.

3. **Tag and push image**: 
- Tag images: 
```bash 
docker tag trungho93/identity-service:0.9.0 <account-id>.dkr.ecr.us-east-1.amazonaws.com/spring-boot-app:latest 
``` 
- Push images: 
```bash 
docker push <account-id>.dkr.ecr.us-east-1.amazonaws.com/spring-boot-app:latest 
```

4. **Verification**: 
- Access **ECR Console**, select repository `spring-boot-app`, check image with tag `latest`.