![Alt text](/Host_a_Static_Website_on_AWS.png)
---

# Host a Static Website on AWS

This project demonstrates how to host a static HTML web application on AWS using various AWS services. The project leverages a combination of networking, security, and compute resources to ensure high availability, security, and scalability.

## Architecture Overview

The project architecture includes the following components:

1. **Virtual Private Cloud (VPC):**
   - Configured with both public and private subnets across two different availability zones.
   - Enhanced reliability and fault tolerance by utilizing multiple availability zones.

2. **Internet Gateway:**
   - Facilitates connectivity between VPC instances and the wider Internet.

3. **Security Groups:**
   - Act as a network firewall mechanism to control inbound and outbound traffic.

4. **Public Subnets:**
   - Used for infrastructure components like the NAT Gateway and Application Load Balancer.

5. **Private Subnets:**
   - Web servers (EC2 instances) are positioned within private subnets for enhanced security.
   - Instances in private subnets access the Internet via the NAT Gateway.

6. **EC2 Instance Connect Endpoint:**
   - Provides secure connections to assets within both public and private subnets.

7. **Application Load Balancer:**
   - Distributes web traffic evenly to an Auto Scaling Group of EC2 instances across multiple availability zones.

8. **Auto Scaling Group:**
   - Automatically manages EC2 instances, ensuring website availability, scalability, fault tolerance, and elasticity.

9. **Simple Notification Service (SNS):**
   - Alerts about activities within the Auto Scaling Group.

10. **Route 53:**
    - Used to register the domain name and set up a DNS record.

11. **Certificate Manager:**
    - Secures application communications.

## Prerequisites

Before you begin, ensure you have the following:

- An AWS account with the necessary permissions to create VPCs, subnets, EC2 instances, security groups, and other resources.
- A registered domain name.

## Deployment Steps

Follow these steps to deploy the web application:

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
   ```

2. **Navigate to the Project Directory:**
   ```bash
   cd host-a-static-website-on-aws
   ```

3. **Run the Deployment Script:**
   ```bash
   ./deploy.sh
   ```

## Deployment Script

The following bash script is used to deploy the static website on an EC2 instance:

```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su
# Update all installed packages to their latest versions
yum update -y
# Install Apache HTTP Server
yum install -y httpd
# Change the current working directory to the Apache web root
cd /var/www/html
# Install Git
yum install git -y
# Clone the project GitHub repository to the current directory
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/
# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws
# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd
# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

## AWS Services Utilized

- **VPC (Virtual Private Cloud):** Custom network configuration.
- **EC2 (Elastic Compute Cloud):** Virtual servers for hosting the application.
- **Internet Gateway:** Enables internet access for the VPC.
- **Security Groups:** Firewall rules to control traffic.
- **NAT Gateway:** Provides internet access to instances in private subnets.
- **Application Load Balancer:** Distributes incoming traffic.
- **Auto Scaling Group:** Manages EC2 instances automatically.
- **SNS (Simple Notification Service):** Sends alerts.
- **Route 53:** DNS and domain registration service.
- **Certificate Manager:** Manages SSL/TLS certificates.

## Contributing

Contributions are welcome! Please fork the repository and create a pull request with your changes.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

