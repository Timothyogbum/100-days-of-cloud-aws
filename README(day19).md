☁️ AWS Identity & Access Management (IAM)
Project: User Permission Lifecycle & Policy Mapping (Day 19)
1. Objective
The primary goal was to complete the authorization cycle for an internal developer. This involved binding a pre-existing, customer-managed IAM policy to a specific user identity to enable their required cloud workflows while maintaining strict Least Privilege standards.

2. Technical Environment
Cloud Provider: Amazon Web Services (AWS)

Region: us-east-1 (Global IAM)

Account ID: 417003076066

Tools: AWS CLI v1 (Legacy stable)

3. Implementation Workflow
Phase 1: Resource Identification
Before attachment, the unique Amazon Resource Name (ARN) for the policy was retrieved to ensure targeting of the correct permission set within the local account scope.

Command: aws iam list-policies --scope Local --query "Policies[?PolicyName=='iampolicy_john'].Arn" --output text

Result: arn:aws:iam::417003076066:policy/iampolicy_john

Phase 2: Policy Attachment
The policy was surgically attached to the user principal. This step activates the permissions defined in the JSON document for that specific user.

Command: aws iam attach-user-policy

--user-name iamuser_john

--policy-arn arn:aws:iam::417003076066:policy/iampolicy_john


Phase 3: Verification & Audit
To ensure the mapping was successful and visible to the AWS Control Plane, a final audit of attached policies was performed.

Verification Command: aws iam list-attached-user-policies --user-name iamuser_john --output table

4. Engineering Reflection
CLI Versioning: During execution, a version mismatch was identified regarding the --output tsv parameter. The workflow was successfully adapted to use --output text, demonstrating situational awareness of the environment's specific tooling constraints.

Separation of Concerns: By using a Managed Policy rather than an Inline Policy, we ensure that iampolicy_john can be versioned, audited, and potentially shared with other users in the future, improving administrative efficiency.