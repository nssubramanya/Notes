# Naming Conventions
EC2 Instance: 
Security Group:  <IAM User Name>_SG_<Region Name> - me_SG_uswest2
Key Pair:
RDS Instance:
DynamoDB Instance:
S3 Buckets:
VPC:
Subnet: 
CDNs:
Route53 Hosted Names:




# Security Group CIDRs
HTTP, Anywhere, 0.0.0.0/0
HTTPS, Anywhere, 0.0.0.0/0
SSH, MyIP, <Your External IP>/32
SSH, <MyIP Range> say 203.0.113.0/24. This allows for 256 IPs


# Never do This
* Allow SSH from 0.0.0.0/0 (Anywhere) for a EC2 Instance
* 