🌐 Project Report: Public VPC Infrastructure
Location: us-east-1

Engineer: DevOps Team

Status: Operational / Live ✅

1. Executive Summary
The Networking Team required a public-facing VPC environment to host external services. This deployment includes a custom Virtual Private Cloud (VPC), a public subnet with auto-assignment for IPv4 addresses, and an internet-accessible EC2 instance.

2. Networking ArchitectureVPC: datacenter-pub-vpc (CIDR: 10.0.0.0/16)Subnet: datacenter-pub-subnet (CIDR: 10.0.1.0/24)Internet Gateway: Attached igw-005db06ce068427e8 to provide a gateway for egress/ingress traffic.Routing: A custom route table directs all non-local traffic ($0.0.0.0/0$) to the Internet Gateway.Auto-IP: Enabled map-public-ip-on-launch attribute on the subnet to ensure resources are reachable by default.

3. Compute & SecurityInstance: datacenter-pub-ec2 (i-0fa2a03f06703b0d3)Type: t2.microOS: Ubuntu 22.04 LTSPublic IP: 100.53.28.188Security Group: datacenter-ssh-sg configured with a stateful inbound rule allowing TCP Port 22 from any source (0.0.0.0/0).

4. VerificationConnectivity: Routing table association confirmed.Access: Port 22 verified as open and listening on the public IP.