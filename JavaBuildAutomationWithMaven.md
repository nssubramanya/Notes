# Java Build Automation with Maven

Dependencies to install Maven
## Maven Download & Install
* ```wget http://mirror.olnevhost.net/pub/apache/maven/binaries/apache-maven-3.2.1-bin.tar.gz```
* ```tar xvf apache-maven-3.2.1-bin.tar.gz```
* Edit ~/.bash_profile to put the following-
```
export M2_HOME=/usr/local/apache-maven/apache-maven-3.2.1
export M2=$M2_HOME/bin
export PATH=$M2:$PATH
```
* Confirm that maven works- ```mvn --help```

Maven Dependencies
Maven Create Project
Maven Clean
Maven Compile
Maven Test
Maven Package
Maven Install
