---
title : "Create DB Subnet Group"
date: 2025-07-01
weight : 4
chapter : false
pre : " <b> 2.4 </b> "
---
## Create DB Subnet Group
#### Create DB Subnet Group
ℹ️ **Information**: DB Subnet Group is a collection of subnets in your VPC that are assigned to your RDS database. DB Subnet Group allows Amazon RDS to deploy database instances in multiple Availability Zones to ensure high availability and fault tolerance.

##### Steps to create DB Subnet Group
1. Log in to AWS Management Console.

2. In the service menu, find and select **Amazon RDS**.

3. In the left navigation bar, select **Subnet groups**.

4. Click the **Create DB Subnet Group** button.

5. In the Create DB Subnet Group interface, enter the basic information:

- **Name**: Enter a descriptive name for the DB Subnet Group

- **Description**: Add a detailed description of the purpose of the DB Subnet Group

- **VPC**: Select the VPC where you will deploy the RDS database

6. In the **Add subnets** section:

- Select the **Availability Zones** (AZs) where you want to deploy the database
- Select the corresponding **Subnets** in each selected AZ
⚠️ Warning: To deploy Multi-AZ, you need to select at least two subnets in different Availability Zones. This ensures high fault tolerance for your RDS database.

7. After completing the configuration, click the Create button to create the DB Subnet Group.