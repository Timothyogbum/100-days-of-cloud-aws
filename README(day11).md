# AWS Day 11: Decoupled Networking - ENI Attachment

## 🎯 Project Objective
Migrate the `datacenter-ec2` instance to a modular networking architecture by attaching a secondary Elastic Network Interface (`datacenter-eni`) in the `us-east-1` region.

## 🛠️ Technical Execution

### 1. Resource Mapping
Resolved the human-readable tags to AWS Resource IDs to ensure precision in the CLI execution:
- **Instance ID:** `i-04d3c7973cf952707`
- **ENI ID:** `eni-0fb54aa47adecfb9f`

### 2. Attachment Process
Attached the ENI as a secondary interface (`eth1`). In AWS, this requires specifying a non-zero device index to avoid conflict with the primary boot interface.
- **Command:** `aws ec2 attach-network-interface --network-interface-id eni-0fb54aa47adecfb9f --instance-id i-04d3c7973cf952707 --device-index 1`



### 3. Verification & Health Checks
Validated the success of the operation through a multi-point check:
- **Network State:** Confirmed ENI status transitioned to `in-use`.
- **Instance Health:** Verified 2/2 Status Checks (System & Instance) passed the `initializing` phase to reach `ok`.

## 💡 Engineering Reflection: The Power of the ENI
This task demonstrates the decoupling of **Compute** and **Networking**. By managing the ENI as a standalone resource:
1. **Identity Persistence:** We can move this specific Private IP and MAC address to a new instance if `datacenter-ec2` fails.
2. **Network Isolation:** We have laid the groundwork for dual-homed networking, allowing for a dedicated management or backup subnet.



## ✅ Final Result
- **Attachment Status:** SUCCESS
- **Deployment Region:** us-east-1