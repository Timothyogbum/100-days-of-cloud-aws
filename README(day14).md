AWS Project Documentation: Day 14
Task: Automated Infrastructure Decommissioning
Objective: To identify and permanently terminate the devops-ec2 instance in the us-east-1 region, ensuring zero residual compute costs for obsolete migration resources.

Technical Specifications:
Provider: AWS
Instance ID: i-0cef3b4cb7db4f684
Region: us-east-1
Final Verified State: terminated

🛠️ The Implementation Workflow
Resource Identification: Used describe-instances with a specific Name tag filter and state filter (running, stopped) to isolate the target Instance ID.

Lifecycle Termination: Executed the terminate-instances command.

Synchronous Verification: Employed the aws ec2 wait instance-terminated command to pause execution until the AWS backend confirmed the final state, ensuring compliance with task requirements.

💡 Engineering Reflection: Version Compatibility & FinOps
CLI Troubleshooting: Encountered a version-specific error where the tsv output format was unsupported. Resolved by switching to text output, ensuring the Instance ID was correctly parsed for the next step in the pipeline.

Cost Governance: This task is a practical application of Cloud FinOps. By moving an instance from a stopped state (which still incurs costs for attached EBS volumes) to terminated, we ensure that all associated resources are flagged for cleanup, optimizing the cloud budget.