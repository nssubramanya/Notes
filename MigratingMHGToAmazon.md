## 1. Create GIT Repository on AWS Code Commit
## 2. Clone the repository to local

`git clone https://git-codecommit.ap-south-1.amazonaws.com/v1/repos/mHealthGenie`



# MySQL
## Get MySQL End Point Name
Get it from RDS Dashboard

## Configuration
Use Default VPC
In Security Group, add personal Laptop/desktop IP to access DB
Ensure that we enable remote access to DB
TODO: In production setup, remote access needs to be disabled. Read-up how to do production setup
## Securing MySQL

## Connect to mysql database
mysql -h mhealthgenie.cmjitp17z0gv.ap-south-1.rds.amazonaws.com -u mhgadmin -p

## Import Database
mysql -h mhealthgenie.cmjitp17z0gv.ap-south-1.rds.amazonaws.com -u mhgadmin -p < 182ServerDb.sql


# EC2
## Configuration Options
- VPC
- Security Groups

## Securing EC2

### System Update
#### Become Root
`$ sudo su`

`$ sudo yum update`

### Apply Hardening Rules

## Software Installation
### MySQL Client
`$ sudo yum install mysql` 
This will install mariadb and also all clients. 
TODO: Find out way to install only mysql client

### Tomcat
> https://www.digitalocean.com/community/tutorials/how-to-install-apache-tomcat-7-on-centos-7-via-yum

`$ sudo yum install tomcat`
`$ sudo yum install tomcat-webapps tomcat-admin-webapps`
`$ sudo systemctl enable tomcat`

#### Configure ports of Tomcat
`$ sudo systemctl start tomcat`

#### Allow 8080 port access



## mHealthGenie
> How to deploy a WAR: https://www.baeldung.com/tomcat-deploy-war

