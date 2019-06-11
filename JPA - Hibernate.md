# JPA - Hibernate
## JPA
## JPA Providers
### Hibernate (Most Popular)
### iBatis
### EclipseLink (Reference Implementation)

## Step 01: Setting up a project with JDBC, JPA, H2 and Web Dependencies
* Go to [Spring Initizr](http://start.spring.io)
* Create Project - Specify Maven, Java, Spring Boot, Group Name, Artifact name
* Select following Dependencies - JPA, Web, JDBC, H2
* Generate Project
* Import Generated project to Eclipse
* Run as Java application and ensure running

## Step 02 - Launching up H2 Console
* To enable H2 Console access add the following configuration to ```application.properties``` file

```
spring.h2.console.enabled=true
```
* Run application 
* Go to URL: ```http://localhost:8080/h2-console```

### Using H2 Console
* Can change setting name
* Driver: org.h2.Driver
* JDBC URL: jdbc:h2:mem:testdb
* User Name: sa (by default)
* Password: blank by default

### H2 Console Features
* Just like any other DB Console app
* Data is transient, lost once applciation is stopped

## Step 03 - Creating Database table in H2
* Use Create New->SQL File to create a new SQL file `data.sql` in `src/main/resources`
* When app is initialized, this SQL file is executed. This is an Auto-Configuration feature provided by Spring.
* Write SQL-DDL code to create a table

```
CREATE TABLE person (
	id INT NOT NULL,
	name VARCHAR(255) NOT NULL,
	location varchar (255),
	birth_date timestamp,
	PRIMARY KEY(id)
);
```

* This code is run when application starts up
* Check in H2 Console, a Table called `person` is created with specified fields.
* We can even use SCHEMA NAME and it is appropriately used, For example

```
CREATE TABLE person_db.person();
```

## Step 04: Populate Data into Person Table
* Data in H2 database is lost when Application restarts
* Write INSERT Statements that populate data inside the `data.sql` file

```
CREATE TABLE person (
	id INT NOT NULL,
	name VARCHAR(255) NOT NULL,
	location varchar (255),
	birth_date timestamp,
	PRIMARY KEY(id)
);

INSERT INTO person (ID, NAME, LOCATION, BIRTH_DATE)
	VALUES(10001, 'Subbu', 'Bangalore', '1976-07-16 10:30:00');
INSERT INTO person (ID, NAME, LOCATION, BIRTH_DATE)
	VALUES(10002, 'Roopa', 'Mysore', '1979-01-05 11:30:00');
INSERT INTO person (ID, NAME, LOCATION, BIRTH_DATE)
	VALUES(10003, 'Sushruth', 'Bangalore', '2006-02-19 10:40:00');
```

## Step 05: Implement `findAll` persons Spring JDBC query Method
### Creating Entity Object
* Create the `Person` class that will hold data from the `person` table in the database.
* Implement fields, constructor, setters, getters for `Person` class

__`src/main/java/Person.java`__

```
package com.subbu.springboot.databasedemo;

import java.util.Date;

public class Person {
	private int id;
	private String name;
	private String location;
	private Date birthDate;
	
	public Person () {
		
	}
	
	public Person(int id, String name, String location, Date birthDate) {
		super();
		this.id = id;
		this.name = name;
		this.location = location;
		this.birthDate = birthDate;
	}

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getLocation() {
		return location;
	}

	public void setLocation(String location) {
		this.location = location;
	}

	public Date getBirthDate() {
		return birthDate;
	}

	public void setBirthDate(Date birthDate) {
		this.birthDate = birthDate;
	}

	@Override
	public String toString() {
		return "Person [id=" + id + ", name=" + name + ", location=" + location + ", birthDate=" + birthDate + "]";
	}
	
	
}

```

### Creating DAO object
* Create a `PersonJdbcDao` class
* We use `JdbcTemplate` 

```
package com.subbu.springboot.databasedemo;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.BeanPropertyRowMapper;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Repository;

@Repository
public class PersonJdbcDao {
	
	@Autowired
	JdbcTemplate jdbcTemplate;
	
	// select * from person
	public List<Person> findAll(){
		return jdbcTemplate.query("select * from person", 
				new BeanPropertyRowMapper<Person>(Person.class));
	}
}

```

## Step 06: Execute `findAll` method using `CommandLineRunner`
### CommandLineRunner
* Implement CommandLineRunner in Application - `public class DatabaseDemoApplication implements CommandLineRunner`
* Add un-implemented methods `run`

```
@Override
	public void run(String... args) throws Exception {
		// TODO Auto-generated method stub
		
	}
```

__DatabaseDemoApp.java__

```
package com.subbu.springboot.databasedemo;

import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
 public class DatabaseDemoApplication implements CommandLineRunner {

	public static void main(String[] args) {
		SpringApplication.run(DatabaseDemoApplication.class, args);
	}

	@Override
	public void run(String... args) throws Exception {
		// TODO Auto-generated method stub
		
	}
}
```

### Introduce Logger
* `private Logger logger = LoggerFactory.getLogger(this.getClass());`
* `import org.slf4j.Logger`
* `logger.info("Hello, {}", name);`

```
package com.subbu.springboot.databasedemo;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
 public class DatabaseDemoApplication implements CommandLineRunner {
	
	private Logger logger = LoggerFactory.getLogger(this.getClass());
	
	@Autowired
	PersonJdbcDao dao;
	
	public static void main(String[] args) {
		SpringApplication.run(DatabaseDemoApplication.class, args);
	}

	@Override
	public void run(String... args) throws Exception {
		// TODO Auto-generated method stub
		logger.info("All users -> {}", dao.findAll());
	}
}
```

* Note that we use `Autowired` for `PersonJDBCDao`