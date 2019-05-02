# Jenkins
What is Jenkins?
What are the benefits of using Jenkins?
What are the prerequisites for using Jenkins
## Mention some useful Jenkins Plugins
* Version Control - Git
* Build - Maven 2 project
* Continous Deployment - Ansible
* Continous Testing - Selenium
* Continuous Monitoring - Nagios
* Others - Amazon EC2, Copy Artifact, HTML Publisher, Join, Green Balls

## Mention commands used to start Jenkins Manually
## Explain how to setup a Jenkins Job
## Explain how to create backup and copy files in Jenkins
## How will you secure Jenkins?
## Relation between Hudson and Jenkins
## What to do when build is broken in Jenkins
## How to schedule builds in Jenkins
## Difference between Maven, Ant, Jenkins
## SCM tools supported by Jenkins

Overview
## Installation
Jenkins needs Java as a pre-requisite

### Install Java on CentOS
* Get the Java Download URL (JDK) - `https://www.oracle.com/technetwork/java/javase/downloads/`

* Download the JDK RPM

```
wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/12+33/312335d836a34c7c8bba9d963e26dc23/jdk-12_linux-x64_bin.rpm
```
* Install the RPM

```
sudo yum install -y jdk-12_linux-x64_bin.rpm
```

* Verify JDK Version

```
java -version
```
### Install Jenkins
1. Add Jenkins repo using the following command

```
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
```

2. Import a Key file from Jenkins-CI to enable installation from the package

```
sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key
```

3. Install Jenkins

```
sudo yum install jenkins -y
```

4. Start Jenkins as a service

```
sudo service jenkins start
```

### How to install Jenkins so that it starts automatically

## Configuring Jenkins
### Connecting to Jenkins
Use the following in Browser
```http://<your_server_public_DNS>:8080```

### Unlocking Jenkins first time
When prompted, enter password found in ```/var/lib/jenkins/secrets/initialAdminPassword```


## References:
https://dzone.com/articles/learn-how-to-setup-a-cicd-pipeline-from-scratch



