🌐 AWS Infrastructure: Web Server Deployment
Project: Nautilus Application Phase 1
1. Executive Summary
The nautilus-ec2 instance was successfully provisioned to serve as a high-availability web server. The deployment utilized a "Stateless Provisioning" approach, where the Nginx software stack was automatically installed and configured during the initial boot cycle using a custom User Data script.

2. Instance Specifications
Resource,Value
Instance Name,nautilus-ec2
Instance ID,i-0cdd280a4e3558987
Public IP,52.23.165.47
AMI ID,ami-053b0d53c279acc90 (Ubuntu 22.04 LTS)
Instance Type,t2.micro

3. Network & Security Configuration
A dedicated Security Group was created to balance accessibility with security, ensuring the web server is reachable via standard HTTP protocols.

Security Group Name: nautilus-http-sg

Inbound Rules:

Port 80 (HTTP): Allowed from 0.0.0.0/0 (Internet)

Outbound Rules:

All Traffic: Allowed (Standard default)

4. Automation & User Data
The Nginx web server was bootstrapped using a Bash script passed to the EC2 User-Data field. This ensures that the server is "Ready-for-Production" the moment it reaches a running state.

Provisioning Script (install_nginx.sh):
#!/bin/bash
apt-get update -y
apt-get install -y nginx
systemctl start nginx
systemctl enable nginx

5. Verification Log
Final validation confirmed the following:

Tagging: Name key nautilus-ec2 applied.

Firewall: Port 80 successfully authorized.

Connectivity: Public IP 52.23.165.47 responding to HTTP requests.