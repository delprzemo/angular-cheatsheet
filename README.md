# Angular Cheatsheet
Set of basic functionalities from Angular in one place

# AngularCLI
Command line inferface for Angular - set of commands that will help us during development.

**1. Setup**

| Command  | Description |
| ------------- | ------------- |
| npm install -g @angular/cli  | Install Angular CLI globally |

**2. New application**

| Command  | Description |
| ------------- | ------------- |
| ng new best-practises --dry-run  | just simulate ng new  |
| ng new best-practises --skip-install  | skip install means don't run npm install  |
| ng new best-practises --prefix best  | set prefix to best  |
| ng new --help	| check available command list  |


**3. Lint - check and make sure that our code if free of code smells/ bad formatting**

| Command  | Description |
| ------------- | ------------- |
| ng lint my-app --help  | check available command list  |
| ng lint my-app --format stylish  | format code  |
| ng lint my-app --fix   | fix code smells  |
| ng lint my-app  | show warnings  |


**4. Blueprints**

| Command  | Description |
| ------------- | ------------- |
| ng g c my-component --flat true  | don't create new folder for this component  |
| --inline-template (-t)  | will the template be in .ts file?  |
| --inline-style (-s) 	  | will the style be in .ts file?  |
| --spec		  | generate spec?  |
| --prefix  | assign own prefix  |
| ng g d directive-name	  | create directive  |
| ng g s service-name	  | create service |
| ng g cl models/customer	  | create customer class in models folder |
| ng g i models/person  | create create interface in models folder |
| ng g e models/gender  | create  create ENUM gender in models folder |
| ng g p init-caps	  | create create pipe  |

**5. Building&Serving**

| Command  | Description |
| ------------- | ------------- |
| ng build   | build app to /dist folder  |
| ng build --aot  | build app without code that we don't need (optimatization)  |
| ng build --prod	  | build for production  |
| ng serve -o   | serve with opening a browser  |
| ng serve --live-reload	  | reload when changes occur  |
| ng serve -ssl   | serving using SSL  |

**6. Add new capabilities**

| Command  | Description |
| ------------- | ------------- |
| ng add @angular/material 	  | add angular material to project  |
| ng g @angular/material:material-nav --name nav  | create material navigation component  |

# Components & Templates
Components are the most basic UI building block of an Angular app. An Angular app contains a tree of Angular components.

**Sample component .ts**
```ts
import { Component } from '@angular/core';

@Component({
	// component attributes
	selector: 'app-root',
	templateUrl: './app.component.html',
	styleUrls: ['./app.component.less']
})

export class AppComponent {
	title = 'my-dogs-training';
}
```
** Component attributes**

# Component attributes

| Attribute  | Description |
| ------------- | ------------- |
| changeDetection	  | The change-detection strategy to use for this component.  |
| viewProviders  | 	Defines the set of injectable objects that are visible to its view DOM children  |
| moduleId  | The module ID of the module that contains the component  |
| encapsulation  | 	An encapsulation policy for the template and CSS styles  |
| interpolation  | 	Overrides the default encapsulation start and end delimiters ({{ and }}  |
| entryComponents  | 	A set of components that should be compiled along with this component.  |
| preserveWhitespaces  | 	True to preserve or false to remove potentially superfluous whitespace characters from the compiled template.   |

# Template syntax

| Syntax  | Description |
| ------------- | ------------- |
| {{user.name}}	| Interpolation - just generate user name here  |
| <img [src] = "user.imageUrl">	| property binding - bind image url for user to src attribute  |
| <button (click)="do()" ... />	| Event - assign function to click event  |
| <button *ngIf="user.showSth" ... />	| Show button when user.showSth is true  |
| *ngFor="let item of items"	| Iterate through items list |
| <div [ngClass]="{green: isTrue(), bold: itTrue()}"/> | Angular ngClass attribute  |
| <div [ngStyle]="{'color': isTrue() ? '#bbb' : '#ccc'}"/>	| Angular ngStyle attribute  |
