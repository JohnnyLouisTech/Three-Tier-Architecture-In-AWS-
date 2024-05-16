# Three-Tier-Architecture-In-AWS
# Scenario: A small e-commerce company named Toy-Buzz wants a scalable and reliable e-commerce platform for their toy business and decided to get a 3-tier architecture deployed with the help of an AWS Engineer.

# Architecture:
![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/963b35a1-50a8-4cd5-888e-5ed81b92d08f)

# Objective 1: Create a Web Tier
# VPC
We need to create a VPC first. Login to your AWS account and type VPC into the search box and click Create VPC.

VPC Settings: VPC only.

VPC Name: Toy-Buzz-VPC.

IPv4 CIDER block: IPv4 CIDER manual.

IPv4 CIDR: 10.0.0.0/16.

IPv6 CIDR block: No IPv6 CIDR block.

Tenancy: Default.

Click create VPC.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/244e7bb6-e3b5-44ad-b03c-2cf40f2b4d64)
![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/0ea59253-61a8-49bb-829c-670ad92af42f)

# We need to created an Internet Gateway for our VPC
Name Tag : Toy-Buzz-IGW

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/826a42e9-e30c-4a91-8080-ff26f1156477)
![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/c3e274b4-c093-44ab-9b99-9fcd11d7f975)

Now we need to Attach it to the VPC and click on “Attach Internet Gateway”.
![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/f50f5b74-5ca5-4f2e-af04-31b580f740a2)

Please Select Toy-Buzz-IGW

# Public Subnets
Next, we need to create two Public Subnets for the VPC. Click on Subnets underneath the virtual private cloud section on the left.

Click on create subnet.

VPC ID: Toy-Buzz-VPC.

Subnet Name: Toy-Buzz-Public-Subnet-1

Availability Zone: US East (N. Virginia)/ us-east-1a.

IPv4 VPC CIDR block: 10.0.0.0/16

IPv4 subnet CIDR block: 10.0.1.0/24

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/f2c086f9-fffd-43a1-b9a1-758e027f7ea3)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/f9978444-7e6c-4387-aafa-92d146da897a)

Now we need to create the second public subnet.

Subnet Name: Toy-Buzz-Public-Subnet-2

Availability Zone: US East (N. Virginia)/ us-east-1a.

IPv4 VPC CIDR block: 10.0.0.0/16

IPv4 subnet CIDR block: 10.0.2.0/24

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/73c61db0-48fa-49cb-b9f8-ec4d823f80f1)

Then click “Create Subnet” to create both public subnets. You should now see both subnets available as showing below. 

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/2c8d9776-04d3-4021-b21f-8ce788d51ccf)

# We need to create our Public Route Table
Click on Route tables on the left side underneath Virtual Private Cloud and click on Create route table.

Name: Toy-Buzz-Route-Table.

VPC: Toy-Buzz-VPC.

Click create route table.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/bedfa413-e81d-43f7-9f95-eaa8d5fd99ee)

Now lets connect our subnets we created earlier to the route table.

click on the route table, go to the subnet associations tab and click edit subnet associations.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/d29790b3-93fb-41d3-8640-52c53c7ffc47)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/b5819e83-dafc-4777-9233-d68320639756)

Select both Public subnets and click save associations.

The Public Subnets are successfully attached to the route table.

Click on Routes tab and click on edit routes

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/4c54cd71-4646-41b7-8906-59bbf246aa4e)

Attach the Internet Gateway.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/f58a1b4f-e709-4b9b-b3e5-2aa6d47f530c)

# NAT Gateway
Click on NAT Gateway on the side panel underneath Virtual private cloud.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/dc80aa9e-a632-4806-a58c-0032a419b869)

Click Create NAT Gateway.

Name: Toy-Buzz-Public-NAT-Gateway.

Subnet: Toy-Buzz-Public-Subnet-1.

Connectivity Type: Public.

Elastic IP allocation ID: Click on Allocate Elastic IP to generate it.

click create NAT gateway.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/e40b98ee-dd32-4669-93b8-1aa359017b32)

# AMI/Launch Template
We are going to create a AMI with a bootstrap of Apache 2 included in the user data.

Search AMI in the search bar.

Click AMI Catalog and search for Ubuntu, choose the free tier Ubuntu Server 22.04

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/e9df72bd-4ac0-4fe0-b40d-c6f5d10f83e3)

Click Create AMI with Template.

Name: Toy-Buzz-EC2-AMI.

