---
title : "Create a VPC"
date: 2025-07-01
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

#### Creating a VPC and Network Resources
**Information** : Amazon Virtual Private Cloud (VPC) lets you launch AWS resources in a defined virtual network. This environment provides complete control over network configuration, including IP address ranges, subnets, routing tables, and gateways.

1. Create a VPC using the AWS Management Console
Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

2. In the VPC console, select Create VPC.

3. In the Resources to create section, select VPC and more to create a VPC along with its associated resources.

4. Configure basic options:

- Leave the Name tag auto-generation option selected to automatically generate labels for resources, or uncheck it to create your own.

- Enter the IPv4 CIDR address range for the VPC (required).

- (Optional) To support IPv6, select IPv6 CIDR block, Amazon-provided IPv6 CIDR block.

- Select the Tenancy option that best suits your needs.

5. Configure Availability Zones (AZs):

- For Number of Availability Zones, select at least two AZs for production environments.

- To specify specific AZs, expand Customize AZs.

6. Configure subnets:

- Select the number of public and private subnets required.

- To customize the CIDR range for subnets, expand Customize subnets CIDR blocks.

7. Configure Internet Connections:

- For NAT gateways, select the number of AZs to deploy NAT gateways.

- For IPv6 connectivity, select Egress only internet gateway if needed.

8. (Optional) To access Amazon S3 directly from VPC, select VPC endpoints, S3 Gateway.

9. For DNS options, both domain name resolution options are enabled by default. Adjust as needed.

10. (Optional) Add labels to the VPC by expanding Additional tags.

11. Preview the VPC structure in the Preview panel:

- Solid lines show the relationships between resources.

- Dashed lines show network traffic flows.

- When the configuration is complete, select Create VPC.

#### Configure public IPv4 address for subnet
ℹ️ **Information**: By default, non-default subnets have the auto-assign public IPv4 address property set to “false”, while default subnets have this property set to “true”. Non-default subnets created through EC2 instance creator will have this property set to “true”.

**To change the public IPv4 address settings of a subnet:**

1. Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

2. In the navigation pane, select **Subnets**.

3. Select the subnet to configure, then select Actions, Edit subnet settings.

4. Check or uncheck the Enable auto-assign public IPv4 address option as needed, then select Save.