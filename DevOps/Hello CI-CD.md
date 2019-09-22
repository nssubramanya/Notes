# Hello CI-CD

## GIT Setup
### Create Repository on GitHub
https://github.com/nssubramanya/hello-ci-cd.git

### Get Repo on Local machine
#### Method #1: Clone Repo
```
$ git clone https://github.com/nssubramanya/hello-ci-cd.git
Cloning into 'hello-ci-cd'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
Checking connectivity... done.

```
#### Method # 2: Start with Empty Repo

```
$ mkdir hello-ci-cd
$ cd hello-ci-cd
```

```
$ git init
$ git config --local user.name "Subramanya N S"
$ git config --local user.email "subramanya.ns@gmail.com"

$ git remote add origin https://github.com/nssubramanya/hello-ci-cd.git

$ git remote -v
origin	https://github.com/nssubramanya/hello-ci-cd.git (fetch)
origin	https://github.com/nssubramanya/hello-ci-cd.git (push)

$ git pull origin master
From https://github.com/nssubramanya/hello-ci-cd
 * branch            master     -> FETCH_HEAD

$ git log
commit 8185ba760fefd47a0433903df34dd3b723676406
Author: Subramanya Narasandra <5724545+nssubramanya@users.noreply.github.com>
Date:   Thu Jul 25 19:15:29 2019 +0530

    Initial commit

```

### Create Branch `dev`

## Create Backend Services Project

### Create Project
Go to `https://start.spring.io`

#### Create New Project
* Project: Maven Project
* Language: Java
* Spring Boot: 2.1.6 (latest)
* Project Metadata:
	- Group: `com.subbu.cicd`
	- Artifact: `hello-services`
	- Name: `hello-services`
	- Description: Demo project for Backend CI-CD`
	- Package Name: `com.subbu.cicd.hello-services`
	- Packaging: `Jar`
	- Java: `8`
Dependencies: Web, Devtools

This will be downloaded as a Zip File

Extract the file in to directory: `hello-ci-cd\`

### Create `.gitignore` file for Backend
1. Go to `gitignore.io`
2. Specify `Java`, `Java-Web`, `Maven`, `Eclipse`
3. Click on Create button to create the file contents
4. Copy paste the content to new file `hello-ci-cd/hello-services/.gitignore`

### Import Maven project in to Eclipse
1. File->Import Project->Existing Maven Projects
Select the folder and see that pom.xml is automatically selected.

2. Change Version to 2.1.4 in <parent> tag. If not, Eclipse throws an error
3. Right click on project->Maven->Update Project


### Change Default port from 8080 to 9000
Local Jenkins will run on 8080, so change the port of the application

1. In `src/main/resources/application.properties` add the code:
`server.port=9000`

### Add Code for default '/' handler
In folder `src/main/java/com/subbu/cicd/helloservices`, add new file `HelloController.java`

```
package com.subbu.cicd.helloservices;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {
	
	@GetMapping("/")
	public String sayHello() {
		return "Hello\n";
	}
}
```


### Build and Verify Services Code
```
$ mvn package
or 
$ mvn install
```

__Run__

```
$ mvn spring-boot:run
```

__Test__

```
$ curl -G http://localhost:9000/
Hello
```

### Commit Backend code

```
$ git branch dev
$ git checkout dev
$ git status
On branch dev
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.gitignore
	hello-services/

nothing added to commit but untracked files present (use "git add" to track)

$ git add .
$ git status
On branch dev
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   .gitignore
	new file:   hello-services/.gitignore
	new file:   hello-services/.mvn/wrapper/MavenWrapperDownloader.java
	new file:   hello-services/.mvn/wrapper/maven-wrapper.properties
	new file:   hello-services/HELP.md
	new file:   hello-services/mvnw
	new file:   hello-services/mvnw.cmd
	new file:   hello-services/pom.xml
	new file:   hello-services/src/main/java/com/subbu/cicd/helloservices/HelloController.java
	new file:   hello-services/src/main/java/com/subbu/cicd/helloservices/HelloServicesApplication.java
	new file:   hello-services/src/main/resources/application.properties
	new file:   hello-services/src/test/java/com/subbu/cicd/helloservices/HelloServicesApplicationTests.java


```

### TODO: TDD for developing REST Service
### TODO: Setup JIRA and put Tasks
### Commit code

```
$ git commit -m 'Added hello-services Spring-boot project, changed port to 9000, basic testing done'
[dev 7216cc9] Added hello-services Spring-boot project, changed port to 9000, basic testing done
 Committer: Subramanya Narasandra <subramanyans@Subramanyas-MacBook-Pro-3.local>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 12 files changed, 785 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 hello-services/.gitignore
 create mode 100644 hello-services/.mvn/wrapper/MavenWrapperDownloader.java
 create mode 100644 hello-services/.mvn/wrapper/maven-wrapper.properties
 create mode 100644 hello-services/HELP.md
 create mode 100755 hello-services/mvnw
 create mode 100644 hello-services/mvnw.cmd
 create mode 100644 hello-services/pom.xml
 create mode 100644 hello-services/src/main/java/com/subbu/cicd/helloservices/HelloController.java
 create mode 100644 hello-services/src/main/java/com/subbu/cicd/helloservices/HelloServicesApplication.java
 create mode 100644 hello-services/src/main/resources/application.properties
 create mode 100644 hello-services/src/test/java/com/subbu/cicd/helloservices/HelloServicesApplicationTests.java
