---
title : "Create EC2 instance"
date: 2025-07-01
weight : 3
chapter : false
pre : " <b> 3. </b> "
---
## Create Amazon EC2 Instance
ℹ️ **Information**: Amazon Elastic Compute Cloud (EC2) provides scalable computing in the AWS cloud. Using EC2 allows you to deploy virtual servers without investing in physical hardware, helping you develop and deploy applications faster.

#### Steps to create EC2 Instance
1. Access AWS Management Console

- Open a browser and access the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

2. Initialize EC2 Instance

- On the EC2 console dashboard screen, in the Launch instance box, select Launch instance, and then select Launch instance from the options that appear.

3. Name the instance

- Under Name and tags, for Name, enter a descriptive name for your instance.

4. Select Amazon Machine Image (AMI)

- Under Application and OS Images (Amazon Machine Image), follow these steps:

- Select Quick Start, then select Amazon Linux.

- From Amazon Machine Image (AMI), select an Amazon Linux 2023 HVM instance.

5. Select the instance type

- Under Instance type, select the t2.micro or t3.micro instance type (in regions where t2.micro is not available).

ℹ️ **Information**: The t2.micro and t3.micro instance types are eligible for use in the AWS Free Tier, suitable for low-resource applications or development environments.

6. Configure the key pair

- Under **Key pair (login)**, select the key pair you created earlier.

7. Configure Security Group

- Next to Network settings, select Edit.

- Select Select existing security group.

- From Common security groups, select the security group you created earlier.

🔒 **Security Note**: Security Groups act as virtual firewalls, controlling network traffic to and from the EC2 instance. Make sure to open only the necessary ports to minimize the attack surface.

8. Confirm and initialize the instance

- Review the instance configuration in the Summary panel.

- When ready, select Launch instance.

9. Confirm and check status

- After receiving the confirmation message, select View all instances to return to the console.

- Monitor the instance initialization status. Initially, the status will be pending and then change to running when the instance is ready.

- Wait until the instance passes the Status check before attempting to connect.

#### Connect to EC2 Instance via SSH using MobaXterm
ℹ️ **Information**: MobaXterm is a multi-purpose application for Windows that provides many networking tools in a single interface, including SSH client, SFTP, X11 server and many more features.

1. Download and install MobaXterm

- Download MobaXterm from the official website: MobaXterm Website.
- Install the application according to the instructions.

2. Create a new SSH session

- Start MobaXterm.

- Click the Session icon in the upper left corner.

3. Configure SSH connection

- In the configuration window, fill in the following information:

- Remote Host: Public IP address or public DNS of the EC2 instance.

- Port: 22 (default SSH port).

- User: Default username (usually ec2-user for Amazon Linux).
- Advanced SSH settings: Select this tab to provide the path to the private key file.

🔒 Security Note: Make sure your private key file (.pem) has restricted access (readable only by the current user) for added security.

4. Connect to EC2 Instance

- Click OK to save the configuration and start the SSH session.

- If this is your first time connecting, you may receive a warning about an unknown host key. Select Yes to continue.

5. Confirm successful connection

- Once successfully connected, you will see the EC2 instance terminal and can start executing commands.