Template version description: Template for EC2.

Auto Scaling guidance: ✅

Application and OS Images (Amazon Machine Image): Ubuntu.

Instance Type: t2.micro.

Key Pair: Toy-Buzz-KeyPair.

Network Settings:

Subnet: Do not included in launch template.

Create Security Group: ✅

Security Group Name: Toy-Buzzz-SG.

Description: Security Group for Toy-Buzz.

Advanced Details:

1. User Data:

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/6d7790e4-8990-43e3-a80d-b284fd0b02a5)

This is going to install Apache to our EC2 Instances.

Click Create Template.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/6e1b76ed-36b8-4dd4-8d7e-77ee35b66ba5)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/fbb34297-4cdf-4a79-bc18-963832fb0d2e)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/8744b521-9c79-4740-a806-f856ed6082ba)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/72407757-8474-4dff-bb9c-6899dc731c88)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/ecb72abc-5386-4194-ad73-70f62caf99d5)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/bf5be477-5f05-4c69-af9f-c5ba3524c498)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/7686b73a-1022-4736-8de3-e1419e6a66c8)

# Web Security Group
Within our launch template, we specified to create a security group, lets verify it is created.

Type security group in the search bar.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/9cc4c7d6-6f63-4ffe-921b-e3488a92a298)

Click Toy-Buzz-SG ID.

Let’s add inbound permissions, click edit inbound rules.

Add Rules:

HTTPS Port 443.
HTTP Port 80.
SSH Port 22.
Custom TCP Port 8080.
Set them to your IP Address for best practice standards.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/102678c4-fff7-4683-b068-08afc66602a2)

Click save rules.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/b4b85b12-b287-43f6-a00f-72ccdcaf8840)

# Autoscaling Group
We need an Autoscaling Group, type Autoscaling Group in the search bar.

Click create Auto scaling Group.

Auto-scaling group name: Toy-Buzz-ASG.

Launch template: Toy-Buzz-EC2-AMI.

Version: Default (1)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/6ce0861e-21e7-4d18-b79f-e79307bc6f33)

Click next.

VPC: Toy-Buzz-VPC.

Availability Zones and subnets: Toy-Blitz-Subnet-1, Toy-Buzz-Subnet-2.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/71f61a25-f903-4111-ab83-0ee39b4c3704)

Skip Load Balancer.

Desire Capacity: 2

Min. Desire Capacity: 2.

Max Desired Capacity: 5

Automatic scaling: No scaling policies.

Instance maintenance policy: No policy.

Click next.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/385f9b57-8fd0-4d94-a9b7-f130304d3a9a)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/18f1fcb0-f562-4121-a7da-d7f1e64632b1)


Skip Notifications & Tags.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/6c9b0f15-0318-4936-9f15-d799c4303960)

Click create Auto Scaling Group.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/57e51e42-4e52-4494-9589-fe9dd3fda1a9)

Lets verify our EC2’s were created.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/6feb419a-feef-4345-887a-59c2f24ba66d)


# Objective 2: Create a Application Tier
# Private Subnets
VPC ID: Toy-Buzz-VPC.

Subnet Name: Toy-Buzz-App-Private-Subnet-1

Availability Zone: US East (N. Virginia)/ us-east-1a.

IPv4 VPC CIDR block: 10.0.0.0/16

IPv4 subnet CIDR block: 10.0.160.0/24

VPC ID: Toy-Buzz-VPC.

Subnet Name: Toy-Buzz-App-Private-Subnet-2

Availability Zone: US East (N. Virginia)/ us-east-1a.

IPv4 VPC CIDR block: 10.0.0.0/16

IPv4 subnet CIDR block: 10.0.128.0/24

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/70d67042-d884-4bb8-91e4-4047a58291ad)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/a05c8175-e028-47dd-a720-3311786a0f67)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/88daa9a5-75f8-44a3-b7ab-af181658d27f)


# Private Route Table
Name: Toy-Buzz-App-Private-Route-Table

VPC: Toy-Buzz-VPC

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/36089ce3-b030-47e2-87ad-81705e9ff77b)

Click create route table.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/b80f0fef-0d2f-448b-b183-4cda3089b4fb)

Associate your Private Subnets to the Private Route Table.

In Route Table, select Toy-Buzz-App-Private-Route-Table and select subnet associations tab then click on edit subnet associations under explicit associations.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/fdf5dc6a-9615-4baf-b01c-c6240f68cf79)

