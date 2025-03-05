# Bank-ARC


creating Banking Architechture using only AWS services 



Step 1: Set Up Networking (VPC & Subnets)
Go to VPC Service → Create a New VPC

Name: Banking-VPC
IPv4 CIDR: 10.0.0.0/16
Enable DNS resolution
Create Subnets (Inside the VPC)

Public Subnet: 10.0.1.0/24 (For Web & App Servers)
Private Subnet: 10.0.2.0/24 (For Databases)
Internet Gateway (Attach it to Banking-VPC)

Route 0.0.0.0/0 → Internet Gateway (for Public Subnet)
NAT Gateway (For Private Subnet to Access the Internet)

Create a NAT Gateway in Public Subnet
Route 0.0.0.0/0 → NAT Gateway (for Private Subnet)
📌 Step 2: Launch EC2 Instances
Go to EC2 → Launch Instance

Web Server: t3.micro, OS: Amazon Linux 2
App Server: t3.micro, OS: Amazon Linux 2
Database Server: t3.medium, OS: Amazon Linux 2
Security Groups for EC2

Web Server SG: Allow 80 (HTTP), 443 (HTTPS) from anywhere
App Server SG: Allow traffic only from Web Server SG
DB Server SG: Allow traffic only from App Server SG
📌 Step 3: Configure Database (RDS)
Go to RDS → Create Database
Engine: PostgreSQL (or MySQL)
Instance Class: db.t3.medium
Subnet Group: Use the Private Subnet
Security Group: Allow traffic only from App Server SG
📌 Step 4: Set Up Load Balancer
Go to EC2 → Load Balancers → Create ALB
Type: Application Load Balancer (ALB)
Target: Web Server Instances
Attach the ALB to the Public Subnet
Configure Security Group to allow traffic on 80, 443
📌 Step 5: Configure Storage
Amazon S3 for Logs & Backups

Create an S3 bucket (banking-app-logs)
Enable Server-Side Encryption
EBS for Persistent Storage

Attach additional EBS volumes for databases
📌 Step 6: Enable Monitoring & Security
CloudWatch

Enable EC2 Monitoring
Set up Custom Dashboards & Alarms
CloudTrail

Enable Logging for AWS API Calls
