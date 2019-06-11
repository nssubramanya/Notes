# REACT

## Tools
#### Dependency Management Tools
```npm``` or ```yarn```

#### Bundler
```webpack```

#### Compiler (Next Gen Javascript)
```Babel``` + Presets

#### Development Server
Web Server (local)

## Creating a new React App
### create-react-app - https://github.com/facebook/create-react-app

### Installation

#### Install Node.js

#### Install create-react-app
To Install Version 2.x
```
npm install -g create-react-app@2
```

To install latest
```
npm install -g create-react-app
```

### Create the react App
```
create-react-app react-complete-guide
```
Replace ```react-complte-guide``` with any other project name

### Launch React App
```
cd react-complete-guide
npm start
```
Access app using http://localhost:3000

Ensure that 'npm start' is kept running.

## Folder structure of React App

### package.json
* Describes the React application
* 'name', 'version' can be configured here
* dependencies are listed - react, react-dom, react-scripts
* To run scripts use command ```npm run <script name>```
* ```npm run build``` will not launch dev server. It will optimize the code for production deployment

### node_modules
* Holds all the node modules - Automatically generated - Don't Edit

### public
* This is the folder served by the Web Server
* ```index.html``` is the key file here - This is the only file for Single-Page-App
* For Multiple page app - you add more app here

### index.html
* We will generally not edit this file
* Can add CSS references, META tags if required
* Element with ID `root` is the Root of the React DOM that will be replaced by React Scripts

### manifest.json
* React gives us a PWA - Progressive Web App out of the box
* We can place relevent meta data here

### src\index.js
* Contains the reference to `root` element described in `index.html`
* Uses `ReactDOM` to render the `App` application in to `root` element
* No need to add `App.js` for the import. It is automatically picked up

### src\App.js
* The React Applciation
* Contains the React Component
* Contains the JSX (HTML code) that is rendered on the page

### src\App.css
* Defines styles to be used by all HTML in `App.js`

### src\index.css
* Global Styles used for Body of App

### src\registerServiceWorker.js

### App.test.js
* For Unit Testing

## Restrictions of JSX
* Use `className` instead of `class` since it is JS keyword
* JSX must be enclosed in one single element. Advisable to return one nested element

## Custom Components
* Introduce a new File say `Persons.js`
* Advisable to name it capitalized
* Import `React` from react; Also import `Component` if required

```
import React from 'react';
// import React, {Component} from 'react';
```
### Functional Components
* Use a function to return JSX

```
const person = () => {
	return (
		<div>
			<h1>Hello, World</h1>
		</div>
	)
}
```
### Class-based Components
* Use a Class that inherit from `React.Component` to hold component data and return JSX
* This has a special method `render` that is over-ridden. This will be called by React.

```
class Person extends Component {
	render () {
		return (
			<div>
				<h1>Hello, World</h1>
			</div>
		)
	}
}
```

## Using Values in JSX
* Use a pair of Curly Braces. Put the variable or compuation within the brace

```
const person = () => {
	return (
		<div>
			<p>Random Age: {Math.floor(Math.random() * 30))}</p>
		</div>
	)
}
```

### Passing Arguments to Function Components - using `props`
* Multiple Arguments can be passed as Attributes during call
* All arguments are combined in to a single argument object called `props`
```
const person = (props) => {
	return (
		<div>
			<p>Name: {props.name} Age: {props.age}</p>
		</div>
	)
}
```

In Calling Component App.js
```
import React from 'react';
import './App.css';
import Person from './Person/Person';


function App () {
	return (
		<div className="App">
			<h1>Main Component</h1>
			<Person name="Steve" age="35"/>
		</div>
	)
}
```

### Storing State in Parent component - state passed to Child component for render

```
import React, { Component } from 'react';
import './App.css';
import Person from './Person/Person';

class App extends Component {
	state = {
		persons: [
			{name: "Steve", age:"35"}
		]
	}
	
	render () {
		return (
			<div className="App">
				<h1>Main component</h1>
				<Person name={this.state.persons[0].name} age={this.state.persons[0].age}>
			</div>
		)
	}
}
```

Same `Person` component is used for rendering `Person`

```
const person = (props) => {
	return (
		<div>
			<p>Name: {props.name} Age: {props.age}</p>
		</div>
	)
}
```
Note:
If `state` changes, React automatically renders the page!

## Handling Events
* Note that Button click events in JSX are called `onClick` instead of `onclick` of javascript
* Handler function is better named with `Handler` as ending word; Ex: `switchNameHandler()`
* If short code is there, it can be written inline using curly braces

## Changing State in Event Handlers
* Entities under `state` SHOULD NOT BE CHANGED DIRECTLY!

