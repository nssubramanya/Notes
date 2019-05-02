#Angular JS
## Dependencies for Angular JS
Node JS

##### Check version of Node JS

```
node -v
```

### How to install Angular CLI

```
npm install -g @angular/cli
```

### How to create a new Angular App
Run the CLI command `ng new` and provide name of app 
`my-app`

```
ng new my-app
```

### How to start the Angular App
1. Switch to the workspace folder (`my-app`)
2. Launch the server by using `ng serve` with `--open` option

```
cd my-app
ng serve --open
```
The `--open` option opens the browser automatically and points to `http://localhost:4200`

### What are the files and folders created in Angular App

#### Main Folders
`my-app` - workspace folder

`my-app\e2e\` - End to End Testing

`my-app\node_modules` - Contains all the installed Node modules

`my-app\src` - Source code of all the projects in the workspace

#### Configuration files under `my-app`

`angular.json` - Angular Workspace Configuration

`package.json` 

`README.md`

`tsconfig.json`

`tslint.json`

`.editorconfig`

`.gitignore`

#### Files under `src` directory
`app` - Project Directory



#### App

## Explain the Flow of Angular App

## How to Change Title of the App
* Look at `index.html` in `src` directory
* Change the  text under `<title> </title>`
* Save and Run

## How to import Forms Module
* Import `FormsModule`
In `src\app\app.module.ts`,

```{js}
import { FormsModule } from '@angular/forms';
```
* Include `FormsModule` in `imports`
	
```
	imports: [
		BrowserModule,
		FormsModule
	]
```

## Topics in Angular
* Basics
* Components & Databinding
* Directives
* Services & Dependency Injection
* Routing
* Observables
* Forms
* Pipes
* Http
* Authentication
* Optimizations & NgModules
* Deployment
* Animation & Testing

## How to install and use Boostrap with Angular?
1. Install Boostrap NPM Module
	To Install Bootstrap Version 3

	```
	npm install --save bootstrap@3
	```	
2. Include Boostrap CSS Styles
	 - Look at `src/angular.json` file
	 - Look for node `projects -- architect -- build`
	 - Look for Boostrap installation folder in `node_modules` and get the CSS and JS folders
	 - In `styles` add bootstrap css folder
	 
	 ```
	 "styles": [
	 	"node_modules/bootstrap/dist/css/bootstrap.min.css",
	 	"src/styles.css"
	 	]
	 ```


## Behind the scenes of Angular
What happens when we visit `http://localhost:4200`?

1. `src/index.html` is the file which is served by the server
2. `index.html` has a `<app-root>` element in the body. So, angular CLI replaces the `<app-root>` with content from the Component that contains the selector as `app-root`
3.  `src/app/app.component.ts` has the `@Component` declaration with `selector app-root`
4. The `html` and `css` files that are part of the component are in `app.component.html` and app.component.css`. These are used for rendering the component
5. The CLI injects JS scripts automatically in to `index.html` files at run-time. This is not seen in source code but seen only when we inspect it in browser
6. In file `main.ts`, `AppModule` is imported and it is boostrapped.
7. The AppModule is defined in `app.module.ts`. Modules are defined using `@NgModule`
8. The `bootstrap` array contains all the Components that Angular should know when starting the application

main.ts (Bootstrap AppModule) -> app.module.ts (Bootstrap Component) -> app.component.ts (Reads Selector to find out Root component) -> index.html (Knows app-root) -> app.component.html (Component HTML)

## Components
* Angular Application is COMPOSED of Components. 
* Components are User-created
* Root Component or `app-root` is the parent component that contains all the other components
* For ex: App can have the following Components - Header, Menu, Main Area, Sidebar
* Each Component has - Template (HTML), Styling (CSS), Business Logic
* Components help in Splitting the Application in to Smaller Pieces that are reusable if required. We can use same component multiple times in the app
* Very easy to Update, very easy to share instead of having one big Monolithic HTML and JS files

### Creating Components   
* Only the Root Component (`AppComponent`) is added to bootstrap array of AppModule. This is the only Special Component
* All other components are added to root-component's html file which is `app.component.html`
* Components are added as separate folders under the application `app`
* It is best practice to keep Component folder name SAME AS Component Name
* Component File Naming Convention - <component_name>.component.ts
* 	A component is a class that can be instantatied by Angular

#### STEP 1: Import Component from Angular Core

```
import { Component } from '@angular/core';
``` 

#### STEP 2: Define Component

```
@Component({
	selector: 'app-server',
	templateUrl: './server.component.html',
	styleUrls: ['./server.component.css']
})
```
##### Selector:
* Selector is the HTML element by which this component will be referred to in the HTML.
* Select string should be UNIQUE, it should not be the name of default HTML elements
* Naming Convention: <app name>-<component name> ex: app-server

##### Template URL
* Create the HTML Template file with naming convention - <component_name>.component.html; Ex: server.component.html
* Use the file name as part of 'templateUrl' property

##### Style URL
* This is an array of strings 'styleUrls'
* Specify the CSS file paths that contain styles for this component
* Does order matter?
 
#### STEP 3: Export Component Class

```
export class ServerComponent {
	serverName = 'MyServer';
}
```

#### STEP 4: Add component to AppModule
* AppModule packages all the components - the root app module
* Angular does not scan all component files - so it is important to register the component in the Module
* Register new components in the `declarations` property of `NgModule` 

###### File: app.module.ts
```
import { ServerComponent } from './server/server.component';
@NgModule({
	declarations: [
		AppComponent,
		ServerComponent
		],
	imports:
	...
})
```
__Note:__ in path for Searching component, no need to add `.ts` extention. It will be automatically added.

#### STEP 5: Add Custom Component to `app.component.html` - Root Component HTML

```
<app-server></app-server>
```

## Creating Component using CLI

Use the CLI

```
ng generate component servers
[or] 
ng g c servers
```
This will do the following-
* Create a folder called `servers` under `app`
* Create the files for `servers` component - `servers.component.ts`, `servers.component.html`, `servers.component.css`, `servers.component.spec.ts`
* Create the @Component section & Export the Component class
* Update the AppModule to Import the Component & Add the component to the `declarations` section of `@NgModule`

## Using Component with-in another component
To use one component within another component, simply include the component selector tag in the HTML file

__Example__
1. Use the `servers` component in `root` component - Make the following change in `app.component.html`

```
<app-servers></app-servers>
```

2. In the `app-servers` component HTML `servers.component.html` use the `app-server` component

```
<app-server></app-server>
<app-server></app-server>
```

Note that `<app-server>` component is Re-usable and can be used multiple times if required.

### Nesting of Components
Components can be nested within one another. In such a case, a component is created in the folder of another component.

To nest components when creating via CLI, mention the containing components separated by `\` when creating the component.

```
ng g c recipes/recipelist
```
### Prevent creation of spec file
To prevent creation of .spec file which is used for testing, following option can be added 

```
ng g c --spec=false recipe-list
```

## Inline HTML Template for Components
HTML for a component is usually written in a separate HTML file. Ex: for Servers component it is written in `servers.component.html`

However, if the HTML line is < 3, we can also write it in the component file itself `servers.component.ts`

To do this, we replace `templateUrl` in `@Component` with `template` and write the inline HTML.

To use Multi-line HTML strings, replace the single (') in the stirng with back-tick (`)

