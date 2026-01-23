📝 AWS Project Documentation: Day 18
Task: IAM Policy Engineering & Governance
Objective: To implement a custom, granular permission set for EC2 monitoring, adhering to the security mandate of Least Privilege.

Technical Specifications:

Policy Name: iampolicy_ammar

ARN: arn:aws:iam::380043499365:policy/iampolicy_ammar

Region: us-east-1

Capabilities: View instances, AMIs, and snapshots without modification rights.

🛠️ Implementation Reflection
JSON Strategy: By limiting the actions to ec2:Describe*, ec2:Get*, and ec2:List*, we ensure that any user assigned this policy can monitor health and status but is strictly prohibited from ec2:RunInstances (cost control) or ec2:TerminateInstances (uptime security).

Managed Policy Advantage: We created a Customer Managed Policy rather than an Inline Policy. This is a "DevOps Best Practice" because it allows the policy to be re-used across multiple users and groups, making future audits much simpler.