Associate your Private Subnets to the Private Route Table.

In Route Table, select Toy-Buzz-App-Private-Route-Table and select subnet associations tab then click on edit subnet associations under explicit associations.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/0ab6c5de-eafc-49e7-8091-6a7e2328f449)


Go to the Toy-Buzz-App-Private-Route-Table and click on routes and edit routes.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/0499c44c-6392-4492-804f-f4834be50825)

Attach the NAT Gateway.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/5c6c60f9-e007-414b-b44e-cfdb59a68d5b)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/3443a744-0bfe-45fd-b2ec-f5385101ea5f)

# AMI/Launch Template
Create another launch template for your Application tier.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/5dbbf9f8-a2db-4ea4-b249-49cfb73e6bd3)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/a4a43534-a992-4cbc-877d-995fc074e0b8)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/808226b2-6ec7-429c-af84-0ed67b620e81)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/56519d7a-d316-4c91-9732-c3d0df4d27de)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/029c1843-a15c-406e-b1c2-6eabbd4b12c3)


Click create launch template.

# Auto-scaling Group
Complete the steps to create a Autoscaling group.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/8b2770a9-b2ef-4511-953c-46c72fdb5ef8)

# Security Group

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/dbe62a36-3dcc-4fa6-87b3-68d7a912f93d)

# Objective 3: Create a Database Tier
# Private Subnets
VPC ID: Toy-Buzz-VPC.

Subnet Name: Toy-Blitz-DB-Private-Subnet-1

Availability Zone: US East (N. Virginia)/ us-east-1a.

IPv4 VPC CIDR block: 10.0.0.0/16

IPv4 subnet CIDR block: 10.0.96.0/24

VPC ID: Toy-Buzz-VPC.

Subnet Name: Toy-Buzz-DB-Private-Subnet-2

Availability Zone: US East (N. Virginia)/ us-east-1a.

IPv4 VPC CIDR block: 10.0.0.0/16

IPv4 subnet CIDR block: 10.0.64.0/24


![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/a00e7ddc-379e-4a40-a44f-0953cef7a1b1)


![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/befd7da0-bf26-4fb8-a9ff-e05be81375e7)


![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/4f47d011-d95c-46c9-8d93-b28f3fbe7a3f)

# Private Route Table
Name: Toy-Buzz-DB-Private-Route-Table

VPC: Toy-Buzz-VPC

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/6bcb9b12-f91e-488d-860a-41845142ab41)

Associate your Private Subnets to the Private Route Table.

In Route Table, select Toy-Buzz-DB-Private-Route-Table and select subnet associations tab then click on edit subnet associations under explicit associations.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/7d5c9182-3315-468e-b5e6-0dfe49592116)

Select Toy-Buzz-DB-Private-Subnet1 & Toy-Buzz-DB-Private-Subnet2.

Click save association.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/de060dba-7a9a-4293-8dd4-bd95025b5f65)

# Database Security Group
Create a Database Security Group and allow port 3306 inbound for MySQL.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/a111b08b-5cba-4a1f-b60e-8de149aabf9e)


# MySQL DatabaseType RDS
Click create database.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/abe1934d-d43d-4a0d-b71b-88fc888c413f)

Standard create.
MySQL.
Free Tier.
DB instance identifier: database-1.

Master username: admin.

Self-managed.

Master password: 12345678 (For demonstration purposes only you would created a more secure password in production.)

Instance configuration: db.t3.micro.

Storage: General Purpose SSD, 20 GIB.

Connectivity:

Do not connect to an EC2 compute resource.
VPC: Toy-Buzz-VPC.
Public Access: No
Existing VPC security groups: Toy-Buzz-SG
Availability Zone: us-east-1a
Create Database.

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/a3363e7e-5e19-4dbc-984c-16177b8f62d9)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/db65988b-3aa7-4bd1-a5b7-2aeded383550)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/488deb73-3c53-41a8-b07d-0244964ad143)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/807dad1c-f339-47a5-97f5-c1bb09ff727a)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/9c1f4b5f-c431-442e-963d-462735514b46)

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/28564a68-3b8e-44b2-9d01-5235d826a875)

The database tier is successfully created.

Lets verify.

Apache:

![image](https://github.com/JohnnyLouisTech/Three-Tier-Architecture-In-AWS-/assets/29494723/432901eb-73b8-4922-bf17-5ba0f4d1a923)

We did it! Well Done!

# References:
https://docs.aws.amazon.com/











