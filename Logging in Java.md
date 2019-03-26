# Logging in Java
## Why Logging is important
* Applications can't be debugged in productions; Only logs will be available to understand application flow and state
* Auditing
* Gathering statistics
* Business Intelligence



### Logging Options in Java
#### java.util Logging
#### Log4J
#### Log4J2
#### Logback
#### SLF4J - Simple Logging Facade for Java

# Logging Issues & Best Practices

## Logging Sensitive Information
* [OWASP provides this exclude-list](https://www.owasp.org/index.php/Logging_Cheat_Sheet#Data_to_exclude)
* __User Data__: *User Personal Info* like Personal Names, Telephone Numbers, E-mail Address, Government Identifiers, Health Information, Authentication Passwords, Secret Questions etc.; *User Financial Information* like Authentication Passwords, Credit-card Details, Information that user has opted out of collection
* __Application Details__: Application Source Code, Access Tokens, DB connection Strings, Unhashed Session Identifiers, File Paths, Network & Server Names/IP Addresses
* __JVM Log Forging__: Logging user provided data or data from untrusted external source in to log directly. Malicious attackers can enter corrupted data. Use ESAPI OWASP Enterprise Security API to encode data before logging
 
## Excessive Logging
* Too much logging and logging everything
* Problems - Performance impact, difficulty in searching and identifying relevant info

### Solutions
* Add Aspects where relevant
* Manage via configuration files
* TODO: Aspects & Config files

## Cryptic Log Messages
* Logging messages that lack specificity Ex: Operation Failed, Invalid Input etc.
* Use Timestamp, Log-level, Thread Name, Fully Qualified Class Name, Line Number?
* Set Log Statement Pattern in Configuration file. TODO: Experiment with Patterns

## Single Log File - No Log Rotation
* Log file will become very huge - Unmanageable
* Log Rotation strategies-
	* Create Log file each day with different name based on size
	* Rolling File appender to create log files at time intervals

## Incorrect Log Levels
* Use correct log levels - FATAL, ERROR, WARN, INFO, DEBUG, TRACE
* FATAL - Errors that cause application to crash or fail to start (Out of Memory etc.)
* ERROR - Technical issues that need to be resolved for proper functioning. Loss of functionality (Ex: DB Connection)
* WARN - Does not hamper functioning of app but causes inconvienience
* INFO - Messages that describe what's happening in the app - For Admin/Advanced User to quickly understand what was happening
* DEBUG - Detailed information with Parameters, Variable Values etc. For developer to debug
* TRACE - Method Entry/Exit etc.

* Control Logs dumped based on levels. Ex: specify bases as INFO/WARN in Logger property file
* TODO: Experiment this feature
* 
## Logging singe operations across multiple logs
## Plain Text Logging - Not JSON
## Impact on App Performance
## Loggint to stdout
## Log Retention
## Searching through Logs
## Other References
* [OWASP Logging Cheat Sheet](https://www.owasp.org/index.php/Logging_Cheat_Sheet)

# Java Logging Standards and Guidelines
[Java Logging Standards](https://wiki.base22.com/btg/java-logging-standards-and-guidelines-2361.html)
## Declaring Logger
## Method Entry/Exit Logging (Tracing)
## Object Instantiation
## Log Statement Format
## Log Levels Description
### FATAL
### ERROR
### INFO
### DEBUG
### TRACE



