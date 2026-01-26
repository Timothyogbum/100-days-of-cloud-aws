📝 AWS Infrastructure Report: Stable Access Deployment
Project: Datacenter App Hosting (Day21)
1. Executive Summary
To support a new application requiring high availability and persistent connectivity, a virtualized compute resource was deployed and associated with a static Elastic IP (EIP). This ensures that the public-facing endpoint remains unchanged through instance reboots or underlying hardware maintenance.

2. Provisioning Details
Resource,Name Tag,ID / Address
EC2 Instance,datacenter-ec2,i-037519e768a4b38f7
Instance Type,t2.micro,"1 vCPU, 1 GiB RAM"
Operating System,Ubuntu 20.04 LTS,ami-0fb0b230890ccd1e6
Elastic IP,datacenter-eip,34.202.140.240

3. Technical Workflow
AMI Discovery: Queried the Amazon owners' market for the latest stable Ubuntu 20.04 HVM SSD image.
Instance Launch: Provisioned the t2.micro instance with atomic tagging for governance.
EIP Allocation: Reserved a static IP from the AWS pool and applied the datacenter-eip metadata.
Association: Mapped eipalloc-0d02bfb790c12b1e6 to the network interface of the instance.

4. Verification
The final validation confirms the mapping is active:
Target: datacenter-ec2
Resolved IP: 34.202.140.240


