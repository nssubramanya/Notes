# CI-CT-CD-CR Pipeline

## CI
Trigger: Source Code Check to GIT

* GIT triggers Jenkins
* Pull Source Code from GIT 
* Static Analysis - Checkstyle, FindBugs, PMD, Sonarcube
* Build using MAVEN - JAR/WAR
* Store build
* [UnitTest Infrastructure Provisioning]
* Run Unit Tests - JUnit
* Get Code Coverage - JaCoCo/Cobertura
* Generate Source Code References
* Generate Documentation & create Site
* [Unit Test Reports - Results, Coverage]
* [Integration Test Infra Provisioning - DB, Cache, Web Services, Docker etc. Using Ansible/Chef/Puppet]
* Run Integration Tests
* Store Integration Test Reports - Test Results, Coverage
* Store build in Binary Repository (S3/SonaType Nexus, Archiva etc.
* Performance Testing - BlazeMeter/jMeter
* Security/Penetration Testing
* Communication (Slack/RocketChat)