```

### Adding UserName & E-Mail

```
$ git config --local user.name "Subramanya N S"
$ git config --local user.email "subramanya.ns@gmail.com"
```

__Status after__

```
$ git status
On branch dev
nothing to commit, working directory clean

$ git log
commit 0e6c0bd4b4d3e415e5d37c64baf2c06a4f68e42c
Author: Subramanya N S <subramanya.ns@gmail.com>
Date:   Thu Jul 25 22:32:41 2019 +0530

    Added hello-services Spring-boot project, changed port to 9000, basic testing done

commit 8185ba760fefd47a0433903df34dd3b723676406
Author: Subramanya Narasandra <5724545+nssubramanya@users.noreply.github.com>
Date:   Thu Jul 25 19:15:29 2019 +0530

    Initial commit

```
### Setting up GitLab
- Take the same SSH Keys created to access Git Hub
- Edit `~/.ssh/config` and put the following code

```
Host gitlab.com
	IdentityFile ~/.ssh/subbu-git
	IdentitiesOnly yes
ServerAliveInterval 120
```
__Change remote from GitHub to GitLab__

```
$ git remote rename origin github
$ git remote add gitlab git@gitlab.com:subramanya.ns/hello-ci-cd.git
$ git push -u origin --all
```

__Display the Remote Branches__

```
git remote -v
github	https://github.com/nssubramanya/hello-ci-cd.git (fetch)
github	https://github.com/nssubramanya/hello-ci-cd.git (push)
gitlab	git@gitlab.com:subramanya.ns/hello-ci-cd.git (fetch)
gitlab	git@gitlab.com:subramanya.ns/hello-ci-cd.git (push)
```

Unfortunately, the latest git Pushed all the branches, including `dev` and feature branches

__Display all branches__

```
git branch -a
* add-backend-project
  dev
  master
  remotes/github/HEAD -> github/master
  remotes/github/master
  remotes/gitlab/add-backend-project
  remotes/gitlab/dev
  remotes/gitlab/master
```
### Deleting Remote Branch

Deleting remote branch will  not work with `git branch -d`

Delete the branch via UI on Gitlab
After deletion, branch still shows up on Local. Hence, pruning is required.
`git remote prune <origin>`

```
$ git remote prune gitlab
Pruning gitlab
URL: git@gitlab.com:subramanya.ns/hello-ci-cd.git
 * [pruned] gitlab/add-backend-project
```

### Merge to Dev and delete Feature Branch

__Diff `dev` branch and 'add-backend-project` feature branch__

```
$ git checkout dev
Switched to branch 'dev'
Your branch is up-to-date with 'gitlab/dev'.
```
__Merge__

```
$ git merge add-backend-project
Updating 8185ba7..dec9b54
Fast-forward
 .gitignore                                         |   1 +
 hello-services/.gitignore                          | 114 ++++++++
 .../.mvn/wrapper/MavenWrapperDownloader.java       | 114 ++++++++
 .../.mvn/wrapper/maven-wrapper.properties          |   1 +
 hello-services/HELP.md                             |  16 ++
 hello-services/mvnw                                | 286 +++++++++++++++++++++
 hello-services/mvnw.cmd                            | 161 ++++++++++++
 hello-services/pom.xml                             |  49 ++++
 .../subbu/cicd/helloservices/HelloController.java  |  13 +
 .../helloservices/HelloServicesApplication.java    |  13 +
 .../src/main/resources/application.properties      |   1 +
 .../HelloServicesApplicationTests.java             |  16 ++
 12 files changed, 785 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 hello-services/.gitignore
 create mode 100644 hello-services/.mvn/wrapper/MavenWrapperDownloader.java
 create mode 100644 hello-services/.mvn/wrapper/maven-wrapper.properties
 create mode 100644 hello-services/HELP.md
 create mode 100755 hello-services/mvnw
 create mode 100644 hello-services/mvnw.cmd
 create mode 100644 hello-services/pom.xml
 create mode 100644 hello-services/src/main/java/com/subbu/cicd/helloservices/HelloController.java
 create mode 100644 hello-services/src/main/java/com/subbu/cicd/helloservices/HelloServicesApplication.java
 create mode 100644 hello-services/src/main/resources/application.properties
 create mode 100644 hello-services/src/test/java/com/subbu/cicd/helloservices/HelloServicesApplicationTests.java
```
__Delete Feature Branch__

```
$ git branch -d add-backend-project

```
### Integrate Checkstyle Plugin

#### Maven Checkstyle Plugin
Look for Maven Checkstyle Plugin on Maven Central
`https://mvnrepository.com/artifact/org.apache.maven.plugins/maven-checkstyle-plugin`

Check-style plugin can be used in following Phases-

1. Validate
1. Build
1. Verify
1. Site/Reporting

In Validate Phase, it can be called with command `mvn validate`.


##### Checkstyle Reporting
Run Checkstyle using command `mvn site`. This will generate the checkstyle report.

Add Checkstyle plugin in `<reporting>` section of `pom.xml`


#### Failing a build using Checkstyle

#### Using google_checks.xml

### Using Custom rules in Checkstyle


### Using Checkstyle Plugin with Jenkins

## Create Frontend React Application
