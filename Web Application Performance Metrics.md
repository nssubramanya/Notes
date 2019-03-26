# Web Application Performance Metrics
## Resources
* [Stackify - Application Performance Metrics](https://stackify.com/application-performance-metrics/)

## User Satisfaction/Apdex 
- Apdex Score means Application Performance Index Score
- Industry standard for tracking relative performance of application
- Goal is specified for how long a web-request should take
- Results are bucketed into Satisfied (fast), Tolerating (sluggish), Too slow and Failed
> - Appdex = (SatisfiedCount + (ToleratingCount/2))/TotalSamples


## Average Application Response Time
### Response Time
- The amount of time an application takes to return a request to the user. 
- Measured in Seconds or Milli-seconds
- Response Time = Network Latency + Server Processing Time
- Application should strive to minimize this time

Should be Measured under different conditions
- Load conditions - Number of concurrent users, Number of transactions
- Geographic Location
- Complexity of information sent

Averages can be deceiving as average of extremes (Very Negative and Very Positive) can give impression as if everything is fine (Neutral)

## Peak Response Time
Helps identify areas where performance can be improved.
Average might be within limit but all those Requests that are exceeding the threshold.

## Error Rates
- HTTP Error % - Number of web-requests that ended in Error
- Logged Exceptions - No. of Unhandled & logged errors from the app
- Thrown Exceptions - Number of exceptions thrown

Error rate in relation to load/stress (number of users/depletion of system resources)

## Number of Concurrent Users
Number of concurrent users application can support with Response time still within acceptable limits.

### Count of Application Instances (In-case of Auto-scaling)
In case app is set to auto-scaling, as user increase, new instances are spawned to manage the load.

App maintains Response time thresholds and supports many concurrent users, but at the cost of increased instances that inturn is costly.

So, COST for supporting 'n' concurrent users with acceptable response time.
 
## Request Rate
Number of Requests per second

Factors:
Requests for Static content
Requests for Dynamic content

Mapping of Response time against Request Rate is useful
Time-series evaluation of Request rate (what times of day, what days of week/month etc.) gives useful insights on user engagement


## App & Server Hardware Utilization
Usage of CPU, Memory, Network and Disk by both the Application and the Application Server

## Usage of other Resources
Other resource usage like Database, Cache, Load Balancers etc.
 

## Application Availability (Uptime)
How much time application is available
Usually measured in % Uptime (Ex: 99.9% etc.)

Detected via Per Minute Ping checks

## Throughput

## Garbage Collection Time
Amount of time spent for Garbage Collection in case of Java/.NET etc.

## Response Time
### Absolute Response Time
Total Time taken from instant User clicked a link or submitted a form until the response from server is rendered completely

### Percieved Response Time
- Absolute Response time for complex web pages may be very high
- Pages are progressively rendered using multiple by request/responses. 
- Appears to user that response was fast because user can do other activities
- It is the response time as perceived by users

### Server Processing Time
- Time taken by server to process the given input and generate output
- Varies based on type of request, complexity of operation, Server hardware and system load

### Rendering Time
- Time for Parsing response + Time to render
- Dependeds on complexity of data
- Depends on system load on user's device

### Network Latency
- Time for Request packets to travel from Client to Server + Time for response packets from Server to Client over network
- Depends on Location of User, Time of day, Network load

## Throughput
- Transaction is sequence of Request-Responses
- Throughput is number of transactions per unit time
- Depends on Server Hardware, System Load, Network Latency
- App should maximize throughput

## Utilization
- Ratio of Throughput of application relative to Maximum Capacity
- Ex: Number of Request/Responses handled in a minute to maximum capacity per minute
- Not desirable to operate above 80% utilization because requests are not evenly distributed and system should have free resources to handle spikes

## Robustness
- Measured by _Mean Time between Failures (MTbF)_
- Measure of how well app detects and handles various errors and exceptions
- Impacts availability

## Scalability
- Measures how well system can expand capacity when additional resources are added
- Is the system Vertically Scalable or Horizontally scalable?

## User Perception
- Response time must match User expectation
- Ex: Upto 6 seconds for a casual news site, Sub-seconds for financial trading app
- Req/Resp may be restructured to improve **Perceived Response Time**

## Cost
- System should consume fewer resources and save money

