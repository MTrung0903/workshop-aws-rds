---
title : "Test the application"
date: 2025-07-01
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

## 8. Test the application

1. **Access the application**:
- Open a browser or Postman, access:
```bash
http://<EC2-Public-IP>/api/<endpoint>
```
For example: If Spring Boot has an endpoint `/api/users`, access `http://<EC2-Public-IP>/api/users`.
![image](/images/test/screenshot_1752401348.png)
2. **Check logs for errors**:

- Spring Boot container log:
```bash
sudo docker logs <container-id-backend>
```
Replace `<container-id-backend>` with the ID of the `backend` container (taken from `docker ps`).
![image](/images/test/screenshot_1752400820.png)
- Nginx log:
```bash
sudo tail -f /var/log/nginx/error.log
```



