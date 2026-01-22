☁️ AWS Infrastructure: Identity & Access Management
Project: Stratos DC Migration (Day 17)
Objective
To establish a scalable and secure identity framework for the Nautilus DevOps team by implementing IAM Groups. This phase focuses on moving away from individual user-level permissions toward a centralized governance model.

Component,Identifier,Details
Group Name,iamgroup_kareem,Primary Permission Container
Group ID,AGPAZY5UTYMPEAVXC5I2J,Unique Backend Identifier
ARN,arn:aws:iam::672004293406:group/iamgroup_kareem,Global Resource Address
Policy State,Initialized (Empty),"Adheres to "Default Deny"

🕹️ Implementation Workflow
1. Group Resource Provisioning
Created a logical container for the DevOps team using the AWS CLI. This group serves as the foundation for Role-Based Access Control (RBAC), allowing the team to manage permissions for an entire department simultaneously.
aws iam create-group --group-name iamgroup_kareem

2. Governance Verification
Validated the group's metadata and confirmed its current membership status. The initialization with zero users ensures that no "Shadow IT" or unauthorized access exists during the infrastructure setup phase.
aws iam get-group --group-name iamgroup_kareem

💡 Engineering Reflection
Scalability: By utilizing Groups instead of individual User policies, the administrative overhead of the Nautilus migration is significantly reduced. Adding a new engineer now requires a single add-user-to-group command rather than manually attaching multiple complex JSON policies.

Security & Auditing: The group's unique ARN enables granular tracking within AWS CloudTrail. Any security events or resource modifications can be traced back to the group's specific ID, facilitating faster incident response—a core skill for the IBM X-Force internship.

Least Privilege: Maintaining a "Default Deny" state upon creation ensures that members only receive the specific permissions required for their migration tasks once the appropriate policies are vetted and attached.

