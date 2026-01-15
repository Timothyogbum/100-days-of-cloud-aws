# AWS Day 9: Critical Infrastructure Guardrails - EC2 Termination Protection

## 🎯 Project Objective
The Nautilus DevOps team identified a vulnerability in the migration of the `xfusion-ec2` instance: it was missing **Termination Protection**. My task was to retrofit this production instance with safety guardrails to prevent accidental deletion via the AWS Console, CLI, or automated cleanup scripts.

## 🛠️ Technical Execution & CLI Workflow

### 1. Resource Identification (Targeting the 'Pet')
In a cloud environment with hundreds of instances, targeting by name is safer than hardcoding IDs. I used the AWS CLI to filter by the `Name` tag to isolate the specific Instance ID.


aws ec2 describe-instances \
  --filters "Name=tag:Name,Values=xfusion-ec2" \
  --query "Reservations[0].Instances[0].InstanceId" \
  --output text
Resulting Instance ID: i-0048e37be35738402

2. Modifying the Instance Attribute
The DisableApiTermination attribute is the specific API flag that governs whether a TerminateInstances call is accepted or rejected by the AWS EC2 service.

Bash

aws ec2 modify-instance-attribute \
  --instance-id i-0048e37be35738402 \
  --disable-api-termination
3. State Verification
DevOps best practice dictates that an operation is not "Done" until the state change is verified against the provider's API.



aws ec2 describe-instance-attribute \
  --instance-id i-0048e37be35738402 \
  --attribute disableApiTermination \
  --query "DisableApiTermination.Value"
Verified Status: true

🌍 Real-World Impact & Logic
Why Termination Protection?
In modern DevOps, we use many tools that have the power to delete resources:

Auto Scaling Groups: Might scale down the wrong node if not configured correctly.

Cleanup Scripts: Boto3 scripts meant to delete "untagged" resources could accidentally target production.

Infrastructure as Code (IaC): A terraform destroy or a CloudFormation stack deletion would be stopped in its tracks by this setting.

The "Friction" Principle
This implementation introduces Intentional Friction. To delete this instance now, an engineer must:

Manually disable the protection (a conscious act of intent).

Then issue the termination command. This two-step process effectively eliminates "fat-finger" errors.

✅ Final Result
Instance: xfusion-ec2 (i-0048e37be35738402)

Status: Secured

Region: us-east-1