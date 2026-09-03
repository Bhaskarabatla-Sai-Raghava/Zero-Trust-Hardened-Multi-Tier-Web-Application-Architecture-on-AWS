# Zero-Trust-Hardened-Multi-Tier-Web-Application-Architecture-on-AWS
## Overview-
- To build a Multi-tier AWS architecture hardened with tiered security group and identity-based IAM access instead of network-only trust. This demonstration uses tools like IAM, AWS WAF, AWS SSM, AWS Secrets manager etc.
- This is build to show the major ways of security in AWS
## Architecture
<img width="1251" height="592" alt="_MConverter eu_P1_FINAL" src="https://github.com/user-attachments/assets/c2466ba0-2e1d-4193-bdb7-7b665f9ca4d1" />
- To follow the flow of traffic and every feature in the architecture look in the architecture file.
## Some important Design decisions explained
1) Multi AZ is used for RDS to keep it fault tolerant and highly available
2) Subnets are isolated so that the data transfer can take place securely like ALB is in the public subnet since it need to receive traffic from the Internet Gateway But the EC2's and RDS instance are in private subnets since they get traffic from specific sources like ALB and need to be protected from attackers.
3) SSM is used instead of SSH since it is more secure as the account with the right Permissions and encrypted password only can enter the Database.
4) HTTP is used instead of HTTPS due to domain and cost constraints but it is in future plans.
5) NAT Gateway is used if our EC2 instances need to connect to the internet for patches and updates but not the vice-versa since the instances are kept isolated for security.
## Components used
- VPC, subnets, route tables, IGW, NAT Gateway
- ALB (listener, target group)
- EC2 (Auto Scaling or manual, AMI, nginx user data script)
- RDS (engine, Multi-AZ, encryption)
- Security Groups (table: SG name, inbound rule, outbound rule)
- IAM roles (EC2 instance role, permissions attached)
- WAF
- Monitoring: CloudWatch, VPC Flow Logs, CloudTrail
- SSM
## Security Controls & Evidence


