# Maven
## About Maven
### What is Maven
* Maven is a **Yiddis** word, meaning _accumulator of knowledge_
* Began as an attempt to simplify Build Processes in Jakarta Turbine project

### Problems in the project
* Multiple projects with their own Ant build files, with no consistency
* JARs were checked-in to CVS

### Maven Objectives
* Make build process easy
* Provide a uniform build system
* Provide quality project information
* Provide guidelines for best practices development
* Allow transparent migration to new features

## Life without Maven
### Dependencies-JARS
* Dependent JARs are added manually via Eclipse Add JARs feature and stored in Project. Reference is in project, but actual JAR file may be missed out
* JARs have to be checked-in to Version Control
* Re-downloading of necessary JARs on multiple projects - With Maven, JARs downloaded once are in Local Repository and hence re-used

### Life-cycle
* Provides multiple Life-cycle and Phase triggers

### Standard File Structure
* Projects usually are structured in myriad different ways and without proper documentation, new comers struggle to find out what is where. With Maven, though structure opinionated, one can always expect code to be a certain defined struture - Ex: src, test, etc.


## Download & Install Maven
Download from following location: http://maven.apache.org/download.cgi

### On Mac - using Homebrew

```
$ brew update 	# Fetch latest version of homebrew and formula		
$ brew search maven	# Searches all known formulae for a partial or exact match
$ brew info maven	# Displays information about given formulae
$ brew install maven	# Installs maven formula
$ brew cleanup	# Remove any older versions from cellar
```

### Download and install
```
$ wget http://mirrors.estointernet.in/apache/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz
$ tar xzvf apache-maven-3.6.1-bin.tar.gz
$ sudo mv apache-maven-3.6.1 /usr/local/maven
```

#### Setup Exports in `~/.bash_profile`

```
export M2_HOME=/usr/local/maven
export M2=$M2_HOME/bin
export PATH=$M2:$JAVA_HOME/bin:$PATH
```

## Running Maven
Show Maven Version Number

```
$ mvn --version
Apache Maven 3.5.4 (1edded0938998edf8bf061f1ceb3cfdeccf443fe; 2018-06-18T00:03:14+05:30)
Maven home: /usr/local/maven
Java version: 1.8.0_66, vendor: Oracle Corporation, runtime: /Library/Java/JavaVirtualMachines/jdk1.8.0_66.jdk/Contents/Home/jre
Default locale: en_US, platform encoding: UTF-8
OS name: "mac os x", version: "10.14.5", arch: "x86_64", family: "mac"
```

## Create Maven Project
Maven Projects need the following information to create a project
1. Group ID
2. Artifact ID
3. Archetype 
4. Architeype Version


### Maven Architypes

## Maven Life-cycles
Three Main Life-cycles

1. default - Used for _*Build*_ and *_Deploy_*
2. clean - Used for cleaning files and folders produced by Maven
3. site - Used for generating Project documentation

## Maven Phases
Life-cycles are assocaited with Phases
### Phases of `default` lifecycle
1. _validate_: Validates that all project information is available and correct
2. _process-resources_: Copies project resources to the specified destination to package
3. _compile_: Compiles source Code
4. _test_: Runs Unit-tests within a suitable framework
5. _package_: Packages compiled code in suitable format
6. _integration-test_: Process package in Integration Test environment
7. _verify_: Verify if package is valid
8. _install_: Installs package in local repository
9. _deploy_: Installs final package in configured repository

* Specifying Life-cycle is not mandatory

### Phases of `clean` lifecycle
1. _clean_: Removes all files and folders created by Maven as part of the build

### Phases of `site` lifecycle
1. _site_: Generates project documentation, which can be published, as well as a template that can be customized further

### Plugins & Goals
Work in life-cycle and phases are actually executed by Maven Plugins. Each Plugin exposes goals.

* A Plugin-goal is a specific task that contributes to builing and managing of project. 
* Plugin Goals can be bound to 0 or more build phases.
* Plugin goals need not always be bound to phases, but can be executed outside of life-cycle phases also.

Phase - Plugin, Goal
clean - clean:clean
site - site:site
process-resources - resources: resource
compile - compiler: compile
test - surefire: test
package - JAR: jar (depends on packaging type)
install - install: install
deploy - deploy: deploy

## Structure of Maven Project
## POM File and content
## Maven Repositories
## Maven Rules
## Maven Plugins
### Clean plugin
* Project artifacts are created in `target`
* `target` folder is usually deleted before new build
* `clean` is a separate life-cycle from `default`, so, `clean` must be explicity called to ensure working directory is removed

```
$ ls
pom.xml	src	target

$ mvn clean
[INFO] Scanning for projects...
[INFO] 
[INFO] -------------------< com.subbu.maven:simple-project >-------------------
[INFO] Building simple-project 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ simple-project ---
[INFO] Deleting /Users/subramanyans/Documents/GitHub/Playground/DevOps/Maven/simple-project/target
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 0.233 s
[INFO] Finished at: 2019-07-05T10:37:28+05:30
[INFO] ------------------------------------------------------------------------

$ ls
pom.xml	src

```

#### Automatically Cleaning
To automatically execute `clean` goal as part of build process, we need to define it in POM file

build -> plugins -> plugin -> executions -> execution -> goals -> goal

## Resources
[Good Set of Maven ToDos] (http://www.avajava.com/tutorials/categories/maven)




