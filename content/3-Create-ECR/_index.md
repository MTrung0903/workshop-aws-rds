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
![image](/images/push_image/screenshot_1752393032.png)
2. **Configure Repository**:

- **Repository name**: `spring-boot-app`.

- **Tag immutability**: Select **Mutable**.
![image](/images/push_image/screenshot_1752393109.png)
- **Scan on push**: Enable to scan for security vulnerabilities.

- Click **Create repository**.
![image](/images/push_image/screenshot_1752393166.png)
3. **Save URI**:
![image](/images/push_image/screenshot_1752393208.png)
- Note down the repository URI, e.g. `<account-id>.dkr.ecr.us-east-1.amazonaws.com/spring-boot-app`.

### 2.2. Push Docker image to ECR

1. **Prepare your application source code**:

- Clone your Spring Boot project from GitHub (or prepare your source code):
  ```bash
  git clone https://github.com/MTrung0903/identity-service.git
  cd <project-folder>
  ```
- Ensure a `Dockerfile` exists in the project root. If not, create one with the following content:
  ```dockerfile
  FROM maven:3.9.8-amazoncorretto-21 AS build
  WORKDIR /app
  COPY pom.xml .
  COPY src ./src
  RUN mvn package -DskipTests
  FROM amazoncorretto:21.0.4
  WORKDIR /app
  COPY --from=build /app/target/*.jar app.jar
  ENTRYPOINT ["java", "-jar", "app.jar"]

  ```
- Build the Spring Boot JAR file (if using Maven):
  ```bash
  ./mvnw clean package
  # or
  mvn clean package
  ```
- Build the Docker image:
  ```bash
  docker build -t <your-image-name>:<tag> .
  ```

2. **Ensure local Docker image**:

- Verify local Spring Boot image (e.g. `trungho93/identity-service:0.9.0`):
```bash
docker images
```

3. **Log in to ECR**:

- Run:
```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.us-east-1.amazonaws.com
```
- Replace `<account-id>` with your AWS account ID (e.g. `238702553701`).

- Output: `Login Succeeded`.

4. **Tag and push image**: 
- Tag images: 
```bash 
docker tag trungho93/identity-service:0.9.0 <account-id>.dkr.ecr.us-east-1.amazonaws.com/spring-boot-app:latest 
``` 
![image](/images/push_image/screenshot_1752393376.png)
![image](/images/push_image/screenshot_1752393426.png)
- Push images: 
```bash 
docker push <account-id>.dkr.ecr.us-east-1.amazonaws.com/spring-boot-app:latest 
```

![image](/images/push_image/screenshot_1752393822.png)
![image](/images/push_image/screenshot_1752393914.png)
5. **Verification**: 
- Access **ECR Console**, select repository `spring-boot-app`, check image .