# Secure 3-Tier Web Application on AWS

## Project Overview

This project demonstrates the design and deployment of a secure and highly available 3-tier web application on Amazon Web Services (AWS).

The architecture separates the application into three layers:

1. Presentation Layer – Application Load Balancer
2. Application Layer – EC2 instances in private subnets
3. Database Layer – Amazon RDS MySQL in private subnets

## Architecture

Internet
   |
   v
Application Load Balancer
   |
   +-------------------+
   |                   |
   v                   v
Private EC2         Private EC2
App Server 1        App Server 2
   |                   |
   +---------+---------+
             |
             v
       Amazon RDS MySQL

## AWS Services Used

- Amazon VPC
- Amazon EC2
- Application Load Balancer
- EC2 Auto Scaling
- Amazon RDS MySQL
- Internet Gateway
- NAT Gateway
- IAM
- Amazon CloudWatch
- Amazon SNS
- Security Groups
- Amazon S3
- Ubuntu Linux
- Nginx

## Network Architecture

### VPC

- VPC CIDR: `10.10.0.0/16`

### Public Subnets

- `10.10.1.0/24`
- `10.10.2.0/24`

Used for the Application Load Balancer and NAT Gateway.

### Private Application Subnets

- `10.10.3.0/24`
- `10.10.4.0/24`

Used for the EC2 application servers.

### Private Database Subnets

- `10.10.5.0/24`
- `10.10.6.0/24`

Used for Amazon RDS MySQL.

## Security

Security groups were configured to control communication between the different layers.

### Internet → ALB

HTTP traffic is allowed on port 80.

### ALB → Application Servers

Application servers accept HTTP traffic only from the ALB security group.

### Application Servers → RDS

RDS MySQL accepts traffic only from the application server security group on port 3306.

The RDS database is configured with public access disabled.

## High Availability

The application servers are distributed across two Availability Zones.

An Application Load Balancer distributes incoming requests between the application servers.

An Auto Scaling Group maintains the required number of application instances.

## Application Server

The application servers run:

- Ubuntu Linux
- Nginx

The servers are deployed in private subnets and do not have public IP addresses.

## Testing

The application was successfully accessed through the Application Load Balancer DNS name.

Traffic flow:

Internet → ALB → Private EC2 → RDS

## Key Concepts Demonstrated

- VPC networking
- Public and private subnet design
- Route tables
- Internet Gateway
- NAT Gateway
- Security groups
- Load balancing
- Auto Scaling
- Private EC2 deployment
- RDS database security
- Linux server administration
- Nginx configuration
- Cloud monitoring

## Author

**Sapparam Mounish Reddy**

B.Tech Computer Science and Engineering  
Madanapalle Institute of Technology & Sciences  
Expected Graduation: 2027
