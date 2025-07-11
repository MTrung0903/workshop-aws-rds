---
title : "Create RDS Security Group"
date: 2025-07-01
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---
## Create RDS Security Group
#### Create Security Group for Amazon RDS
ℹ️ **Information**: Security Groups for Amazon RDS act as virtual firewalls to control network traffic to and from your database. Properly configuring Security Groups is an important step to protecting your data in AWS.

##### Steps to create a Security Group for RDS
1. Sign in to the AWS Management Console.

2. In the service menu, select **VPC** under **Networking & Content Delivery**.

3. In the left navigation bar, under **Security**, select **Security Groups**.

4. Click the **Create security group** button to start the creation process.

5. In the Basic details section, enter the basic information:

- Security group name: Enter a descriptive name for the Security Group
- Description: Add a detailed description of the purpose of the Security Group
- VPC: Select the VPC where you will deploy the RDS database
6. In the Inbound rules section, add rules to allow traffic to the database:

- Select MySQL/Aurora from the Type list
- Port 3306 will be automatically populated
- For Source, select the Security Group of the EC2 instance you created earlier
🔒 **Security Note**: Allow connections only from specific sources instead of opening the database port to all IP addresses (0.0.0.0/0). This follows the principle of least privilege and enhances security.

7. (Optional) Configure Outbound rules if you need to limit outbound traffic. By default, all outbound traffic is allowed.

8. Once the configuration is complete, click the **Create security group** button.

The new Security Group has been created and is ready to be assigned to your RDS DB instance.

⚠️ **Warning**: It is not recommended to use the same Security Group for both EC2 and RDS. Separating Security Groups allows for more precise access control and compliance with security best practices.