WRONG!!
```
switchNameHander = () => {
	this.state.persons[0].name = "Stephan"
}
```

* Use the `setState` function to set the state
* setState takes the object whose state needs to be changed as argument
* It replaces only the object passed to `setState`. If there are other objects/entities as part of `state` they are not touched/changed

```
class App extends Component {
state = {
	persons: [
		{name: "Stan", age=25}
	],
	course="React"
};

switchStateHandler = () => {
	this.setState({
		persons: [
			{name: "Stan", age=30},
			{name: "Bill", age=21}
	});
}
```
Here, the `course` variable is not changed

### Changing state in Functional components
Functional components do not have the `state` variable. Hence we need a different way of changing state here.

Here, we use `useState` function for setting the state internally.
`useState` can be called multiple times for setting different state variables

#### useState
`useState` takes any argument (state to be saved) and returns 2 arguments
1st argument is the current state object/value
2nd argument is the function that can be used to update the state when called

```
const [someState, setSomeState] = useState(anyData)

const someFunction = () => {
	setSomeState(newState)
}
```

The function `setSomeState` does not do Automatic Merging, but replaces the new State.

To over come this problem, there are 2 strategies:
__Strategy 1__: Add the missing state as part of the `setSomeState` function arguments
```
	setSomeState(newState, oldMissingState)
```
__Strategy 2__: Call `useState` multiple times, each time with a different state object to internally store the different state objects. 
Each time, `useState` returns separate State Variables and State Updating functions. Call the respective functions to update relevant state objects

```
const app = props => {
	const [personState, setPersonState] = useState({
		persons: [
			{ name: "Steve", age=28 },
			{ name: "Laura", age=30 }
		]
	});
	
	const [otherState, setOtherState] = useState('some other value');
	
	const switchNameHandler = () => {
		setPersonState ({
			persons: [
				{ name: "Stephen Fleming", age = 36},
				{ name: "Laura Phillip", age = 30 }
			]
		});
	}
}
```

## Stateful and Stateless Components
### Stateful Components
* Any component that stores and manages internal state using Class-based `state` method or Function-based `useState` method is a Stateful component
* This is also called Container Component or Smart Component

### Stateless Component
* A component that does not contain any internal state is a Stateless Component
* This is also called a Presentation Component or Dumb Component
* It is advisable to create as many Stateless Components as possible instead of Stateful components

## Passing Method References
Method reference can be passed as part of parameters from one component to another one. It can be used with `props`.

## Two-way Binding
When UI changes -> Model/State must be updated
When Model/State Changes -> UI must be updated

Step 1: Setup the Component

__File: hello.js__

```
import React from 'react';

const hello = (props) => {
	return (
		<div>
			<input type="text" placeholder="Enter Company" onChange={props.changed} value={props.company}/>
			<p>{props.company}</p>
		</div>
	)
}

export default hello;
```

__File: App.js__

```
class App extends Component {
	state = {
		company: "Aseema"
	}
	
	companyChangedHandler = (event) => {
		this.setState ({
			company: {event.target.value}
		});
	}
	
	render () {
		return (
			<div className="App">
				<Hello company={this.state.company} changed={this.companyChangedHandler} /> 
			</div>
		)
	}
}
```

## Inline styles

## Conditional output
* Similar to *ngIf directive in Angular
* JSX is actually javascript, so we can use Ternary operator to decide
* Use a variable that will determine whether to Include the element (& its children) into DOM or not
* Enclose within Angle brackets and put the ternary operator and the elements within it

```
let showPersons = false;

{
	showPersons ?
	<div>
		<Person />
		<Person />
	</div>
	: null
}
```

Alternatively, we can assign the DOM elements to a variable and use that variable to include it in to the DOM

## Looping
* Use Javascript tools - Map

```
function App() {
	return (
		<div>
		{
			persons.map(person => {
				return <Person name={person.name} age={person.age}/>
			})}
		</div>
	)
}
```

Pattern is to MAP an Array in to an Arrary with JSX elements

### Passing Click handler into Lists
```
const nameChangedHandler = (event, id) => {
	const personIndex = this.state.persons.findIndex(p => {
		return p.id === id;
	});
	
	const person = {
		...this.state.persons[personIndex];
	};
	
	person.name = event.target.value;
	const persons = [...this.state.persons]
	persons[personIndex] = person;
	
	this.setState({persons: persons})
}

const deletePersonHander = (personIndex) => {
	// const persons = this.state.persons.slice();
	const persons = [...this.state.persons];
	
	persons.splice(personIndex, 1);
	this.setState({persons: persons});
}

let persons = null;

if (this.state.showPersons) {
	persons = (
		<div>
			{
				this.state.persons.map((person, index) => {
					return <Person
						click = {() => this.deletePersonHanlder(index)}
						name = { person.name }
						age = { person.age }
						key = { index }
						changed={(event) => this.nameChangedHandler(event, person.id)}
				})
			}
		</div>
}
```

