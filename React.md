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

