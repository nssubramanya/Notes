
## Types of Testing
### Page Testing
* Involves UI Testing - Presentation and functionality of Page
* Use [Mocha](https://mochajs.org)

### Cross Page Testing
* Testing functionality that requires navigation from one page to another one. Ex: Ecommerce Checkout
* Considered Integration Testing
* Use [Zombie](http://zombie.js.org)

### Logic Testing
* Unit and Integration Testing of Javascript Logic
* Tests only Javascript
* Jasmine/Mocha/JTest/AVA/Tape

### Linting
* Source code static analysis to find potential errors
* JSHint/EsLint/JsLint

### Link Checking
* To make sure there are no broken links
* Use LinkChecker

## Other Tools
### Auto-Restart of Server
* Automatically re-start Node applciations on saving
* Nodemon
* Grunt Plugin

### Testing Tools
#### Some Links
* [Overview of Javascript Testing in 2018](https://medium.com/welldone-software/an-overview-of-javascript-testing-in-2018-f68950900bc3)
* [180+ Web Application Testing Example Test Cases](https://www.softwaretestinghelp.com/sample-test-cases-testing-web-desktop-applications/)
* [Unit Testing in Agile Web Projects](https://medium.com/aperto-an-ibm-company/unit-testing-in-agile-web-projects-4db5547a733b)
* [Unit Testing: Time-consuming but Product Saving] (https://thenewstack.io/unit-testing-time-consuming-product-saving/)

#### Provide Testing Structure
* Mocha, Jasmine, Jest, Cucumber

#### Provide Assertion Functions
* Chai, Jasmine, Jest, Unexpected

#### Generate, Display and Watch Test Results
* Mocha, Jasmine, Jest, Karma

#### Generate/Compare Snapshots to make sure previous runs are intended
* Jest, AVA

#### Provide Mocks, Spies & Stubs
* Sinon, Jasmine, enzyme, Jest, testdouble

#### Generate Code Coverage Reports
* Istanbul, Jest, Blanket

#### Browser-like environment for Test Scenario Execution Control
* Protractor, Nightwatch, Phantom, Casper

#### Cross-Page Testing
* Selenium, PhantomJS, Zombie

#### Load & Stress Testing
* ApacheBench, Siege, Jmeter, Tsung
* strongloop.com, phanos, 

#### TODO: res.locals
