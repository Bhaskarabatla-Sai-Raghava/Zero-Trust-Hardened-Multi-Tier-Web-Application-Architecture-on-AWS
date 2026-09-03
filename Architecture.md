# **This is the Architecture being used in the project**
<img width="1251" height="592" alt="_MConverter eu_P1_FINAL" src="https://github.com/user-attachments/assets/006de881-b082-4f6f-9242-41cd3e1af4dd" />

## Traffic travel path

1) First when the Client enters any data the data is passed through the internet through the Internet Gateway(IGW) to enter our VPC.
2) Then, It passes through WAF(Web Application Firewall) which checks through for common web attacks like SQL, XSS we use AWS shield to protect us against DDOS.
3) Then the data is transferred to Application Load Balancer(ALB) In which the data is distributed among 2 EC2 instances across different AZ for high availability.
4) These EC2 Instances are kept in a private subnet only ALB can send traffic through.
5) The suitable data is then sent to another private subnet with our main RDS Database.
6) This RDS DB is also highly available and can only get data from our EC2 instance to maintain security, also This DB can be accessed through SSM only not plain password.
7) ALL this is monitored and tracked by CloudWatch and the API calls are tracked by CloudTrail and also VPC flow logs are enabled for troubleshooting and analysis.
- A NAT gateway is used to let our EC2 get internet updates and patches reach from the internet but not the vice-versa.
- All these are connected through IAM roles and VPC route tables.
