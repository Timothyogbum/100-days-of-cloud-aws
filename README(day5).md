## Day 5: AWS EBS Storage - Provisioning gp3 Volumes
**Objective:** Deploy next-generation block storage for the incremental migration of Nautilus infrastructure.

**Configuration Details:**
- **Resource:** `AWS::EC2::Volume`
- **Name Tag:** `nautilus-volume`
- **Type:** `gp3`
- **Capacity:** 2 GiB
- **Availability Zone:** `us-east-1a`

**Technical Advantage:**
Implemented the **gp3** volume type, which allows for independent scaling of IOPS and throughput from storage capacity. This ensures high performance for small volumes without the cost overhead of over-provisioning storage just to get higher IOPS.