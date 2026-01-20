📝 AWS Project Documentation: Day 21
Task: EBS Volume Data Protection
Objective: To create a point-in-time, durable backup of the datacenter-vol EBS volume to support automated recovery and disaster mitigation.

Technical Specifications:
Source Volume: vol-0ba827719649a8832 (datacenter-vol)
Snapshot ID: snap-041d353f55a4f559d
Region: us-east-1
Status: completed

🛠️ The Implementation Workflow
Resource Identification: Queried the EC2 environment to locate the specific Volume ID associated with the datacenter-vol tag.
Snapshot Initiation: Executed the create-snapshot command with the required metadata:
Name Tag: datacenter-vol-ss
Description: datacenter Snapshot

Synchronous Verification: Employed the aws ec2 wait snapshot-completed utility. This ensured that all data blocks were successfully transferred to Amazon S3 and verified for integrity before marking the task as finished.

💡 Engineering Reflection: Incremental Backups & DR
Storage Efficiency: Because EBS snapshots are incremental, this backup only stored the blocks that changed since the last snapshot, optimizing storage costs while providing a full recovery point.

Incident Readiness: In the context of Incident Response, having a verified "completed" snapshot is the prerequisite for spinning up a forensic instance or restoring a compromised service without data loss.