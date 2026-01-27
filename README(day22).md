🌐 AWS Infrastructure: xfusion-ec2 Deployment
Project: Secure EC2 Landing Zone
1. Executive Summary
Provisioned a t2.micro instance in the us-east-1 region. The deployment required manual configuration of Security Group ingress rules and a credential bridge to satisfy the requirement for passwordless root access from the aws-client host.

2. Technical Specifications
Resource,Value,Status
Instance Name,xfusion-ec2,✅
Instance Type,t2.micro,✅
Public IP,54.163.20.140,✅
SSH Key Path,/root/.ssh/id_rsa,✅
Security Group,sg-018b0010d6961cf2b,✅ (Port 22 Open)
User Access,root,✅ (Passwordless)

3. Operational Implementation Log
Identity Management: Generated a 4096-bit RSA key on the aws-client jump host.

Infrastructure: Imported the public key as an AWS Key Pair and launched the instance into the default VPC.

Firewall Management: Authorized inbound TCP traffic on Port 22 to enable remote management.

Credential Bridging: Since standard Ubuntu AMIs disable root SSH, the public key was manually injected into /root/.ssh/authorized_keys via the ubuntu bootstrap user.