# JMeter
## JMeter Installation & Configuration
### Dependencies
### Installation
```
$ ls -l `which jmeter`
lrwxr-xr-x  1 subramanyans  admin  31 Dec 26 12:51 /usr/local/bin/jmeter -> ../Cellar/jmeter/5.0/bin/jmeter
```
### Launch
```
$ open `which jmeter`
```
### Command Line Mode

```
./jmeter -n -t [path to test script] -l [path to results files]
```
### Install Plugin Manager
### Launch & Use Plugin Manager

## Running Simple Tests
### Test Plan
### ThreadGroups
#### Name
#### Number of Threads/Users
#### Ramp-up Period
#### Loop-count
#### Scheduler Configuration
#### Action on Sampler Error
##### Continue
##### Start Next Thread Loop
##### Stop Thread
##### Stop Test
##### Stop Test Now
### Sampler
#### HTTP Request
### Timer
#### Constant Timer
#### Uniform Random Timer
### Response Assertion
### View Results Tree
 