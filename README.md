# Hands-On-Lab-Build-a-VPC-with-AWS

the steps to create and configure a Virtual Private Cloud (VPC) on AWS with public and private subnets, including route tables and an Internet Gateway (IGW). This can be used as a reference for networking basics in AWS.
# AWS VPC Setup Guide

---


The goal is to set up a VPC with the following configuration:
- **VPC**: `10.0.0.0/16`
- **Public Subnet**: `10.0.1.0/24` (Availability Zone: `eu-west-2a`)
- **Internet Gateway**: Attached to enable public internet access.
- **Route Table**: Configured to route internet traffic via the IGW.
- **EC2 Instance**: Launched in the public subnet to test connectivity.

---

## **Steps**

### 1. **Create a VPC**
   - **Why?** A VPC is your private network in AWS, where all resources will reside.
   - Navigate to the VPC dashboard.
   - Create a new VPC with the following details:
     - **Name**: `my-vpc`
     - **CIDR Block**: `10.0.0.0/16`

---

### 2. **Create a Public Subnet**
   - **Why?** Subnets divide your VPC into smaller, manageable network segments. A public subnet allows resources to connect to the internet.
   - Go to **Subnets** and create a new subnet:
     - **VPC**: `my-vpc`
     - **Name**: `public-subnet`
     - **Availability Zone**: `eu-west-2a`
     - **CIDR Block**: `10.0.1.0/24`

---

### 3. **Attach an Internet Gateway (IGW)**
   - **Why?** An IGW provides internet access for resources in your public subnet.
   - Go to **Internet Gateways** and create an IGW:
     - **Name**: `my-igw`
   - Attach the IGW to the VPC (`my-vpc`).

---

### 4. **Update Route Table for Public Subnet**
   - **Why?** Route tables define how traffic flows within your network. Adding a route to the IGW enables internet connectivity.
   - Go to **Route Tables** and:
     1. Find the route table associated with your VPC (`my-vpc`).
     2. Add a route:
        - **Destination**: `0.0.0.0/0` (all traffic)
        - **Target**: `my-igw`
     3. Associate the route table with the `public-subnet`.

---

### 5. **Launch an EC2 Instance in the Public Subnet**
   - **Why?** EC2 instances are virtual servers. Launching one in the public subnet allows you to test your setup.
   - Go to **EC2** and launch an instance:
     - **AMI**: Amazon Linux 2 (Free Tier Eligible)
     - **Instance Type**: `t2.micro`
     - **Network**: `my-vpc`
     - **Subnet**: `public-subnet`
     - **Auto-assign Public IP**: Enabled
     - **Key Pair**: Create or use an existing one for SSH access.

---

### 6. **Test SSH Connectivity**
   - **Why?** Testing ensures your configuration works and the EC2 instance can communicate with the internet.
   - Find the public IP of your EC2 instance from the EC2 dashboard.
   - Use the following SSH command to connect:
     ```bash
     ssh -i <KEY_FILE>.pem ec2-user@<PUBLIC_IP>
     ```
   - Accept the SSH fingerprint and verify the connection.

---

Feel free to clone and modify this guide for your own AWS projects!
