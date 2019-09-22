# REST Services in Java Spring Boot

## Create Empty Spring application
* Use Spring Initilizr - Goto https://start.spring.io
* Copy to relevant folder
* Import Existing Project
* Run main application - app will start on http://localhost:8080


## Spring Topics
1. Intro to Spring Boot Starters
2. Spring Boot: Configuring Main Class
3. Embedded Tomcat Configuration
## Things to do with REST Applications
1. Start Application on Different Port than default port of 8080

## REST API Implementation
### GET
#### Query Parameters
### 
### POST
### DELETE
### UPDATE

## GET
### Returning HTTP 404 - Not Found when resource is not Found


## POST
### Returning Created Object URI from POST
If POST is successful in CREATING the Resource, it is advised to return the URI of the newly created resource along with HTTP Status code 201 - CREATED.

Java code for this purpose is shown below:

```
URI location = ServletUriComponentsBuilder
							.fromCurrentRequest()
							.path("/{id}")
							.buildAndExpand(s.getId())
							.toUri();
				
return ResponseEntity.created(location).build();
```

## Throwing Custom Exception from REST Services
Exception Details MUST be similar across projects. Some details can be - timestamp, message, details

### Create a new Package `Exceptions`
``` package com.subbu.springboot.collegerestapi.exceptions;```

### Create Custom Exception 
* Create custom Exception Class - Extending `RuntimeException` which is not CHECKED Exception
* Mark `@ResponseStatus() with appropriate Http Status

__File: StudentNotFoundException.java__

```
package com.subbu.springboot.collegerestapi.exceptions;

import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.ResponseStatus;

@ResponseStatus(HttpStatus.NOT_FOUND)
public class StudentNotFoundException extends RuntimeException {

	/**
	 * 
	 */
	private static final long serialVersionUID = 1L;

	public StudentNotFoundException(String message) {
		super(message);
		// TODO Auto-generated constructor stub
	}

}

