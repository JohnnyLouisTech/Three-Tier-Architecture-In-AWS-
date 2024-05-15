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



