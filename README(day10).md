# AWS Day 10: Infrastructure Persistence - Elastic IP (EIP) Integration

## 🎯 Project Objective
In the "devops-ec2" migration phase, the Nautilus team identified a risk: the instance was relying on a dynamic Public IP. This meant any maintenance reboot would break DNS records and external whitelists. My objective was to allocate and associate a static **Elastic IP (EIP)** to ensure a permanent network endpoint.

## 🛠️ Technical Implementation & CLI Workflow

### 1. Discovery and Variable Mapping
I utilized the AWS CLI to resolve human-readable tags into the unique Amazon Resource Names (ARNs) and IDs required for API operations.


# Extracting Instance ID
INSTANCE_ID=$(aws ec2 describe-instances --filters "Name=tag:Name,Values=devops-ec2" --query "Reservations[0].Instances[0].InstanceId" --output text)

# Extracting EIP Allocation ID
ALLOCATION_ID=$(aws ec2 describe-addresses --filters "Name=tag:Name,Values=devops-ec2-eip" --query "Addresses[0].AllocationId" --output text)
2. Network Interface Association
The associate-address command was executed to map the EIP to the primary Network Interface (ENI) of the instance.



aws ec2 associate-address \
  --instance-id i-037e3365507544d85 \
  --allocation-id eipalloc-00dc9b6ceb23487f7
Resulting Association ID: eipassoc-0aae88c5d85353d07

3. Verification of "Static" State
Post-association, I queried the EC2 metadata to confirm the instance was broadcasting the reserved IP.

Verified Public IP: 18.235.44.118

🌍 The "Why" Behind the Architecture
Ephemeral vs. Elastic Networking
By default, AWS Public IPs are released back to the AWS pool when an instance is stopped. An Elastic IP is a reserved asset that remains under our account's control regardless of the instance state.

Real-World Benefits
DNS Stability: The A-record for api.nautilus.com can now point to 18.235.44.118 permanently.

Security Whitelisting: External firewalls at partner sites can now safely whitelist this single IP without fear of it changing during a weekend maintenance window.

Fault Tolerance: If this instance fails, the EIP can be "remapped" to a standby instance in seconds, redirecting all traffic without a DNS propagation delay.

✅ Final Result
Target Instance: devops-ec2 (i-037e3365507544d85)

Assigned Static IP: 18.235.44.118

Network Status: Persistent / Production-Ready