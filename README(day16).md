📝 AWS Project Documentation: Day 16
Task: Identity & Access Management (IAM) Provisioning
Objective: To initialize a unique user identity (iamuser_mark) to transition the Nautilus project from shared administrative access to a decentralized, auditable security model.

Technical Specifications:
User Name: iamuser_mark
User ID: AIDARQIPD6YH4XBNPGQQU
ARN: arn:aws:iam::103647802895:user/iamuser_mark
Region: Global (IAM is a global service)

🛠️ The Implementation Workflow
Identity Creation: Used the AWS CLI iam service to register the new user within the account's identity directory.
Resource Verification: Executed get-user to confirm the account was successfully written to the AWS global backend and assigned a unique Amazon Resource Name (ARN).

💡 Engineering Reflection: Zero Trust & Accountability
Blast Radius Reduction: By creating individual users instead of sharing the "Root" or "Admin" credentials, we ensure that if one set of keys is compromised, the rest of the infrastructure remains secure.

Digital Forensics: Every API call made by this user will now be recorded in AWS CloudTrail with their specific UserId. This provides the "Who, What, and When" necessary for incident response and security auditing.

Least Privilege Foundation: This user currently has zero permissions. This "Default Deny" state is the safest starting point, allowing us to layer on only the specific permissions Mark needs to do his job.