---
title : "Cleaning Up Resources"
date: 2025-07-01
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

### Clean Up AWS Resources
ℹ️ **Information**: After completing the lab, cleaning up AWS resources is an important step to avoid unexpected costs. Follow the steps below to delete all created resources.

1. ##### Delete RDS Database and Snapshots
###### Delete DB Instance:
-
- Go to RDS Management Console
- In the left navigation bar, select Databases
- Select all DB Instances related to the lab
- Click Actions, then select Delete
- Uncheck Create final snapshot? and select the confirmation box I acknowledge that upon instance deletion, automated backups, including system snapshots and point-in-time recovery, will no longer be available

- Type delete me in the confirmation box

- Click Delete
⚠️ Warning: Deleting a DB Instance cannot be undone. Make sure you have backed up important data before performing this step.

###### Delete DB Snapshots:

-
- Go to RDS Management Console

- In the left navigation bar, select Snapshots

- Select all snapshots related to the lab

- Click Actions

- Select Delete snapshot

- Click Delete to confirm
###### Delete DB Subnet Group:

-
- Open Amazon RDS Console

- In the left navigation bar, select Subnet groups

- Select the DB subnet group related to the lab

- Click Delete, then select Delete in the confirmation window
2. ##### Terminate EC2 Instances

1. Go to EC2 Management Console

2. In the left navigation bar, select Instances

3. Select all EC2 Instances related to the lab

4. Click Actions

5. Select Instance state, then select Terminate instance

6. Click Terminate to confirm

💡 Pro Tip: Before terminating an instance, make sure you have backed up all important data from the instance, as the data on the instance will be permanently deleted.

3. ##### Release Elastic IP Addresses

1. Open the Amazon EC2 Console

2. Select EC2 Dashboard, then select Elastic IPs

3. Select the Elastic IP address associated with the lab

4. From the Actions menu, select Release Elastic IP addresses

5. On the confirmation page, click Release

🔒 Security Note: Releasing Elastic IPs prevents incurring charges for unused IP addresses. AWS charges for Elastic IPs that are not associated with a running instance.

4. ##### Delete VPC and associated resources
###### Delete Security Groups:
-
- Open Amazon VPC Console
- Select Security Groups from the left navigation bar
- Select the security group associated with the lab
- Click Actions, select Delete security groups
- Click Delete to confirm
###### Delete NAT Gateway:
-
- Open Amazon VPC Console
- Select NAT Gateways from the left navigation bar
- Select the NAT Gateway associated with the lab
- Click Actions, select Delete NAT gateway
- Confirm the deletion and click Delete
ℹ️ Information: Deleting a NAT Gateway does not automatically release the Elastic IP associated with it. Make sure you released the Elastic IP in the previous step.

###### Delete a VPC:

-
- Open the Amazon VPC Console

- Select Your VPCs from the left navigation bar

- Select the VPC you want to delete

- From the Actions menu, select Delete VPC

- On the confirmation page, type delete, then click Delete
💡 Pro Tip: When you delete a VPC, AWS automatically deletes related resources such as subnets, route tables, and internet gateways. However, some resources such as security groups, NAT gateways, and DB subnet groups need to be manually deleted first.