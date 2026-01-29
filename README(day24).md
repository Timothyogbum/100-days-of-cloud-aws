Here is the comprehensive, professional README and the final Git synchronization steps to close out the Nautilus ALB deployment. This documentation is designed to serve as a hand-off for the application team.

🌐 AWS Infrastructure: Application Load Balancer
Project: Nautilus Web Application Front-End
1. Executive Summary
Successfully implemented a highly available entry point for the Nautilus application using an Application Load Balancer (ALB). The architecture decouples the public-facing entry point from the backend compute, enhancing security by ensuring the nautilus-ec2 instance is not directly exposed to the open internet.

2. Technical Architecture
The traffic flow is configured as follows:

Ingress: Internet traffic arrives at nautilus-alb on TCP Port 80.

Listener: A rule-based listener forwards traffic to nautilus-tg.

Backend: Traffic is routed to the nautilus-ec2 instance (i-09bba86f71d8e02ae).

3. Resource Specifications
Component,Resource Name / ID,Configuration
Load Balancer,nautilus-alb,"Application (Layer 7), Internet-facing"
Target Group,nautilus-tg,"Protocol: HTTP, Port: 80"
Public SG,nautilus-sg,Inbound: 0.0.0.0/0 (Port 80)
Backend SG,sg-0a7a5a59f13ebba23,Inbound: Restricted to nautilus-sg

4. Security Hardening
A "Security Group Chaining" strategy was employed. The nautilus-ec2 security group was updated to remove generic public access. It now strictly permits incoming traffic only if it originates from the nautilus-sg (the ALB's security group).

5. Verification Proof
Target Health: Verified as initial / healthy.

DNS Verification: Load Balancer DNS is active and responding to heartbeats.

Connectivity: Routing verified from ALB listener to Nginx target.