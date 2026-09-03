# Zero-Trust-Hardened-Multi-Tier-Web-Application-Architecture-on-AWS
## Overview-
- To build a Multi-tier AWS architecture hardened with tiered security group and identity-based IAM access instead of network-only trust. This demonstration uses tools like IAM, AWS WAF, AWS SSM, AWS Secrets manager etc.
- This is build to show the major ways of security in AWS
## Architecture
<img width="1251" height="592" alt="_MConverter eu_P1_FINAL" src="https://github.com/user-attachments/assets/c2466ba0-2e1d-4193-bdb7-7b665f9ca4d1" />
- To follow the flow of traffic and every feature in the architecture look in the architecture file.

### Some important Design decisions explained

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
- WAF
- Monitoring: CloudWatch, VPC Flow Logs, CloudTrail
- SSM

## Security Controls & Evidence
1) The below shows the security groups configuration for ALB, EC2, RDS <img width="4563" height="569" alt="SG Settings IGW to ALB-imageonline co-merged" src="https://github.com/user-attachments/assets/eed3c754-d45f-473d-b699-be6bb734fbd7" />
2) The below is the photo of the IAM role created to connect EC2 with SSM<img width="1904" height="824" alt="IAM role to connect EC2 and SSM" src="https://github.com/user-attachments/assets/0c59c8c8-e880-4200-a19f-345442c062c1" />
3) Proof of Accessing EC2 from SSM and connecting to our Database<img width="1913" height="162" alt="Proof of EC2 to RDS" src="https://github.com/user-attachments/assets/2a966cae-8db7-4955-8e2e-52dfa90765c6" />
4) WAF Settings are shown below <img width="1914" height="861" alt="WAF-SETTINGS" src="https://github.com/user-attachments/assets/b78e2363-ca28-4e21-8c5f-045198b19fd0" />

## Zero-Trust Boundary Proof

1)  direct SSH attempt to EC2 blocked-<img width="1907" height="957" alt="Proof EC2 Not connecting directly to internet" src="https://github.com/user-attachments/assets/e235ad29-74bd-4417-8de8-c674fd13c4c6" />
2) direct RDS connection attempt from outside fails<img width="1417" height="92" alt="RDS Not connecting proof" src="https://github.com/user-attachments/assets/47d6f6ec-37c9-4806-aef6-8e124110e779" />
3) Only works from ALB to EC2 to RDS<img width="1918" height="322" alt="INSIDE RDS FROM EC2" src="https://github.com/user-attachments/assets/e08f9c21-61fb-448a-84ad-82ee2faef762" />

## Monitoring and Logging

1) CloudWatch automatically registers the events of the architecture with event history
2) VPC Flow logs event history in CloudWatch<img width="1914" height="853" alt="Cloudwatch proof" src="https://github.com/user-attachments/assets/e2cae3ac-e6d8-4ea6-8334-5becc7c57fde" />
3) CloudTrail Event History is mapped by creating a trail<img width="1917" height="817" alt="Cloudtrail with history" src="https://github.com/user-attachments/assets/7738aa9e-6afc-48c0-937e-fe737eb79941" />

## Troubleshooting

1) didn't know SSM requires an IAM role with the policy 'AmazonSSMManagedInstanceCore' and also after that a NAT Gateway or VPC Endpoints are required to access the EC2 Instances with SSM .
2) ALB target groups which are our EC2 instances are shown unhealthy since the nginx user data script pasted at the creation of our instances didn't download so to fix it we had to connect to the instances via SSM and manually install and enable nginx.
3) Also learned and implemented the difference between IAM permission and trust policies.

## Future improvements

1) HTTPS instead of HTTP and requesting and managing the SSL certificate by AWS ACM this couldn't be done now due to domain hosting issues.
2) Higher storage and compute power to there sources couldn't be done now due to free account restrictions.

## Cost Managment

- This is a free tier AWS account with a $200 credit and all free tier options.

## All Tools Used

- AWS- VPC, EC2, RDS, ALB, IAM, WAF, KMS, CloudWatch, CloudTrail, SSM 










