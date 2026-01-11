## Day 6: AWS Compute - EC2 Instance Provisioning (Detailed Case Study)

### 📋 Objective
Deploy a standardized compute node (`datacenter-ec2`) within the default VPC using the Amazon Linux 2 AMI and RSA key pair authentication.

### ⚙️ Infrastructure Specifications
- **Instance Name:** `datacenter-ec2`
- **Instance ID:** `i-0108877703f0d88bc`
- **AMI ID:** `ami-0fcb14c72c80bdef2`
- **Instance Type:** `t2.micro`
- **Key Pair:** `datacenter-kp`
- **Security Group:** `sg-0a6f3dcebff56b68e` (default)

### ✅ Execution Results (Terminal Audit)

**1. Key Pair Generation:**
Validated that the key material was correctly piped to a local `.pem` file and secured with `chmod 400`.
```text
$ ls -l datacenter-kp.pem
-r-------- 1 thor thor 1674 Jan 11 20:05 datacenter-kp.pem
2. Provisioning Metadata (JSON Snippet): The following network and state metadata was captured immediately after the resource reached the running state:

JSON

{
    "InstanceId": "i-0108877703f0d88bc",
    "State": {
        "Code": 16,
        "Name": "running"
    },
    "PublicIpAddress": "107.20.47.87",
    "PrivateIpAddress": "172.31.28.232",
    "VpcId": "vpc-0a5ee60179e75cc9f",
    "SubnetId": "subnet-0a7d230083f4f6481"
}

3. Availability Zone Placement: The instance was successfully placed in us-east-1a, matching the regional requirement for the Nautilus migration project.

🏆 Key Takeaways
Idempotency: Encountered InvalidKeyPair.Duplicate error on a re-run attempt, confirming AWS's protection against overwriting existing cryptographic keys.

Resource Tagging: Successfully applied the Name tag to ensure discoverability within the AWS Management Console and via CLI filters.

Network Readiness: Confirmed the instance received both a Private IP for internal VPC routing and a Public IP for external management. 