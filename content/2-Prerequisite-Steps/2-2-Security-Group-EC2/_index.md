---
title : "Create EC2 Security Group"
date: 2025-07-01
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

#### Creating a Security Group for Amazon EC2
**Information**: Security Groups act as virtual firewalls to control traffic in and out of your AWS resources. Each Security Group contains a set of rules that allow network traffic to the associated resources.

##### Steps to create a Security Group for EC2

1. Sign in to the AWS Management Console.

2. In the service menu, select **EC2 under **Compute**.

3. In the left navigation bar, under **Network & Security**, select **Security Groups**.

4. Click the **Create Security Group** button to begin the creation process.

5. In the Basic details section, enter the basic information:
- Security group name: Enter a descriptive name for the Security Group
- Description: Add a detailed description of the purpose of the Security Group
- VPC: Select the VPC where you want to apply this Security Group

6. In the Inbound rules section, add the following rules to allow incoming traffic:
- HTTP (80): Allow standard HTTP web traffic
- HTTPS (443): Allow HTTPS secure web traffic
- Custom TCP (8080): Allow traffic to application port 8080
- SSH (22): Allow SSH connections for server administration
🔒 **Security Note:** For production environments, it is recommended to limit SSH access to only trusted IP addresses instead of opening it to everyone (0.0.0.0/0).

7. (Optional) Configure **Outbound rules** if you need to limit outbound traffic. By default, all outbound traffic is allowed.

8. (Optional) Add tags to easily manage and categorize your Security Group.

9. Once the configuration is complete, click the **Create security group** button.

The new Security Group has been created and is ready to be assigned to your EC2 instances.

Security Group Created