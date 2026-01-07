## Day 2: AWS Security Group Configuration
**Task:** Create a firewall perimeter for Nautilus App Servers.
**Outcome:** Successfully provisioned `devops-sg` with specific ingress rules.
**Details:**
- **Security Group ID:** `sg-0f8d3e200262ad729`
- **Inbound Rules:** Port 80 (HTTP) & Port 22 (SSH) allowed from all sources (0.0.0.0/0).
- **Verification:** Confirmed via AWS CLI `describe-security-groups`.
