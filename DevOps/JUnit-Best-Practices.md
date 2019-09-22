# JUnit Best Practices

## Goals
* Unit test execution must be __lightning fast__
* Unit tests must be reliable and indicate problems in __production code__

## Run Tests in Memory
Highly recommended that Unit Tests SHALL NOT perform HTTP Access, Data base access or Read from File System.

## Do not Skip Unit TEsts
Because there is no use. If any test is not requried, don't put it to Source Control

Don't use JUnit's @Ignore, Maven's maven.test.skip, Surefire plugin's skipTests & excludes.

## Aim for only one assertion per method
* Much easier to find out what went wrong when test fails

## Use Strongest assertions possible
* Strongest - asserting on return value of method
* Strong - Vital Independent Mock objects were interacted with correctly
* Weak - Vital non-independent mock objects were interacted with correctly (Ex: Logging statements etc.)
* Non-existent assertions

## Using Proper Assertion Methods
TODO

## Test Naming Convention
Follow a consistent naming convention
### Test Class
Test Class - <Class_Under_Test>Test
Ex: Calculator, CalculatorTest

### Test Methods
<methodUnderTest>_Condition
Ex:
add_integers
add_integerAndFloat
add_integerAndString

## Packaging Production & Test code
Test class shall use package-private classes and package-private methods

This makes it necessary that both production source code and test code are part of same package

## Test code and Production code are separated
Production code in - src/main/java
Test code in - src/test/java

## Don't print anything in unit-tests
No print statements in Unit-tests like Debug statements, Stack Traces etc.

## Initializing Classes
Use @Before method to initialize class and class members required for test

Or use private static final members

## Catching
Do not write catch blocks to -
* Fail a test
* Pass a test

## Test Classes Directly; don't rely on indirect testing
If Class A depends on Class B, methods of B will be called by A.

It is better to test Class B directly even though methods of B are called when testing methods of A

## References
[JUnit Best Practices - Kyle Blaney](http://www.kyleblaney.com/junit-best-practices)