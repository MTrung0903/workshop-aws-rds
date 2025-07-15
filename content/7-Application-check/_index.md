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

2. **Check logs for errors**:

- Spring Boot container log:
```bash
sudo docker logs <container-id-backend>
```
Replace `<container-id-backend>` with the ID of the `backend` container (taken from `docker ps`).
- Nginx log:
```bash
sudo tail -f /var/log/nginx/error.log
```

3. **Check RDS connection**:

- In EC2 terminal:
```bash
mysql -h <RDS Endpoint> -u admin -p
```
- Enter RDS password.
- Check data:
```sql
USE first_cloud_users;
SHOW TABLES;
SELECT * FROM users;
```

4. **Troubleshooting**:

- **RDS connection error**: Check Security Group `rds-sg` allows `ec2-sg` on port 3306.

- **API error**: Check container log and make sure `SPRING_DATASOURCE_URL` is correct.

- **Nginx error**: Check `nginx.conf` and log `/var/log/nginx/error.log`.

---