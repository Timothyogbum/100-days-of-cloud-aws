Project Name: Nautilus DevOps Private Subnet Connectivity

Environment: us-east-1 (VPC: nautilus-priv-vpc)

### 🎯 Objective
Enable secure outbound internet access for the nautilus-priv-ec2 instance located in a private subnet to allow automated uploads to the nautilus-nat-27558 S3 bucket, while maintaining a cost-effective architecture by using a NAT Instance instead of a NAT Gateway.

### 🛠️ Technical Implementation Details
1. Networking Infrastructure

Public Subnet: Created nautilus-pub-subnet (10.1.2.0/24) to host the NAT bridge.

Internet Gateway: Provisioned and attached an IGW to the VPC to provide the public egress point.

Public Routing: Established a route table (nautilus-pub-rt) with a default route (0.0.0.0/0) targeting the IGW.

2. NAT Instance Configuration

Instance: Launched nautilus-nat-instance using Amazon Linux 2.

Hardware Attribute: Disabled Source/Destination Checks. This is critical as it allows the instance to process and forward traffic that is not addressed to its own private IP.

Security Group: Implemented nautilus-nat-sg allowing all traffic from the VPC CIDR (10.1.0.0/16) to ensure the private instance can reach the gateway.

3. OS-Level Logic (Persistence)

Used a Multipart MIME User Data script to ensure configuration persistence.

Enabled IPv4 forwarding via sysctl.

Configured iptables with a MASQUERADE rule on eth0 to translate private IP addresses to the NAT instance's public IP for internet-bound packets.

4. Private Routing

Modified the nautilus-priv-rt route table.

Associated the route table explicitly with the nautilus-priv-subnet.

Added a default route (0.0.0.0/0) targeting the nautilus-nat-instance ID.

### ✅ Verification Results
Successfully verified connectivity by listing the S3 bucket from the AWS CLI, confirming the presence of the nautilus-test.txt file uploaded by the private instance's cron job.