```
@Component ({
	selector: 'app-servers',
	template: `
		<app-server></app-server>
		<app-server></app-server>		...
})
```

__Note__:
`template` or `templateUrl` is MANDATORY in a Component.
`styleUrls` is NOT MANDATORY.

## Inline CSS for Components
Just like Inline HTML, we can also write Inline CSS in Components.

To do this, use the `styles` property instead of `styleUrls` property. Note that both of them are arrays.

In case of `styles`, we can specify an array with multiple strings. As usual, we can use back-ticks to use multi-line strings.

Only one of `styles` or `styleUrls` can be used at a time. Both should not be used. If both are used, Inline style is IGNORED.

Example:
In file `app.component.css`,

```
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styles: [`h3 { color: dodgerblue;}`]
  // styleUrls: ['./app.component.css']
})
```

## Different ways of using Angular Component Selectors
Component selectors usually work like Element Selectors

Specified like-

```
@Component ({
	selector: 'app-servers',
})
```

Used like-

```
<app-servers></app-servers>
```

Instead of Element-type selector, we can also use "Class-type" selector or "Attribute Type" selector

```
// Class Type Selector
@Component({
	selector: '.app-servers',
})

// Attribute Type selector
@Component({
	selector: '[app-servers]',
})
```

Usage:

```
<!-- Class Type Selector Usage -->
<div class="app-servers"> </div>

<!-- Attribute Type Selector Usage -->
<div app-servers> </div>

```
## Databinding
Communication between Business Logic (Typescript code) and HTML Template

Ways of Data-binding
1. One Way data binding
	 From Business logic to Template using String Interpolation ({{ data }}) or Property Binding ([property] = "data")
	 
2. React to User Events
	Event Binding - executing some code on events like Button click etc. ((event) = "expression")
	 
3. Two-way Data binding
When Model changes due to Business logic execution, the UI is changed and similarly when UI is updated, the model is also updated automatically

### String Interpolation
* Specified in HTML Template
* Uses the {{ }} syntax
* A String has to be present within the {{ }} syntax. It can be a hard-coded string or an expression that returns a string
* Ex: {{ 'Server' }} or {{ serverName }} or {{ getServerName() }}
* Usual way is to have Class properties and use the property name in the {{ }} syntax to replace the value of the property

###### File: server.component.ts
```
export class ServerComponent {
	serverStatus: string = 'offline';
	
