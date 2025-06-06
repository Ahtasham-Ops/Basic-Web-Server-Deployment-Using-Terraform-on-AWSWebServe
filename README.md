# Basic-Web-Server-Deployment-Using-Terraform-on-AWSWebServe
1.  **Introduction:** This document describes the setup of a minimal AWS infrastructure using Terraform. It was developed for proof-of-concept purposes to understand basic infrastructure automation and provisioning using Infrastructure as Code (IaC).
    
2.  **Objective:**  Provision a minimal AWS infrastructure using Terraform to deploy a public Ubuntu EC2 instance running an Nginx web server accessible via a custom domain or public IP. The main goals of this project are:
    

*   To provision a basic cloud infrastructure on AWS using Terraform
    
*   To deploy an EC2 instance running Nginx configured with a custom virtual host
    
*   To understand the differences between simplified and production-ready infrastructure
    
*   To use variables and outputs to make the Terraform code modular and reusable
    

3.  **Infrastructure Overview:** The Terraform configuration provisions the following AWS resources:
    

*   IAM User for Restricted Access
    
*   A VPC with a defined CIDR block
    
*   A public subnet with auto-assign public IP
    
*   An internet gateway attached to the VPC
    
*   A route table associated with the public subnet
    
*   A security group that allows SSH, HTTP, and HTTPS access
    
*   An EC2 instance (Ubuntu 22.04) with Nginx installed and configured
    
*   A simple custom Nginx virtual host pointing to a custom directory
    

4.  **Terraform Implementation:**
    

Following Terraform files created:

main.tf: Defines all infrastructure resources

variables.tf: Holds input variables for customization

outputs.tf: Outputs useful values like instance IP

User data is used to automate the installation and configuration of Nginx with a custom domain \`test.eagle.com\` using a virtual host file.

1.  **Simplifications vs. Production Standards**
    

This setup was intentionally simplified to reduce cost and complexity. Below are comparisons:

**Simplified Setup:**
---------------------

*   No private subnets or NAT gateways
    
*   No Load Balancer or Auto Scaling Group
    
*   Security group allows open 0.0.0.0/0 access for demo purposes
    
*   EC2 instance is configured using user\_data with a basic bash script
    
*   Custom domain resolved via /etc/hosts only (not public DNS)
    
*   No SSL/TLS setup
    

**In Production:**
------------------

*   Use of private subnets for backend services and NAT gateway for outbound access
    
*   Integration with Route 53 for DNS
    
*   Proper ACM-issued SSL certificates and HTTPS enforced
    
*   Secure, least-privilege security group rules (Allow HTTP/HTTPS access from Reverse Proxy and only Office Ips access to SSH) 
    
*   Load balancer with auto-scaling groups
    
*   Infrastructure modularized into reusable Terraform modules
    

5.   **Future Improvements**
    

*   Use Route 53 to map a domain to the instance public IP/or AWS ALB
    
*   Add TLS with self-signed certs or ACM for HTTPS support
    
*   Use Terraform modules for better structure
    
*   Introduce Load Balancer and Auto Scaling Group
    
*   Deploy multiple instances in multiple AZs
    
*   Use S3 backend for storing Terraform state securely
