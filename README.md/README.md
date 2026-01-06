## Project: Nautilus AWS Migration
Documenting my transition to Amazon Web Services.

### Day 1: Identity and Access (EC2 Key Pairs)
**Objective:** Create a secure RSA key pair named `devops-kp` for instance access.

**Hurdles & Solutions:**
- **Environment Context:** Found that CLI access keys were not provided in the lab `showcreds`.
- **Solution:** Utilized the **AWS Management Console** (Web UI) to provision the key pair in the `us-east-1` region.
- **Verification:** Successfully generated `devops-kp` as an RSA type with a `.pem` format.

**Key Cloud Concepts:**
- **Regions:** AWS services are region-specific; all work was done in **us-east-1**.
- **Key Pairs:** AWS uses asymmetric encryption (RSA) to ensure only the holder of the private key can access a Virtual Machine.
EOF