	getServerStatus() {
		return this.serverStatus;
	}
}
```

###### File: server.component.html

```
<p> {{ 'Server' }} with ID {{ serverId }} is {{ getServerStatus() }} </p>
```

### Property Binding
We can bind HTML Properties to Angular identifiers so that the HTML properties change based on the value of the identifiers.

Ex: Binding to `disabled` property of a HTML button to a Angular identifier `allowNewServer`. Based on `true` or `false` value of the identifier, the button can be `enabled` or `disabled`

```
<button class="btn btn-primary" [disabled]="!allowNewServer">AddServer</button>
```
```
export class ServerComponent {
	let allowNewServer:boolean = false;
}
```
Note that Property binding uses Square Brackets []

### Event Binding
Event Binding helps us to bind to HTML events and execute code when that event occurrs

Event binding uses Parantheses ()

To bind a Button click event to execute a function,

```
<button class="btn btn-primary" (click)="onServerCreate()">New Server</button>
```
This code will call `onServerCreate` function on button click.

### Two Way Data Binding
We combine One-way data binding and Event Binding

If HTML Element changes, the Model variable changes. Same way if model variable changes, HTML element is updated automatically.

__File__:`servers.component.html`

```
<input type="text" [(ngModel)]="serverName"/>
```
__File__:`servers.component.ts`

```
export class ServersComponent {
	serverName = 'TestServer';
}
```

## Directives
Directives are Instructions in the DOM. Note that Components are also Directives.

They are extended HTML Attributes with prefix ng-

Directives are markers on DOM element (may be attribute, element name, comment or CSS class) that tells Angular's HTML compiler to attach a specified behavior to that DOM element or transform the DOM element and its children
```
<p appTurnGreen> Receives a green Background! </p>
```

```
@Directive({
	selector: '[appTurnGreen]'
})
export class TurnGreenDirective {
}
```

### ngIf
The ngIf is used with HTML Element to conditionally include/exclude the element.

A structural directive that conditionally includes a template based on the value of an expression coerced to Boolean.

__File__: servers.component.html
```
<input type=text [(ngModel)]="serverName">
<p *ngIf="serverCreated">Server was created, server name is {{ serverName }}</p>
``` 

__File__: servers.component.ts

```
export class ServersComponent {
	serverName = '';
	serverCreated = false;
	
	onServerCreated() {
		serverCreated = true;
	}
```

### ngIf-Else
Refer to the following article:
[ngIf documentation] (https://angular.io/api/common/NgIf)

### ngStyle
* This is a attribute directive. 
* Structural directives add/remove elements. Attribute directives only change the element where they are placed on
* Sets one or more style properties, specified ad colon separated key-value pairs

```
<p [ngStyle]="{background-color: getColor()}">{{getServerStatus()}}</p>
```

`getColor()` can dynamically evaluate conditions and specify color appropriately.
 
### ngClass
* Applies a CSS class to an element conditionally. Adds or Removes CSS classes

Examples:
```
<some-element [ngClass]="'first second'">...</some-element>
<p [ngClass]="{online: isServerOnline()}">
```

### ngFor
Loop through and insert DOM elements

```
<ul>
	<li *ngFor="let hero of heroes">
		{{ hero }}
	</li>
</ul>
```

#### To get the index value in ngFor
```
<ul>
	<li *ngFor="let hero of heroes; let i = index">
		{{i}} - {{ hero }}
	</li>
</ul>
```

## Course Project
```
ng g c headerng 
ng g c recipes --spec false
ng g c recipes/recipe-list --spec false
ng g c recipes/recipe-details --spec false
ng g c recipes/recipe-list/recipe-item --spec false

ng g c shopping-list --spec false
ng g c shopping-list/shopping-edit --spec false
```

## Augury - To Debug Angular Code
* Chrome Plugin
* Look in Debug Console - Augury Tab
* Shows Component Tree, NgModules, Router Tree
* Great tool to understand application dependencies

## Passing Data between Components

### Exposing a Bindable property from a Component
A component can expose a bindable property by using the `@Input('<alias>')` decorator in front of the property that is visible from outside and to which data can be passed

By default, all attributes of a Component are private and not accessible from outside. 

```
export class ServerElementComponent{
	@Input('srvElement') element: {type: string, name: string};
	
}
```

The alias inside the @Input is not mandatory. If it is not present, the property name is used as is.

__Note:__
This method is extremely useful to pass data from PARENT component to CHILD component

### Binding to custom Events
A component can raise events and other components can bind to those events to catch them. Data can also be passed as part of raising this event.

1. Import `Output` and `EventEmitter` from `@angular/core`
2. Create the events
3. Emit the events
4. In HTML, attach handler functions to events
5. Get the Event data and act on it in the hander

##### Setting up a Component to raise Events
```
import { Component, Output, EventEmitter } from '@angular/core';

@Component(){
}

export class CockpitComponent {
@Output() serverCreated = new EventEmitter<{serverName: string, serverContent: string}>();

@Output('bpCreated') blueprintCreated = new EventEmitter<{serverName: string, serverContent: string}> ();
}
```

##### Emitting Events
```
export class CockpitComponent {


}

```


kubeadm join 172.31.99.250:6443 --token s05tzb.bw87atsb08ardxzi --discovery-token-ca-cert-hash sha256:3da00a1f60215810a2923032303e938bdec395640347f50cbd23752fd7043b9f


