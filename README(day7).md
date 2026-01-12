## Day 7: AWS EC2 - Vertical Scaling & Resource Optimization

### 📋 Objective
Resize the `datacenter-ec2` instance from `t2.micro` to `t2.nano` to optimize resource utilization and reduce cloud spend within the `us-east-1` region.

### ⚙️ Technical Implementation
- **Instance Name:** `datacenter-ec2`
- **Current Instance ID:** `i-0bd767cc51f0c9277`
- **Action:** Upgraded from `t2.micro` to `t2.nano`.
- **Workflow:** 1. Graceful shutdown (`stopping` -> `stopped`).
    2. Attribute modification via `modify-instance-attribute`.
    3. Power on (`pending` -> `running`).

### 🛠️ Troubleshooting: ID Discovery
Initial attempts using the Day 6 ID failed. A manual audit using `describe-instances` revealed that the instance had been assigned ID `i-0bd767cc51f0c9277` in the current session.

### ✅ Verification Results
Captured following the vertical scaling event:

```text
+----------------------+----------+-----------+
|          ID          |  State   |   Type    |
+----------------------+----------+-----------+
| i-0bd767cc51f0c9277  | running  |  t2.nano  |
+----------------------+----------+-----------+
🏆 Key Takeaway
Vertical scaling in AWS EC2 is a non-zero-downtime event. Understanding the state transition requirements (Instance must be stopped to modify attributes) is critical for planning maintenance windows in production environments.