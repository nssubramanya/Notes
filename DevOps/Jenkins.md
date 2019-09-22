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
Following link has All Installation Methods listed - [Jenkins Installation Guide](https://jenkins.io/doc/book/installing/)

Ensure `wget` is present. otherwise,

```
$ sudo yum install -y wget
```

Jenkins needs Java as a pre-requisite

### Install Java on CentOS
* Get the Java Download URL (JDK) - `https://www.oracle.com/technetwork/java/javase/downloads/`

* Download the JDK RPM

```
$ wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/12+33/312335d836a34c7c8bba9d963e26dc23/jdk-12_linux-x64_bin.rpm
```
* Install the RPM

```
$ sudo yum install -y jdk-12_linux-x64_bin.rpm
```

OR

```
$ sudo yum install -y java-1.8.0-openjdk-devel
```

* Verify JDK Version

```
$ java -version
```
### Install Jenkins
1. Add Jenkins repo using the following command

```
$ sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
```

2. Import a Key file from Jenkins-CI to enable installation from the package

```
$ sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key
```

3. Install Jenkins

```
$ sudo yum install jenkins -y
```

4. Start Jenkins as a service

```
$ sudo service jenkins start
```

### How to install Jenkins so that it starts automatically

```
$ systemctl status jenkins
$ systemctl enable jenkins
$ systemctl start jenkins
$ systemctl status jenkins
```
## Configuring Jenkins
### Connecting to Jenkins
Use the following in Browser
```http://<your_server_public_DNS>:8080```

### Unlocking Jenkins first time
When prompted, enter password found in ```/var/lib/jenkins/secrets/initialAdminPassword```

### Listing RPM Packages

```
rpm -qa | grep jdk
```

### Removing RPM Packages

```
rpm -e <package>
```
## Other ways to Use Jenkins
### Download war
* Download WAR file from `http://mirrors.jenkins.io/war-stable/latest/jenkins.war`
* Run `java -jar jenkins.war`
* Browse to `http://localhost:8080` to get Jenkins Unlock page
* To change HTTP Port, use `java -jar jenkins.war --httpPort=9090` for port on 9090 instead of 8080

### Install with Tomcat
### Jenkins with Docker

## Testing in Jenkins
### Install Ant
```
$ which ant
/usr/bin/which: no ant in (/usr/local/rvm/gems/ruby-2.4.1/bin:/usr/local/rvm/gems/ruby-2.4.1@global/bin:/usr/local/rvm/rubies/ruby-2.4.1/bin:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/usr/local/rvm/bin:/home/cloud_user/.local/bin:/home/cloud_user/bin)

$ sudo yum install ant and ant-junit
$ ant -version
```

### Ant Installation Folder
ANT is installed in `/usr/share/ant`. However, the ANT binaries are available in `/bin`.

### Update ANT location in Jenkins
Jenkins -> Global Tool Configuration -> Ant Installations

* Un-check "Install Automatically"
* Give Ant Name - Ex: "Ant1.9.4"
* Give ANT_HOME: "/usr/share/ant"

## Security
### Authentication
#### LDAP

### Authorization

## Distributed Builds
## Configuring Master
### Build Process
* Configure Maven - M3, Install Maven
* Create Freestyle Project
* Get Source-code from GIT
* Execute Maven step - 
* Execute Build step - bin/makebuild
* Archive index.jsp
* Enable Fingerprinting 

### Setup Slave

## Promoting Builds

## Pipeline Builds
There are 2 types of Pipelines - Decorated Pipeline and Scripted Pipeline

### Decorated Pipeline
* Mostly a Free-style project converted to Pipeline
* This creates a `Jenkinsfile` that is checked in to SCM
* 
## Configuring Slaves

## Jenkins & Docker

## Integrations
### Software Configuration Management Tools
#### GIT
#### Subversion

### Static Analysis Tools
#### Checkstyle
#### PMD
#### Find Bugs

### Code Coverage Tools
#### Cobertura

### Build Tool
#### Maven

### Unit Test Tools
#### JUnit

### Integration Testing Tools
#### Selenium

### Performance Testing Tools
#### JMeter
#### Blaze Meter

### Communication Tools
#### E-Mail
#### Slack

### IDE Integration
#### Eclipse

### Reporting
#### 

### Monitoring Tools

### 

## References:
https://dzone.com/articles/learn-how-to-setup-a-cicd-pipeline-from-scratch

## Jenkins Certified Exam
* [Passing the Certified Jenkins Engineer Exam](https://medium.com/@denniswebb/jenkins-cje-e82dc00fc640)
* [Study Guide for Certified Jenkins Engineer Exam](https://github.com/smartrus/certified-jenkins-engineer-study-guide/blob/master/certified-jenkins-engineer.md)

## ToDo - Jenkins in Production
### Jenkins for High Availability & Scalability
Master-Slave Mode

#### Preparing Build Server for Jenkins
Hardware config for Master & Slave Servers - CPU, Memory, I/O, DB Connectivity etc.

* Builds can be run in parallel based on number of Executors
* Rule of thumb, you will need 1 Processor per parallel build
* Preferably reserve Build server for running Builds continuously. Don't use the same machine as App Server/Test Server/DB Server etc.

* Memory usage of CI Server will be spiky - Jenks will be creating additional JVMs for build jobs and these need memory
* Other strategy is to use Build slaves for running build jobs

### Users
* Create a special User Group `build` and User `jenkins` for running builds

```
$ sudo groupadd build
$ sudo useradd --create-home --shell /bin/bash --groups build jenkins
```

* Configure JAVA_HOME and add it to path

### Jenkins Home Directory
This is the place where Jenkins stores its data-

- Build Server Configuration
- Build Jobs
- Build Artifacts
- User Accounts
- Plugins

This directory needs lot of space.

Default Jenkins Home directory: `/home/<user>/.jenkins` or c:\Users\<user>\.jenkins


```
export JENKINS_BASE=/usr/local/jenkins  // location of Jenkins WAR file
export JENKINS_HOME=/var/jenkins-data   // Location of Jenkins Home Directory
java -jar ${JENKINS_BASE}/jenkins.war
```

How many jobs can run?
Where to store the Artifacts?

Running the same with Docker
Running Jenkins behind NGinx

### Monitoring performance
Build Performance
Hardware Performance of Jenkins Master/Slaves

### Metrics

### Build Staggering
Compilation
Document Generation
Unit & Integration Testing

Which servers to take these up?
When to run these type of jobs?

### Securing 
Users & User Groups

### Jenkins on the Cloud
Jenkins with AWS
Jenkins with Google Cloud
Jenkins with Azure
Jenkins in Private/Hybrid Cloud

### Backing Up

### Upgrading Jenkins

