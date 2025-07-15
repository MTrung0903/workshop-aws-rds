---
title : " How to Deploy a Spring Boot Application on AWS with Docker"
date: 2025-07-01
weight : 1
chapter : false
---

# How to Deploy a Spring Boot Application on AWS with Docker

## General information

This document guides you through deploying a Spring Boot application (backend API) using Docker on Amazon EC2, integrating with Amazon ECR for Docker image storage, Amazon RDS for MySQL database, and Nginx as a reverse proxy. The guide is updated with the latest AWS features (as of July 2025) and optimized for production environments, while leveraging the AWS Free Tier to minimize costs.

---

## Objectives

- Create and push a Docker image of a Spring Boot application to Amazon ECR.
- Deploy the application on Amazon EC2 using Docker Compose.
- Use Nginx as a reverse proxy to route traffic from port 80 to Spring Boot on port 8080.
- Connect the application to a MySQL database on Amazon RDS (database `first_cloud_users`).
- Ensure security, high availability (Multi-AZ), and easy resource cleanup.

---

## Assumptions

- You already have a **Spring Boot Docker image** (e.g. `trungho93/identity-service:0.9.0`) that has been tested to work well on your local environment or Docker Hub.
- The Spring Boot application has the database configuration in the `application.yml` or `application.properties` file as follows:

```yaml
spring:
datasource:
url: ${DBMS_CONNECTION:jdbc:mysql://localhost:3306/first_cloud_users?useSSL=false&serverTimezone=UTC}
driverClassName: com.mysql.cj.jdbc.Driver
username: ${DBMS_USERNAME:root}
password: ${DBMS_PASSWORD:09032003}
jpa:
hibernate:
ddl-auto: update
```

- The application uses port **8080** (Spring Boot default).

- You have access to:
- **AWS Management Console**.
- **AWS CLI** (version 2.x).
- **Docker CLI** (latest version).

- SSH key pair (`.pem` file) to access EC2.

- Local machine with root or sudo privileges to install tools.

- You have installed **MobaXterm** to SSH into EC2.

---

## Main content

1. Prepare infrastructure (VPC, Security Groups, IAM Role, DB Subnet Group).

2. Create and push Docker image to Amazon ECR.
3. Create EC2 instance.
4. Install Docker, Nginx, and MySQL Client on EC2.
5. Create RDS database instance.
6. Deploy application with Docker Compose.
7. Test application.
8. Clean up resources.

---

## Important notes

- **Helpful tip**: Consider using Amazon ECS or EKS to manage containers in production, instead of running directly on EC2.
- **Security**: Configure Security Groups and VPCs properly, use AWS Secrets Manager to manage sensitive information.

- **Cost**: Track costs via **AWS Cost Explorer** and clean up resources after the workshop to avoid additional costs.

---