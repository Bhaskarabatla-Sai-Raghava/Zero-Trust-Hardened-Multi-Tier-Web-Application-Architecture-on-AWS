## In this document i will walkthrough the entire process (settings, configurations etc.)

- This will take place in the same order as the traffic flow with every service i will upload its configurations and proof if any
1) Firstly the internet gateway catches the traffic from the internet to our VPC just its name and the VPC attachment are asked and the security group is already shown in readme.
2) WAF analyzes this traffic its settings are<img width="1914" height="861" alt="WAF-SETTINGS" src="https://github.com/user-attachments/assets/4848fa64-8f48-47c4-b8e6-1e2674b1128e" /> and it creates logs in CloudWatch<img width="1916" height="536" alt="WAF-LOGS PROOF" src="https://github.com/user-attachments/assets/232033f4-5713-49a6-b865-f5bcb3ebb8e5" />
3) This is then forwarded to ALB whose settings are <img width="1871" height="688" alt="ALB settings 2" src="https://github.com/user-attachments/assets/ab3fc910-e3f0-471c-8de7-4ef882a97885" />
<img width="1885" height="603" alt="ALB settings 1" src="https://github.com/user-attachments/assets/d9d07b5a-119b-4679-940b-a97566e8e008" /> and its security group to both EC2 and IGW are already uploaded in readme. Its targets are EC2 Instances which will be created in the next step<img width="1910" height="809" alt="TARGETS" src="https://github.com/user-attachments/assets/f534434d-3fb9-4539-932a-ccc090a097e7" />

4) EC2 has the settings <img width="1903" height="799" alt="EC2 settings 2" src="https://github.com/user-attachments/assets/d097c874-f3cf-4d98-bec8-a1daf2067c61" />
<img width="1912" height="801" alt="EC2 Settings1" src="https://github.com/user-attachments/assets/d65bf4e0-fce3-42b2-a562-28c2a0b15792" /> and this is the nginx script<img width="1905" height="777" alt="Userdata EC2" src="https://github.com/user-attachments/assets/65a9caf2-5ebc-42a2-99f6-fd17ad58f06d" />
5) The above instances can be accessed only through SSM not the internet<img width="1907" height="957" alt="Proof EC2 Not connecting directly to internet" src="https://github.com/user-attachments/assets/a2fbfe62-14ba-4248-9089-c33c71b34f6c" /> The SSM needs a role to connect<img width="1904" height="824" alt="IAM role to connect EC2 and SSM" src="https://github.com/user-attachments/assets/e411210a-f4a5-4521-a595-d3e2f853bfd4" />

6) Then this data is stored in the RDS with the settings<img width="1914" height="769" alt="RDS settings 3" src="https://github.com/user-attachments/assets/d0ee1370-dfc2-41ad-b9d5-c7d874874034" />
<img width="1904" height="801" alt="RDS settings 2" src="https://github.com/user-attachments/assets/1b552abc-2388-47c4-8322-bc0ca5e95441" />
<img width="1892" height="682" alt="RDS settings1" src="https://github.com/user-attachments/assets/af99212e-5a57-42dd-a589-82dab883d08a" />
This can only be accessed through EC2 not through the internet<img width="1417" height="92" alt="RDS Not connecting proof" src="https://github.com/user-attachments/assets/86d1508e-a1a7-4264-8858-6e02f6632239" /> the security group is already uploaded.
7) The below is the proof of the instance working<img width="1911" height="872" alt="Proof of EC2 working" src="https://github.com/user-attachments/assets/d7262b63-9371-4107-850f-ed4e18f38b7c" />
8) The subnets are public1<img width="1919" height="800" alt="Public subnet1" src="https://github.com/user-attachments/assets/bebf4a30-40cd-4e1f-bf38-6cb868f6a5be" /> and public 2<img width="1908" height="823" alt="Publicsubnet2" src="https://github.com/user-attachments/assets/5c54ffe0-961c-4b95-8830-5a45c127e186" /> private 1<img width="1907" height="724" alt="Private subnet1" src="https://github.com/user-attachments/assets/63223bfa-1c27-4c51-8d11-2bd9e2e78190" /> and<img width="1919" height="837" alt="Private subnet 2 real" src="https://github.com/user-attachments/assets/7d321e29-8998-4d92-ba0c-16232effbf88" />
 private subnet2 and also RDS<img width="1919" height="821" alt="RDS Subnet" src="https://github.com/user-attachments/assets/b2c343db-68e1-47ea-9179-a48a9cb8dc03" />

Also the Route tables for RDS<img width="1639" height="828" alt="RDS Route table" src="https://github.com/user-attachments/assets/0e79b5e7-a00b-43b2-bf93-9ffb37c8d956" /> Public<img width="1919" height="871" alt="Public route table" src="https://github.com/user-attachments/assets/4ac3d573-7004-4714-9817-a7f614d91cc6" /> and private<img width="1579" height="227" alt="PVT ROUTE TABLE" src="https://github.com/user-attachments/assets/7fab2a2b-d866-4c9c-ab90-090e34a3f824" /> With the routes <img width="1522" height="242" alt="PUBLIC ROUTES" src="https://github.com/user-attachments/assets/21859149-3d05-40d7-b976-0a927b0bde4b" /> and private <img width="1593" height="233" alt="PVT ROUTES" src="https://github.com/user-attachments/assets/236f1c11-96e8-4ebc-8753-b9474936e067" /> RDS just has the default local route since it is meant to be private.

9) After connecting EC2 with RDS we can access RDS through EC2<img width="1918" height="322" alt="INSIDE RDS FROM EC2" src="https://github.com/user-attachments/assets/530de2f8-9984-429c-a376-312b94cdf181" />
Cloud Watch CLoudTrail proof<img width="1914" height="853" alt="Cloudwatch proof" src="https://github.com/user-attachments/assets/17816835-8cdf-42df-8586-1f4fff2362c6" /><img width="1917" height="817" alt="Cloudtrail with history" src="https://github.com/user-attachments/assets/8a5e3eda-3a08-462d-9c7c-62633bae112a" /> they are just one click deploy no settings needed.
But Flow Logs settings are<img width="1916" height="871" alt="Flow logs settings real" src="https://github.com/user-attachments/assets/eba0ff6a-4284-47f1-82f6-db40bff94b8d" /> it also needs a IAM role<img width="1919" height="876" alt="Role for VPC LOGS" src="https://github.com/user-attachments/assets/c28fbb14-92e2-4c6e-9d27-491e4de76b21" /> with the permission policy <img width="1914" height="864" alt="Permission policy" src="https://github.com/user-attachments/assets/e6abf55c-aef9-49bb-854e-8755ffd2b889" /> to connect.

10) Finally The NAT Gateway so our Instances can access the internet for updates and patches but not vice-versa<img width="1562" height="334" alt="NAT-GW" src="https://github.com/user-attachments/assets/19f5c337-f485-4ffa-bff7-6065003b4318" />

























