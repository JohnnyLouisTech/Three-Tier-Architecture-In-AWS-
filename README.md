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



