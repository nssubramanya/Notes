# Packages
## Package Statement
* Package is used to group together related set of classes, interfaces, enums etc.
* They provide access protection and namespace management

### Package Statement Rules
* Package name must be all lower-case
* All Java classes are part of Package
* Package can be explicitly specified
* If not specified, class becomes part of default package without name
* Package statement must be the first statement in class definition
* Package is usually specified as a dotted triad as shown below-

```java
	// package com.<company>.<project>.<subproject>;
	package com.oracle.javacert.associate;
	
	// gov, org, edu etc. can also be used appropriately
```
* Package cannot be specified within the class or below it
* There can only be 1 package statement, even same package statement cannot be repeated
* For all package statement errors following error is displayed-

> _JavaClassStructure.java:3: error: class, interface, or enum expected_

#### FQDN

* Fully-qualified name of class/interface in an package is formed by prefixing its package name. Ex: ```com.oracle.javacert.assocaite.ExamQuestion```

#### Directory Structure and Package Hierarchy
* Hierarchy of class/project must match the package name
* No constraint on base directory in which the package hierarchy is present
* Add base directory of Package hierarchy to CLASSPATH to enable JRE to find the classes
* 
## Import Statement
* Allows to use simple names instead of using FQDN when using Packaged entities
* Classes, Interfaces in same package can use the names directly
* Classes, Interfaces in different package need to use FQDN or use imported name

* No need to use explicit import statement to use members from java.lang package
* Classes with Same name ex: ```java.util.Date``` and ```java.sql.Date``` CANNOT be imported in to the same Java file. This causes an error
* To over come the above error use FQDN or import the frequently used classs and use FQDN for infrequently used class

#### Import Single Member vs all members
* ```import certification.* ``` imports all members of the class
* ```import certification.ExamQuestion``` imports only one class
* Problem with using '*' is that it is difficult to find out which ones are imported. Maintainability problem!
* Import will not import Sub-packages. We have to use full package name
* Entities in Default package can access each other directly if they are in the same directory

#### Static Imports
* Static members of a class in package can be imported statically. By doing so, they can be accessed directly without class Name

```java
	import static certification.ExamQuestion.*; // Imports all static
```

## Java Access Modifiers
* They restrict the accessibility of class and its members in same and different packages

* Note: Top level class or interface is one that's not defined within another class or interface. They are called nested or inner classes

* Access modifiers can be applied to classes, interface and their members (instance variables and methods)

* We cannot specify access modifiers to Local variables & paramemters
### Default Access
* If class/interface/method/variable is not defined with explicit access modifier, it is said to be defined with 'Default' access or 'Package' access
* 4 Access levels - Public, protected, default, private
* Public - Derived and Unrelated classes in both Same & different packages can access the class and members
* Protected - Derived and Unrelated classes in same package can access. Derived class in another package can access via inheritence. Un-related classes in other packages cannot access
* Default - Accessible only to Classes and interfaces in same package. Classes in other packages cannot access
* Private - Only class methods can access the member variables and methods. No outside classes within packages or outside package can access these

## Non-Access Modifiers
* These are optional modifiers
* They change the default behaviour of a java class and its members
* ```abstract```, ```static```, ```final```, ```synchronized```, ```native```, ```strictfp```, ```transient```, ```volatile```

* ```synchronized``` - Classes/Interfaces/Methods **can't** be marked with this. **Synchronized method** cannot be accessed by Multiple threads concurrently

* ```native```:  **Native method** calls and makes use of libraries and methds implemented in other languages like c or C++. Can't be makred for interfaces, classes and variables

* ```transient```: **A Transient Variable** is not Serialized when corresponding object is serialized

* ```volatile```: **A volatile variable** value can be safely modified by different thereds

* ```strictfp```: **Classes, Interfaces, Methods** marked with this ensure Floating-point calculations are identical on all platforms. Can't be marked on variables.

### Abstract
* Applicaple to Class, Interface or Method

#### abstract class
* A ```abstract class``` can't be instantiated
* Applying ```abstract``` to a Concrete class (one that does not define a ```abstract``` method) will make it Abstract
* Abstract class may or may not define abstract method. 
* Concrete Class CAN't define abstract method

#### abstract interface
* By default, interfaces are abstract
* Java compiler adds abstract to interface by default
* So, it is redundant

#### abstract method
* abstract method does not have body.
* It has to be implemented by Derived class
* ```public abstract void perform()```

#### abstract variables
* Code won't compile

#### Access Specifiers with abstract
* private abstract is not possible since derived methods can't see it. It is not a compilation error though
* public and protected abstract methods are possible

### final

1.1 - a
1.2 - 3,2,1,5,6,4 - d
1.3 - a/d
1.4 - 



Default Method in Interfaces - Multiple Inheritence