# Spring Security

* Defines a framework for security
* Implemented using Servlet filters in the background
* Two methods of securing Web App - Declarative & Programmatic

## Spring Security with Servlet Filters
* Servlet filters are used to pre-process/post-process web requests
* Servlet filters can route web request based on security logic
* Spring provides a bulk of security functionality with servlet filters

## How Spring Security works
* Web browser tries to access a protected resource
* Spring Security filters use the Applications Security Configuration and information such as Users/Passwords/Roles to figure out if access can be provided to the protected resource

* Spring checks if Web Resource is Protected. If yes, it starts User Authentication processs. If no, it provides access to resource
* If user is authenticated, Spring starts User Authorization process. If not, User is sent to Login form to authenticate using Username and Password
* If user is authorized based on the role, Access is provided to Resource, else Access Denied is returned to user

## Security provided
* Authentication - Based on User ID & Password
* Authorization - Based on Roles

## Security Implementation Types
### Declarative Security
* We can define Security constrains in
	- All Java Configuration (using ```@Configuration```)
	- Spring XML Configuration

### Programmatic Security
* API for Custom Security Implementation
* Provides greater customization for specific app requirements

## Login Methods
* HTTP Basic Authentication
* Default Login Form - Spring Security provides a default login Form
* Custom Login Form - Your own look and feel, HTML+CSS

### Basic Authentication
* Default form generated by Browser. Asks for Username & Password.
* Very Ugly and provides no control

## Authentication & Authorization
* In-Memory
* JDBC
* LDAP
* Custom/Pluggable
* Others...

## Developing a Authentication using Spring
### Maven Dependencies
1. spring-webmvc
2. jstl
3. javax.servlet-api
4. javax.servlet.jsp-api

### Customize Maven Build
Use 'maven-war-plugin' and there is no need to use web.xml

### XML to Java Config
1. Instead of using web.xml use Spring's @Configuration
2. Instead of dispatcher-servlet.xml use Spring Dispatcher & Servlet Initializer

Note about dispatcher-servlet.xml:
The following activities are done in this XML
* Add Support for Component scanning via ```context:component-scan``` and provide package
* Add support for Annotiations via ```mvc:annotation-driven```

### Enabling the MVC Java Config
__```@EnableWebMvc```__
* Provides support to __```<mvc:annotation-driven```__ in XML
* Adds conversion, formatting and validation support
* Processing of @Controller class and @RequestMapping


 
