📝 Project README: S3 Data Migration
Project: Nautilus Data Migration Phase 1
1. Objective
To migrate critical data assets from a legacy S3 environment to a new, private production bucket while ensuring absolute data integrity and consistency.

2. Infrastructure Details
Resource,Name,Region
Source Bucket,datacenter-s3-17011,us-east-1
Destination Bucket,datacenter-sync-19178,us-east-1
Migration Tool,AWS CLI (S3 Sync),N/A

3. Implementation Workflow
Provisioning: Created the datacenter-sync-19178 bucket using the mb (Make Bucket) command.

Synchronization: Executed a recursive sync to transfer all objects. This method was chosen over a simple copy to ensure that object metadata was preserved and that the transfer could be resumed if interrupted.

Validation: Performed a recursive summarization of both buckets to verify that the Object Count and Total Payload Size matched exactly.

4. Verification Results
Total Objects Migrated: 3,349

Total Data Volume: 76.13 MB (76,133,582 bytes)

Status: 100% Consistent ✅