### Lists & Keys
Key property is extremely important for React to figure out which item in the list got changed and only render them. Otherwise, for every change, the whole list is re-rendered and this is wasteful and slow.

Look at `key` attribute in previous code listing

## Styling React Elements & Components
* Using Inline Styling, React only provides options to set CSS properties
* No Support for Pseudo selectors like `hover`. Pseudo selectors depend on other elements Ex:

```
button {
	background: white;
}

button:hover {
	background: green;
}
```

### Inline Style

```
const style = {
	background: 'white',
	color: 'red'
}

<button style={style}></button>
```

### Dynamically adding Styles
* Since everything is Javascript in JSX, use code to specify styles

```
	const style = {
		background: 'green',
		color: 'white'
	}
	
	if (this.state.showPersons) {
		style.background = 'red';
	}
	
	<button sytle={style}></button>
```
Once the `style` object is set, any changes to it are automatically applied

### Dynamically adding classes
* Use code to put the necessary classes in to a variable.
* Assign that variable to `className`
* Any change to that variable, the classes are re-applied automatically

### Using Radium for dynamic styling (solving pseudo selector problem)
* Radium is a set of tools to manage inline styles on React elements
* It give you powerful styling capabilities without CSS
* Radium unlocks power of React & inline styling by enabling support for CSS pseudo selectors, media queries, vendor-prefixing and much more through a simple interface

#### Installing Radium

```
npm install --save radium
```

#### Importing Radium
Radium must be imported in every file it is being used.

```
import Radium from 'radium';
```

#### Using Radium
To use radium, the component must be Wrapped within Radium
Radium works as a Higher-Order-Component (HOC), a component that contains another component

This Wrapping can be used for both Class-based components and function-based components

```
export default Radium(App);
```

## Organizing App in to Component
* Have more Presentation components (function-based) dumb components
* Manage State in only a few components
* Prefer to use Class-based components to manage State

## Class-based Vs Function-based Components
### Class Based
* __Creation:__ `class XY extends Component`
* __State Management:__ Yes using `state` and `setState()`
* __State Access:__ Directly via `this.state.XY` or `this.props.XY` (in case of child components that are also class-based)
* __Lifecycle Hooks:__ Yes

Use this if you need to manage State or access to Lifecylce Hooks and don't want to use React Hooks!

### Functional Components
* __Creation:__ `const XY = props => { }
* __State Management__: Yes via `useState()`
* __State Access__: Yes
* __Lifecycle Hooks__: No
* Access Props via `props` (`props.XY`)

Use this in all cases where we dont' want to manage State, Don't need Lifecylce Hooks!

## Component Lifecycle
### Creation Life Cycle
#### `constructor (props)`
* DO: Setup State
* DON'T: Cause Side-effects like - (a) Making HTTP Request (b) Storing data in Local Storage of Browser (c) Sending Analytics to Google analytics etc.

#### `getDerivedStateFromProps()`
* Whenever props of Class based component change, you can sync your state to them!
* When props change, if we want to change some internal state
* Very Rare to use!
* Don't cause Side Effects (Making HTTP Requests etc.)

#### `render()`
* Prepare and Structure your JSX & HTML
* Don't cause Side Effects like Making HTTP Requests, Blocking, Timeouts etc. To block the Rendering process
* In Render, if we are rendering any Child Components, their Life-cycle Hooks get Executed in the same order as above - constructor, getDerivedStateFromProps, render

#### `componentDidMount()`
* Will be called after rendering of current component
* Very Important LifeCycle event that is very often used
* We can make HTTP Requests
* Do NOT Set State here immediately. This can be done after the HTTP Request returns the data. 
* Anytime `setState` is called, a re-render cycle is executed which is bad for performance!

#### `getShapshotBeforeUpdate()`

* `componentDidCatch()`
* `shouldComponentUpdate()`
* `componentDidUpdate()`
* 
* `componentWillUnmount()`


## Creating a Project

### Identify Requirements
### Identify Components
### Identify State
### Create Project
### Setup
- Remove SVG file & its references
- Remove default JSX content in App.js 
- Remove App.css and its reference in App.js
- Use Google Fonts to get reference of `Open Sans` font; Customize for Add Regular & Bold; Add font reference to `index.html`
- Change Application Title in `index.html`
- Create folders `src\components`, `src\containers`, `src\assets`; `src\components  ` will contain Presentational Components (Functional or Class-based), `src\containers` will contain Smart Components that manage State; `assets` will contain Image assets
- 









