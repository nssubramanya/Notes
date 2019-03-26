# EC2 - Elastic Cloud Compute
* EC2 Instances - On Demand, Spot, Reserved, Dedicated
* Instance Types - Compute Intensive, Memory Intensive, General Purpose, Graphics, TBD, How to Determine Instance Types to use
* EC2 Dashboard
* EC2 Instance Operations
	- Instance State Change - Start, Stop, Reboot, Terminate

* Pricing
* Launching in Regions & Availability Zones
* IP Address - Elastic IPs, Private IPs, Secondary Private IPs
* 
* Instance Security - Security Group, VPC, Subnet
* Connecting to EC2 Instance - Direct connection, SSH using Keypairs
* Associating IAM Roles for EC2
* Monitoring EC2 Instances using CloudWatch
* EC2 Tags - Create, Display, Practical Uses, Tagging Strategies
* AMI
* Launch Templates



## EBS (Elastic Block Storage)
* EBS Volumes
* Lifecycle Manager
* Snapshots


## Managing Software On EC2 Linux Instance
Amazon Linux2 instances manage their softare using 'yum' package manager. 
`sudo yum update`
OR
`screen` to create a screen session to recover from SSH Disconnections during update
`sudo yum update -y` Automatically Approve and Install updates
`sudo yum update -y <Package Name>` to update only a single package
`screen -ls` list screens
`screen -r <Screen Number>` Reconnect to Screen
`exit` to Close the session

Reboot the EC2 Instance post update

## Installing HTTPD
`sudo yum install httpd -y`
`sudo systemctl enable httpd`
`sudo systemctl is-enabled httpd`
`sudo systemctl start httpd`
`sudo usermod -a -G apache ec2-user` - Add ec2-user to apache users group
`groups` - Check whether ec2-user is part of apache group
`sudo chown -R ect-user:apache /var/www`


