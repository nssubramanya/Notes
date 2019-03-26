# Certified Developer Associate 2018
### Experiences of Passed Candidates

## S3
* CORS
* Encryption
* S3 Encryption Header
* API Calls
* S3 Performance Optimization
* [Optimizing S3 Key files names for Heavy load] (http://docs.aws.amazon.com/AmazonS3/latest/dev/request-rate-perf-considerations.html))
* Hosting Static Site
* Default 100 Buckets
* APIs - CreateBucket, DeleteBucket, GetBucketPolicy, CopyObject, AbortMultipartUpload

## EC2
* Launching EC2 Instances
* Encrypting EC2 Instances
* EC2 Snapshots
* AMIs in Region
* EBS Vs Instance Store
* AMI: DescribeImages, CreateImage, RegisterImage
* EBS: Attach-Volume, Add-EC2Volume

## SQS
* Visibility Timeouts
* Message Delivery
* Min/Max timeouts
* Long Polling
* Protocols Used

## SNS
* SNS Message Format

## DynamoDB
* Partition Keys
* Local/global Secondary Indexes
* Calculate Read/Write Throughput
* ProvisionedThroughputExceeded Exception
* API Calls
* [Optimizing DynamoDB Operations] (http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/QueryAndScanGuidelines.html))
* How Global & Local Indeces related to Provisioned Throughput
* Hash and Range Keys
* How to optimize for specific queries for best performance

## IAM
* Users
* Groups
* Roles
* Inline policies
* Restricting access to Resources (policies, ACLs)
* Authenticating LDAP with IAM - LDAP Integration

## VPC
* Subnets
* Routing Tables
* NAT Gateways

## ELB
* [ELB and Session Cookies] (http://docs.aws.amazon.com/ElasticLoadBalancing/latest/DeveloperGuide/elb-sticky-sessions.html)

## CloudFormation
* Ability to Read and Understand Simple Template
* Methods used in Templates
* Sections - Output Section
* Functions used

## Elastic Beanstalk
* Resources that EBS can provision - ASG, ELB, EC2, RDS, SNS, S3

## Lambda
* Concurrency & Scale Model
* [AWS Lambda Best Practices] (https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html)

## SNS
* Registering Devices for Push Notifications

## KMS
* Core KS
* API to generate Data Key
* All places where Encryption is used

## STS
* How Identity Broker integrates with STS
*

## SWF
* API Calls
* 

## API Gateway

## CodeCommit, CodeDeploy, CodePipeline, Cognito, X-Ray
* Read FAQs

## 
## CloudWatch & CloudTrail
* Know backwards and forwards!
* 
## Kinesis


## Elasticache
* Differences b/w Redis and MemcacheD
* 
## Misc
* Service Limits for S3, DynamoDB, EC2, SNS, SQS
* API Calls for all services
* All WhitePapers
* All FAQs
* AWS Reinvent TAlks on VPC, EC2, S3, RDS
* Monitoring EC2 with Custom Metrics from ACG SysOps Administrator
* Montitoring/Metrics/Logging Sections from Certified DevOps Engineer-Professional
* Security/Govenrence/Validation section from Devops Engineer Professional
* How CloudWatch interacts with each and every Service - Features, Permissions, Errors, APIs

## Questions & Resources
* https://quizlet.com/256610752/aws-developer-practice-test-1-flash-cards/
* https://blog.cloudthat.com/sample-questions-for-amazon-web-services-certified-developer-associate-certification/
* __TheCertSchool.com__
* __AWS Practice Test__


## Exam Notes
* http://clusterfrak.com/notes/certs/aws_deva_notes/


## Exam Tips
* https://acloud.guru/forums/aws-certified-developer-associate/discussion/-KBkBPMHpN2ITSH1oDTO/passed-with-90-my-exam-tips
* https://acloud.guru/forums/aws-certified-developer-associate/discussion/-KUdI5f2LNbi4wvK7v4I/how_to_pass_aws_certified_deve
* https://medium.com/@ozdemircili/how-i-passed-3-aws-certifications-in-26-days-without-hands-on-experience-and-saved-24-000-8b2fec392db0
* 

## Dumps
* http://www.amazondumps.us/aws-certified-developer-associate.html
* 

## Misc
AMI: DescribeImages, CreateImage->RegisterImage

S3: 100 buckets (default)

Attach EBS to EC2 (AWS CLI): attach-volume

Attach EBS to EC2 (Windows Powershell): Add-EC2Volume

S3 API common starts:

AbortMultipartUpload

CompleteMultipartUpload

CopyObject

CreateBucket

DeleteBucket

DeleteObject

GetBucketPolicy

Encryption: 256-bit Advanced Encryption Standard (AES-256)

AWS platform: 16 Regions, 44 AZ

Display AMI: DescribeImages

Instance Metadata: http://169.254.169.254

DynamoDB Throughput Exceeded: ProvisionedThroughputExceededException

DynamoDB Item size: 400KB

DynamoDB Local+Global Secondary Index: 5 for each

DynamoDB Max Tables Per: 256 tables

DynamoDB Attributes (column): Unlimited Region

DynamoDB doesn’t consume capacity units if it’s just modifying Table

DynamoDB (Scan/Query): ProjectionExpression

DynamoDB query item by partition: GetItem

DynamoDB query multiple item (up to 100 items + Max 16MB): BatchGetItem

DynamoDB scan data: 1MB

DynamoDB Reserved Capacity: 100 Capacity

DynamoDB list up to 100 tables: ListTables

SQS message retained: 14 days

SQS message: 256 KB of text in any format (10 items max)

SQS timeout: 30 seconds (default) 12 hours (max)

SQS long polling: 20 seconds(default/max) 1 sec(min)

SQS is PCI DSS certified

SQS/SNS visibility: ChangeMessageVisiblity

SQS/SNS delete: DeleteMessage

SNS pending: 3 days

SNS Topic: 100,000

SNS endpoint API: CreatePlatformEndPoint

SWF retention: 1 year

SWF Domain: 100 per account (containers for segregating app resources)

SWF Workflow/activity-10,000

SWF Request size: 1MB

SWF Open: 1000

CloudFormation get Output Data: Fn:GetAtt

CloudFormation List all Resources: ListStackResources

CloudFormation stack waiting: WaitCondition

Cloud Formation stack: 200

Cloud Formation Template: No limit

Cloud Formation Parameter: 60

Subnet VPC: 200

Lambda Default timeout: 3 sec

400 - Server does not understand the request. (MissingAction, MissingParameter, incompleteSignature, invalidParameterValue, incompleteBody)

403 - forbidden (Ex: AccessDenied, InvalidClientTokenID, MalformedQueryString, invalidObjectState)

404 - The page URL request cannot be found due to the Server Down Time or Broken Links. (Ex: NoSuchBucket, NoSuchVersion,NoBucketPolicy)

409-

BucketAlreadyExists

InvalidBucketState

BucketNotEmpty

OperationAborted

RestoreAlreadyInProgress



