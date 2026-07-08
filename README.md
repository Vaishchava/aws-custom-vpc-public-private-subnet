# AWS Custom VPC with Public & Private Subnets

## Project Overview

This project demonstrates how to build a production-style AWS networking environment using a custom Virtual Private Cloud (VPC).

Instead of using the default VPC, I created my own network architecture with public and private subnets, custom route tables, an Internet Gateway, a NAT Gateway, and EC2 instances deployed in both subnets.

This project helped me understand how AWS networking works internally and how production environments are designed.

---

## Architecture

```
                    Internet
                        │
                Internet Gateway
                        │
                Public Route Table
                        │
         ┌─────────────────────────┐
         │                         │
 Public EC2 Instance         NAT Gateway
    (Public IP)                   │
         │                        │
         └──────────────┬─────────┘
                        │
               Private Route Table
                        │
              Private EC2 Instance
               (No Public IP)
```

---

## AWS Services Used

- Amazon VPC
- EC2
- Internet Gateway
- NAT Gateway
- Route Tables
- Public Subnet
- Private Subnet
- Security Groups
- Network ACL
- Elastic IP

---

## Network Design

### VPC

| Property | Value |
|----------|--------|
| CIDR | 10.0.0.0/24 |

---

### Public Subnet

| Property | Value |
|----------|--------|
| CIDR | 10.0.0.0/25 |
| Route | Internet Gateway |
| Public IP | Enabled |

Purpose

- Web Servers
- Bastion Host
- Internet-facing Applications

---

### Private Subnet

| Property | Value |
|----------|--------|
| CIDR | 10.0.0.128/25 |
| Route | NAT Gateway |
| Public IP | Disabled |

Purpose

- Application Servers
- Databases
- Internal Services

---

## Route Tables

### Public Route Table

| Destination | Target |
|-------------|---------|
| 10.0.0.0/24 | local |
| 0.0.0.0/0 | Internet Gateway |

---

### Private Route Table

| Destination | Target |
|-------------|---------|
| 10.0.0.0/24 | local |
| 0.0.0.0/0 | NAT Gateway |

---

## Internet Gateway

Used to provide internet access to resources in the public subnet.

---

## NAT Gateway

Allows EC2 instances inside the private subnet to access the internet for updates and package installation without exposing them to inbound internet traffic.

---

## EC2 Deployment

### Public EC2

- Public IP Enabled
- SSH Access
- Internet Access

### Private EC2

- No Public IP
- Internet Access via NAT Gateway
- No Direct Internet Access

---

## Security

- Separate Public and Private Subnets
- Custom Route Tables
- Internet Gateway only for Public Subnet
- NAT Gateway for Private Subnet
- Security Groups configured separately

---

## Learning Outcomes

- AWS Networking Fundamentals
- CIDR Planning
- Public vs Private Subnets
- Internet Gateway
- NAT Gateway
- Route Tables
- VPC Design
- EC2 Networking
- Secure Network Architecture

---

## Screenshots

- Custom VPC
- Public Subnet
- Private Subnet
- Route Tables
- Internet Gateway
- NAT Gateway
- Public EC2
- Private EC2

---

## Future Improvements

- Deploy Nginx on Public EC2
- Deploy Flask Application
- Add Application Load Balancer
- Launch RDS in Private Subnet
- Provision Infrastructure using Terraform
