![Alt text](/Host-a-Static-Website-on-AWS(2).png)

---

# Host a Static Website on AWS

This project demonstrates how to host a static HTML web application on AWS using a secure, highly available, and fault-tolerant architecture. The infrastructure and deployment scripts are provided in this repository.

## 📌 Project Overview

The web app is deployed on **Amazon EC2 instances** inside a well-architected **Virtual Private Cloud (VPC)**. Traffic is balanced using an **Application Load Balancer** and managed by an **Auto Scaling Group** for scalability and reliability.

## ✅ Key Features

* **VPC Configuration**

  * Public and private subnets across two Availability Zones.
  * Internet Gateway for secure Internet connectivity.
  * NAT Gateway for outbound Internet access from private subnets.
  * EC2 Instance Connect Endpoint for secure connections.

* **Security**

  * Security Groups configured as firewalls.
  * Web servers hosted in private subnets for improved security.
  * SSL/TLS managed via AWS Certificate Manager.

* **Scalability & High Availability**

  * Auto Scaling Group distributes traffic across multiple Availability Zones.
  * Application Load Balancer with a target group for balanced web traffic.
  * SNS notifications for Auto Scaling Group activities.

* **DNS Management**

  * Domain name registered and managed via Route 53.

* **Version Control**

  * Website source files hosted on GitHub for easy collaboration and version tracking.

## 📂 Architecture Diagram

A detailed architecture diagram is included in the repository for reference.

## 🚀 Deployment

Below is the user-data script used to configure the EC2 instances automatically:

```bash
#!/bin/bash
# Switch to the root user
sudo su

# Update installed packages
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change to the web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project repository
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git

# Copy project files to the web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository directory
rm -rf host-a-static-website-on-aws

# Enable and start Apache
systemctl enable httpd
systemctl start httpd
```

> **Note:** Replace the repository URL with your actual repository link if different.

## 🔒 Security Best Practices

* Web servers are hosted in private subnets.
* Secure connections are enabled via EC2 Instance Connect Endpoint.
* SSL/TLS certificates are managed through AWS Certificate Manager.

## 📢 Notifications

Simple Notification Service (SNS) is configured to send alerts for Auto Scaling events to ensure you stay informed about the health and performance of your web servers.

## 🌐 DNS

Domain registration and DNS management are handled via **Amazon Route 53**, providing robust and reliable domain resolution.

## 📎 Repository Contents

* `architecture-diagram.png` — Reference architecture diagram.
* `user-data.sh` — EC2 user-data script for automatic server configuration.
* Website source files — Static HTML content to be served.

## 📖 How to Use

1. Clone this repository.
2. Use the provided user-data script when launching your EC2 instances.
3. Ensure your VPC, subnets, security groups, load balancer, Auto Scaling Group, NAT Gateway, and Route 53 records are configured as described.
4. Access your website using your registered domain name.

## 📫 Contact

For questions, feel free to open an issue or reach out via [GitHub](https://github.com/aosnotes77).

---



