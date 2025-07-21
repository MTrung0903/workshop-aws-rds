---
title : "Preparation Steps"
date: 2025-07-01
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

## AWS Infrastructure Preparation Steps

**Information:**
Before you deploy Amazon RDS and your applications, you need to set up the appropriate network and security environment. The steps below will help you prepare the necessary infrastructure, ensure it is secure, and ready for AWS services.

---

### Quick Checklist

- [ ] Have an AWS account with administrative rights
- [ ] Have defined the deployment region (e.g. us-east-1)
- [ ] Have prepared resource names (VPC, subnet, security group, etc.) according to the naming standard

---

### 1. Create a VPC (Virtual Private Cloud)

**Purpose:**
Create a separate virtual network environment to isolate AWS resources, increase security and control traffic.

- Follow the detailed instructions at [Create VPC](/2-Prerequisite-Steps/2-1-VPC/)
- **Note:** Select the appropriate IP range, enable DNS hostnames and DNS resolution.

---

### 2. Create Subnet

**Purpose:**
Divide VPC into subnets for Multi-AZ deployment, separate public (for EC2) and private (for RDS) subnets.

- Follow the instructions at [Create VPC](/2-Prerequisite-Steps/2-1-VPC/)
- **Note:**
- Create at least 2 public subnets (for EC2) and 2 private subnets (for RDS).
- Enable auto-assign public IP for public subnets.

---

### 3. Create Security Group for EC2

**Purpose:**
Control network traffic to/from application server (EC2), ensure only necessary connections are allowed.

- Follow the instructions at [Create Security Group](/2-Prerequisite-Steps/2-2-Security-Group/)
- **Note:**
- Only open port 22 (SSH) for your IP.

- Open port 80 (HTTP), 443 (HTTPS) for public.

- Port 8080 is only open for Nginx or for testing.

---

### 4. Create Security Group for RDS

**Purpose:**
Only allow EC2 to access the database, increase security for RDS.

- Follow the instructions at [Create Security Group](/2-Prerequisite-Steps/2-2-Security-Group/)
- **Note:**
- Only open port 3306 (MySQL) for EC2's security group.

---

### 5. Create DB Subnet Group

**Purpose:**
Specify the private subnets that Amazon RDS can use, ensuring that the database is not public to the internet.

- Follow the instructions at [Create DB Subnet Group](/2-Prerequisite-Steps/2-3-DB-Subnet/)
- **Note:**
- Select the correct 2 private subnets belonging to 2 different AZs.

---

### 6. Create IAM Role for EC2 (to work with ECR)

**Purpose:**
Give permission for EC2 instance to pull/push Docker images from/to Amazon ECR.

- Follow the instructions at [Create IAM Role for ECR](/2-Prerequisite-Steps/2-4-Create-IAM/)
- **Note:**
- Attach enough Read/Write policies to ECR.

- Assign this role to EC2 when initializing.

---

### Common errors & how to handle

- Not creating enough subnets or choosing the wrong subnet type → RDS/EC2 cannot initialize.

- Security group does not open the correct port → EC2 cannot SSH, EC2 cannot connect to RDS.

- Not assigning IAM role to EC2 → Cannot pull/push image from ECR.

---

### Verify after completion

- Go to each console (VPC, EC2, RDS, IAM) to check that the created resources have the correct name and configuration.

- Check that the subnets, security groups, DB subnet groups are correctly linked to the VPC.

- Save the resource IDs for use in the next steps.

---

### Refer to AWS CLI commands (advanced)

If you want to automate, you can refer to the corresponding AWS CLI commands in each detailed step.

---