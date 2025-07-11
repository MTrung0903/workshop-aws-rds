---
title : "Cấu hình CloudWatch"
date: 2025-07-01
weight : 7
chapter : false
pre : " <b> 7. </b> "
---


## 7.1. Cài CloudWatch Agent trên EC2

- Thêm vào User Data:
  ```bash
  dnf install -y amazon-cloudwatch-agent
  cat <<EOF > /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json
  {
    "agent": { "metrics_collection_interval": 60 },
    "metrics": {
      "namespace": "EcommerceIdentityApp",
      "metrics_collected": {
        "cpu": { "measurement": ["cpu_usage_active"] },
        "mem": { "measurement": ["mem_used_percent"] }
      }
    },
    "logs": {
      "logs_collected": {
        "files": {
          "collect_list": [
            {
              "file_path": "/var/log/docker",
              "log_group_name": "ecommerce-app-logs",
              "log_stream_name": "{instance_id}"
            }
          ]
        }
      }
    }
  }
  EOF
  /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -s -c file:/opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json
  ```

## 7.2. Tạo IAM Role cho EC2

- Vào **IAM Console** > **Roles** > **Create role** > **AWS service** > **EC2**
- Gắn policy: `CloudWatchAgentServerPolicy`
- Name: `ecommerce-ec2-cloudwatch-role`
- Gắn role này vào Launch Template

## 7.3. Tạo Alarm & Dashboard

- **Alarm**: CPUUtilization > 70% trong 5 phút, gửi SNS hoặc trigger scaling
- **Dashboard**: Thêm widget CPU, memory, request count, latency