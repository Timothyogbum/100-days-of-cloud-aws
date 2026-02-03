This was a textbook "full-stack" networking challenge. You didn't just plug in a cable (Peering); you had to draw the map (Routes), open the gates (Security Groups), and fix the lock (SSH Key Persistence).

Here is your comprehensive documentation and commit history for the Nautilus VPC Peering project.

Lab Report: Nautilus VPC Peering Infrastructure
## Objective
Establish a secure, bi-directional communication bridge between the Default Public VPC and the Nautilus Private VPC in us-east-1, enabling administrative access (SSH) and connectivity testing (ICMP) across network boundaries.

## The Struggle (Technical Hurdles)
This lab required solving three distinct layers of the OSI model:

The Handshake (Layer 3 - Peering):

Problem: VPCs are isolated by design.

Solution: Created pcx-0ec6047e8ca397fbb and performed a "self-accept" within the account to move the status from provisioning to active.

The Map (Layer 3 - Routing):

Problem: Packets knew where they wanted to go but didn't know the "next hop."

Solution: Injected explicit routes into both the Public (172.31.0.0/16) and Private (10.1.0.0/16) Route Tables pointing to the Peering ID.

The Gatekeeper (Layer 4 - Security Groups):

Problem: The Private EC2 was dropping all inbound traffic, and the Public EC2 was unreachable via SSH.

Solution: Authorized Port 22 (TCP) for the Public SG and All ICMP for the Private SG specifically from the peer VPC CIDR.

The Persistent Lock (Access Management):

Problem: AWS Instance Connect is ephemeral (60-second window), which often causes automated validators to fail.

Solution: Used the 60-second window to permanently append /root/.ssh/id_rsa.pub to the ec2-user's authorized_keys file on disk.

## Implementation Summary
Resource,Name / ID,Configuration
Peering Connection,nautilus-vpc-peering,pcx-0ec6047e8ca397fbb (Active)
Public Route,rtb-03be...,Destination: 10.1.0.0/16 via pcx-0ec6...
Private Route,rtb-0466...,Destination: 172.31.0.0/16 via pcx-0ec6...
Public SG,sg-0d99...,Allowed TCP 22 (SSH) from 0.0.0.0/0
Private SG,sg-0be7...,Allowed ICMP (Ping) from 172.31.0.0/16

## Final Verification Results
SSH Connectivity: Successfully authenticated as ec2-user on 54.227.0.100.

Cross-VPC Ping:

4 packets transmitted, 4 received, 0% packet loss, time 3006ms

Peering Status: Verified via CLI as active.