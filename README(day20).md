🔐 AWS IAM: Service-Linked Role Configuration
Project: Nautilus DevOps Access Controls (Day 32)
1. Objective
The primary goal was to establish a secure, role-based access control (RBAC) mechanism for EC2 instances. By creating a specific IAM role with a trust relationship for the EC2 service, we allow cloud compute resources to securely interact with other AWS services without the use of long-term, static credentials.

2. Technical Specifications
IAM Role Name: iamrole_kareem

Entity Type: AWS Service

Use Case: EC2

Attached Policy: iampolicy_kareem

Account ID: 703570702606

3. Implementation Workflow
Phase 1: Trust Policy Definition
A JSON trust policy was authored to define the AssumeRole permission for the Amazon EC2 service.

JSON

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": { "Service": "ec2.amazonaws.com" },
      "Action": "sts:AssumeRole"
    }
  ]
}
Phase 2: Role Creation & Policy Attachment
Utilizing the AWS CLI, the role was provisioned and associated with the existing managed policy.

Creation: aws iam create-role --role-name iamrole_kareem ...

Dynamic Mapping: Retrieved the POLICY_ARN via a filtered query to ensure accuracy.

Association: Attached iampolicy_kareem to grant the role its specific functional permissions.

4. Security Justification
Identity Federation: By using service principals (ec2.amazonaws.com), we eliminate the need for manual secret rotation on host machines.

Resource Isolation: The role is restricted to the specific policy iampolicy_kareem, ensuring granular control over what an assumed instance can do.