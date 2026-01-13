## Day 8: AWS Governance - Protecting Critical Workloads

### 📋 Objective
Configure **Stop Protection** for the `datacenter-ec2` instance to prevent accidental service interruptions during the Nautilus infrastructure migration.

### ⚙️ Technical implementation
- **Target Host:** `datacenter-ec2`
- **Region:** `us-east-1`
- **Instance ID:** `i-0fce16e3285183afe`
- **Protection Mechanism:** `DisableApiStop` attribute enabled via AWS CLI.

### ✅ Verification Log
The attribute modification was audited using the `describe-instance-attribute` command.

```text
$ aws ec2 describe-instance-attribute --instance-id i-0fce16e3285183afe --attribute disableApiStop
{
    "DisableApiStop": {
        "Value": true
    }
}
🧠 Lessons Learned
Governance Guardrails: Enabling DisableApiStop is a best-practice for production instances where high availability is paramount. It forces an administrator to intentionally remove the protection before the instance can be shut down.

Operational Safety: This differs from DisableApiTermination in that it specifically guards the instance state (Running) rather than its existence (Deletion).