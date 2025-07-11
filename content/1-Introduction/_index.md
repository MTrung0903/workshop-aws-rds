---
title : "Introduction"
date: 2025-07-01
weight : 1
chapter : false
pre : " <b> 1. </b> "
---

The **"AWS Cloud Deployment with Spring Boot and Docker"** workshop provides a hands-on guide to deploying a Spring Boot application, packaged as a Docker image, on Amazon Web Services (AWS) while connecting it to a relational database service (RDS) with MySQL. This workshop aims to equip participants with practical skills in cloud-native application deployment, a critical competency in modern software development. Spring Boot, with its robust integration of Spring Data JPA and the portability of Docker, enables rapid deployment and scalability, while AWS offers a reliable cloud infrastructure with automation and security features. Adapted from the original "workshop aws-rds.txt" documentation, this guide replaces a Node.js application with Spring Boot and integrates database connectivity using custom environment variables (DBMS_*) or standard Spring Boot variables (SPRING_DATASOURCE_*).

This workshop is designed for beginners exploring AWS and developers seeking to optimize CI/CD (Continuous Integration/Continuous Deployment) pipelines using Docker and cloud computing. By the end, you will understand how to set up a secure network infrastructure (VPC), deploy a Spring Boot application, and manage cloud resources efficiently. These skills are applicable to real-world projects such as building APIs, user management systems, or enterprise applications, making this a valuable step toward mastering cloud-based development.

##### Objectives
- Deploy a Spring Boot application from a Docker image on Docker Hub to an Amazon EC2 instance.
- Connect the application to an RDS MySQL database (database database-workshop).
- Ensure security, high availability (Multi-AZ), and a streamlined process for cleaning up resources after completion.

