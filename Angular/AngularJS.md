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
3. Include Boostrap Javascript 

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

