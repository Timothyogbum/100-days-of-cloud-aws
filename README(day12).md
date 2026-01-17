# AWS Day 12: Persistent Block Storage Integration

## 🎯 Project Objective
Attached an Elastic Block Store (EBS) volume to an existing EC2 instance to facilitate data persistence and storage expansion for the Nautilus DevOps team's services.

## 🛠️ Technical Implementation
- **Cloud Provider:** AWS
- **Service:** EC2 (Elastic Compute Cloud) & EBS (Elastic Block Store)
- **Region:** us-east-1
- **Identifiers:**
  - Instance ID: `i-0bcddf19ce557ff93`
  - Volume ID: `vol-0d6917a6a867a9f2c`
- **Device Mapping:** `/dev/sdb`

## 💡 Key Engineering Concepts
### 1. Decoupled Architecture
By attaching a separate EBS volume rather than using the instance's root partition for everything, we ensure that critical application data is decoupled from the compute instance. This allows for easier instance replacement and snapshots.



### 2. Device Path Convention
While AWS uses the path `/dev/sdb`, modern Linux kernels may internally rename this device (e.g., to `/dev/xvdb` or `/dev/nvme1n1`). Understanding this mapping is crucial for the subsequent OS-level mounting process.

## ✅ Final Status
The volume `vol-0d6917a6a867a9f2c` is successfully attached to `i-0bcddf19ce557ff93` as a block device.