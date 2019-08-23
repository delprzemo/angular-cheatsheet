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

# Components

**Sample component .ts**
```ts
import { Component } from '@angular/core';
@Component({
selector: 'app-root',
templateUrl: './app.component.html',
styleUrls: ['./app.component.less']
})
export class AppComponent {
	title = 'my-dogs-training';
}
```
