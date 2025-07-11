---
title : "Deploy Spring Boot Application from Docker Hub"
date: 2025-07-01
weight : 6
chapter : false
pre : " <b> 6. </b> "
---
### Deploy Spring Boot Application from Docker Hub

1. Pull Docker image from Docker Hub:
docker pull trungho93/identity-service:0.9.0
- If the image is private, log in to Docker Hub:
docker login
- Enter Docker Hub username and password.

2. Configure RDS connection:
- Pass custom environment variables (DBMS_*) to connect to RDS:
docker run -d -p 8080:8080 \
-e DBMS_CONNECTION=jdbc:mysql://database-workshop.ctsk2qmig8wy.ap-southeast-2.rds.amazonaws.com:3306/database-workshop \
-e DBMS_USERNAME=admin \
-e DBMS_PASSWORD=trung09032003 \
--name spring-boot-app trungho93/identity-service:0.9.0

3. Run container:
docker run -d -p 5000:5000 \
-e DBMS_CONNECTION=jdbc:mysql://database-workshop.ctsk2qmig8wy.ap-southeast-2.rds.amazonaws.com:3306/database-workshop \ 
-e DBMS_USERNAME=admin \ 
-e DBMS_PASSWORD=trung09032003 \ 
--name spring-boot-app trungho93/identity-service:0.9.0

4. Test the application: 
http://3.25.221.88:8080/identity/auth/token

Check log if there are errors:
docker logs spring-boot-app