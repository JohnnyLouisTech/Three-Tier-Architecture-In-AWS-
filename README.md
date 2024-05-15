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