```
### Throw Custom Exception
* Throw the custom exception from Controllers in case of exception condition
* Pass approriate message
```
if (student == null) {
			throw new StudentNotFoundException("id-" + id);
```

### Create Generic Exception Class across the App - `ExceptionResponse`
* Create a Generic and common Exception class that will be used across the Application for all Exceptions
* This shall at minimum contain - timestamp(Date), message(String), details(String)

__File: ExceptionResponse.java__

```
package com.subbu.springboot.collegerestapi.exceptions;

import java.util.Date;

public class ExceptionResponse {
	private Date timestamp;
	private String message;
	private String details;

	public ExceptionResponse(Date timestamp, String message, String details) {
		super();
		this.timestamp = timestamp;
		this.message = message;
		this.details = details;
	}

	public Date getTimestamp() {
		return timestamp;
	}

	public String getMessage() {
		return message;
	}

	public String getDetails() {
		return details;
	}

}

```

### Override ```ResponseEntityExceptionHandler```
* Since this is marked in all controllers, mark it as @RestController instead of @Component
* Mark as @ControllerAdvice since this class will be shared across controllers
* Have a function to `handleAllExceptions` that returns `500-INTERNAL SERVER ERROR`
* Write functions for other individual Exceptions and return appropriate HTTP Error Codes
* Other Examples: Validation Logic - BAD REQUEST

```
package com.subbu.springboot.collegerestapi.exceptions;

import java.nio.file.attribute.UserPrincipalNotFoundException;
import java.util.Date;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.context.request.WebRequest;
import org.springframework.web.servlet.mvc.method.annotation.ResponseEntityExceptionHandler;

@ControllerAdvice
@RestController
public class CustomizedResponseEntityExceptionHandler extends ResponseEntityExceptionHandler {
	public final ResponseEntity<Object> handleAllExceptions(Exception ex, WebRequest request) {
		ExceptionResponse exceptionResponse = new ExceptionResponse(new Date(), ex.getMessage(),
				request.getDescription(false));

		return new ResponseEntity(exceptionResponse, HttpStatus.INTERNAL_SERVER_ERROR);
	}

	public final ResponseEntity<Object> handleUserNotFoundException(UserPrincipalNotFoundException ex,
			WebRequest request) {
		ExceptionResponse exceptionResponse = new ExceptionResponse(new Date(), ex.getMessage(),
				request.getDescription(false));
		return new ResponseEntity(exceptionResponse, HttpStatus.NOT_FOUND);
	}
}

```

### Other References
[Exception handling for rest with spring - Baeldung](https://www.baeldung.com/exception-handling-for-rest-with-spring)


## Validation in REST APIs
### Use Java Validation API
### Use @Valid
* Use `@Valid` annotation for `@RequestBody` or `@PathVariable`

### Add Constraints in Entity object
* The constraints are defined in package `javax.validation.constraints` found in `validation-api-2.x.jar`
* Hibernate Validator is one of the most popular implementations of Validation API. 

* Some Popular constraints are-
#### Size
Specify Size/Length of String. We can specify `min` and `max` characters
One can specify a Message also using `message` as part of the Constraint

#### NotBlank, NotEmpty, RegularExpression
#### NotEmpty
#### Past, PastOrPresent, Future
These are used for Dates. `Past` ensures that Date is always in the Past

```
...

public class Student {
	private String id;
	
	@Size(min=2, max=30, message="Name must have at-least 2 characters ")
	private String name;
	
	@Past
	private LocalDate dob;

...	  
```

### Throw Proper Exception in case of error
* When the Validation fails, by default, a 400-BAD REQUEST is returned, but no details regarding failure is present in headers. 
* In `CustomResponseEntityExceptionHandler` override `handleMethodArgumentNotValid`. This is raised when Binding to arguments is not proper.
* `Exception.getBindingResult() contains information` about what went wrong
* `getBindingResult()` has lot of options and we can customize what we show to the user

```
@ControllerAdvice
@RestController
public class CustomizedResponseEntityExceptionHandler extends ResponseEntityExceptionHandler {
....

@Override
	protected ResponseEntity<Object> handleMethodArgumentNotValid(MethodArgumentNotValidException ex,
			HttpHeaders headers, HttpStatus status, WebRequest request) {
		ExceptionResponse exceptionResponse = new ExceptionResponse(new Date(), "Validation Failed", 
				ex.getBindingResult().toString());
				
		// TODO Auto-generated method stub
		return new ResponseEntity<Object>(exceptionResponse, HttpStatus.BAD_REQUEST);
	}
}


```
## HATEOAS 
* Hypermedia As The Engine Of Application State
* Along with Response, the API also returns links that are relevant for future actions. Ex: If I get Bank account details, I also get links to Withdraw/Deposit etc along.
* HATEOAS is still not widely followed 

### Include `spring-boot-starter-hateoas`
* To use HATEOAS in Spring, Include `spring-boot-starter-hateoas` Maven dependency in `pom.xml`

```
<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-hateoas</artifactId>
		</dependency>
		...

```
### Static Import Hateoas
```import static org.springframework.hateoas.mvc.ControllerLinkBuilder.*;```

### Code
* Return `Resource` instead of actual Object
* Introduce links using `ControllerLinkBuilder` and reference internal methods - Their URI Mapping is automatically picked up

```
@GetMapping("/{id}")
//	public ResponseEntity<Student> getStudent(@PathVariable("id") String id) {
	public Resource<Student> getStudent(@PathVariable("id") String id) {
		Student student = this.studentService.findStudentById(id);
		if (student == null) {
			throw new StudentNotFoundException("id-" + id);
//			return new ResponseEntity<Student>(HttpStatus.NOT_FOUND);
		}
		
		Resource<Student> resource = new Resource<Student>(student);
		
		ControllerLinkBuilder linkTo = 
				linkTo(methodOn(this.getClass()).getAllStudents());
		
		resource.add(linkTo.withRel("all-users"));
		return resource;
//		return new ResponseEntity<Student>(student, HttpStatus.OK);
	}
```

### Request/Response

```
curl http://localhost:8080/api/students/1
{"id":"1","name":"Subramanya","dob":"1976-07-16","_links":{"all-users":{"href":"http://localhost:8080/api/students/"}}}
```

## Swagger Documentation
### Introduce Swagger Maven Dependency

```
		<dependency>
			<groupId>io.springfox</groupId>
			<artifactId>springfox-swagger2</artifactId>
			<version>2.9.2</version>
		</dependency>

		<dependency>
			<groupId>io.springfox</groupId>
			<artifactId>springfox-swagger-ui</artifactId>
			<version>2.9.2</version>
		</dependency>
```

### Create new file `SwaggerConfig`

## Versioning
### Types of Versioning
1. Media Type Versioning ("Content Negotiation") or ("Accept Header") - GitHub
2. Custom Headers Versioning - Microsoft
3. URI Versioning - Twitter
4. Parameter Versioning - Amazon

#### Using Different URI (URI Versioning) - Twitter Style

```
@GetMapping("v1/person")
// getPerson - Version 1

@GetMapping("v2/person")
// getPerson - Version2

// Calls
// http://localhost:8080/v1/person
// http://localhost:8080/v2/person
```

#### Using Request Params (Request Param Versioning) - Amazon Style

```
@GetMapping(value="/person", params="version=1")

@GetMapping(value="/person", params="version=2")

// Calls
// http://localhost:8080/person?version=1
// http://localhost:8080/person?version=2
```

#### Using HTTP Headers (HTTP Header Versioning) - Microsoft Style

```
@GetMapping(value="/person", headers="X-API-VERSION=1")

@GetMapping(value="/person", headers="X-API-VERSION=2")

// Calls
// curl -H "X-API-VERSION: 1" http://localhost:8080/person
// curl -H "X-API-VERSION: 2" http://localhost:8080/person
```

#### Using Produces (Media Type Versioning or MIME Type or Content Negotiation Versioning or Accept Header Versioning) - GITHUB Style
Differentiate services based on what it produces

```
@GetMapping(value="/person", produces="application/vnd.company.app-v1+json")

@GetMapping(value="/person", produces="application/vnd.company.app-v2+json")

// Calls
// curl -H "Accept: application/vnd.company.app-v1+json" http://localhost:8080/person
// curl -H "Accept: application/vnd.company.app-v2+json" http://localhost:8080/person
```
### Factors
#### URI Pollution
In-case of URI Versioning & Request Parameter Versioning, we are polluting the URI

#### Misuse of HTTP Headers
HTTP Headers were never intended for Versioning. Incase of HTTP Header Versioning & MIME type versioning, HTTP Headers are mis-used

#### Caching
* Caching becomes a problem in HTTP Header & Mime type versioning. This is because URI is same, Headers have to be looked at to differentiate. So, caching is not possible.

#### Can we execute the request on the browser?
Versioning using Headers cannot be executed on browser. It needs a client like Postman or Plugin or an Application. Normal users can't use it.

#### API Documentation
URI based is easier on documentation

### No Perfect Solution
* There is no perfect solution
* Prototype before Implementation and see which way makes it better for your application.

### More
* https://www.mnot.net/blog/2011/10/25/web_api_versioning_smackdown
* https://urthen.github.io/2013/05/09/ways-to-version-your-api/
### TODO: Discuss with multiple architects their experiences on API Versioning

## Securing REST Services
### Basic Authentication
Basic Authentication uses UserName & Password

* Add dependency `spring-boot-starter-security`

```

```

## Embedded Tomcat Configuration
### Server Address & Port
### Error Handling & Whitelabel Error Page
### Server Resources - Threads, Timeouts etc.
### SSL Support
### Access Log configuration

# REST APIs
## REST Actions
* GET (Get All Resources/Resource)
* POST (Create new Resource)
* PUT (Update Resource
* PATCH (Partial Update)
* DELETE (Delete)

## End-point Naming
### Singular/Plural
### Relations
## Status Codes & Return Content
### Fetch
### Creation
### Update
### Deletion
### JSON/XML - Encoding
### JSON/XML Format
## Validation
## SSL with REST
## Documentation
## Versioning
## Filtering, Search & Sort
### Filtering
### Searching
### Sorting
### Limiting Fields
### Pagination
## Pretty Print
## GZIP Support
## Rate Limiting
## Authentication
### Basic Authentication
### Digest Authentication
### 2-Legged OAuth
### 3-Legged OAuth

## Authorization
## Caching
## Validation, Error/Exception Handling
## Internationalization
## HATEOAS
## Monitoring
## Gateways
### AWS API Gateway
### ZUUL
### APIARY
## API References
### GitHub
### Tiwllio
### Facebook/Google
## Discovery