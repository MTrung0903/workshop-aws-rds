---
title : "Introduction"
date: 2025-07-01
weight : 1
chapter : false
pre : " <b> 1. </b> "
---
# How to deploy Spring Boot applications on AWS with Docker

ℹ️ **Information**: This document guides you through deploying a Spring Boot application (Backend) on Docker, using AWS services such as EC2, RDS, and ECR, integrating Nginx as a reverse proxy. The guide is updated with the latest AWS features (as of 2025) and optimized for production environments.

## Objectives

- Deploy a Spring Boot application from a Docker image on Amazon ECR.
- Use Nginx as a reverse proxy to route traffic to the Backend.

- Connect the application to a MySQL database on Amazon RDS.
- Ensure security, high availability (Multi-AZ), and easy resource cleaning.

## Main content

1. Prepare the infrastructure

2. Create and push the image to Amazon ECR
3. Create an EC2 Instance

4. Install Docker, Nginx, and MySQL Client on EC2
5. Create an RDS Database Instance

6. Deploy Spring Boot application with Docker Compose
7. Test the application
8. Clean up resources

💡 **Helpful tip**: Use **Amazon ECS** or **EKS** instead of running Docker directly on EC2 to manage containers more efficiently in production environments.

🔒 **Security note**: Ensure proper Security Groups and VPC configuration, restrict access, and use AWS Secrets Manager to manage sensitive information.

⚠️ **Warning**: Monitor AWS costs via **AWS Cost Explorer** and clean up resources after completion to avoid unnecessary costs.