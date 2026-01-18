# Day 13: AWS Infrastructure Templating (AMI Creation)

## 🎯 Project Objective
Establish an immutable deployment template for the `devops-ec2` instance to ensure consistency, scalability, and disaster recovery readiness during the Stratos DC migration.

## 🛠️ Technical Implementation

### 1. Resource Identification
Identified the target EC2 instance via CLI filters to ensure the correct "Golden State" was captured.
- **Source Instance ID:** `i-08a1b7f98773077cb`

### 2. Image Capture
Executed the `create-image` command to initiate block-level snapshots of all attached EBS volumes.
- **AMI Name:** `devops-ec2-ami`
- **Command:** `aws ec2 create-image --instance-id i-08a1b7f98773077cb --name "devops-ec2-ami"`



### 3. State Management & Verification
Managed the asynchronous nature of cloud imaging by utilizing AWS CLI waiters. This ensured the image was fully registered and the underlying snapshots were finalized before concluding the task.
- **Verification:** `aws ec2 wait image-available --filters "Name=name,Values=devops-ec2-ami"`
- **Final State:** `available`

## 💡 Engineering Reflection: The Power of Immutability
Creating an AMI is a core tenet of **Immutable Infrastructure**. By baking the OS, patches, and configurations into a single image ID, we eliminate "Configuration Drift." If a production server becomes unstable, we do not troubleshoot; we terminate and redeploy a fresh instance from this AMI in seconds.



## ✅ Final Status
The `devops-ec2-ami` is registered and available in the `us-east-1` region, ready to be utilized by Auto Scaling Groups (ASG) or as a backup recovery point.