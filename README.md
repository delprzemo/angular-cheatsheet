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

## Sample component ts file
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


| Attribute  | Description |
| ------------- | ------------- |
| changeDetection	  | The change-detection strategy to use for this component.  |
| viewProviders  | 	Defines the set of injectable objects that are visible to its view DOM children  |
| moduleId  | The module ID of the module that contains the component  |
| encapsulation  | 	An encapsulation policy for the template and CSS styles  |
| interpolation  | 	Overrides the default encapsulation start and end delimiters ({{ and }}  |
| entryComponents  | 	A set of components that should be compiled along with this component.  |
| preserveWhitespaces  | 	True to preserve or false to remove potentially superfluous whitespace characters from the compiled template.   |

## Component life cycles

| Life cyccle  | Description |
| ------------- | ------------- |
| ngOnInit  | Called once, after the first ngOnChanges()   |
| ngOnChanges  | Called before ngOnInit() and whenever one of input properties change.   |
| ngOnDestroy  | Called just before Angular destroys the directive/component  |
| ngDoCheck  | Called during every change detection run  |
| ngAfterContentChecked  | Called after the ngAfterContentInit() and every subsequent ngDoCheck()  |
| ngAfterViewChecked  | Called after the ngAfterViewInit() and every subsequent ngAfterContentChecked().  |
| ngAfterContentInit  | Called once after the first ngDoCheck().  |
| ngAfterViewInit  | Called once after the first ngAfterContentChecked().   |

**Template syntax**

| Syntax  | Description |
| ------------- | ------------- |
| {{user.name}}	| Interpolation - just generate user name here  |
| <img [src] = "user.imageUrl">	| property binding - bind image url for user to src attribute  |
| <button (click)="do()" ... />	| Event - assign function to click event  |
| <button *ngIf="user.showSth" ... />	| Show button when user.showSth is true  |
| *ngFor="let item of items"	| Iterate through items list |
| <div [ngClass]="{green: isTrue(), bold: itTrue()}"/> | Angular ngClass attribute  |
| <div [ngStyle]="{'color': isTrue() ? '#bbb' : '#ccc'}"/>	| Angular ngStyle attribute  |


## Content projection
Content projection is injection inner html into child component

Example:

**Parent component template**
```html
<component>
	<div>
		(some html here)
	</div>
</component>
```

**Child component template**
```html 
<ng-content></ng-content>
```
(some html here) will be injection into <ng-content></ng-content>

**Two differents htmls**
```html
<component>
	<div well-title>
		(some html here)
	</div>
	<div well-body>
		(some html here)
	</div>
</component>
```

```html
<ng-content select="title"></ng-content> 
<ng-content select="body"></ng-content>
```

# Routing
The Angular Router enables navigation from one view to the next as users perform application tasks.

**Sample routing ts file**
```ts
const appRoutes: Routes = [
  { path: 'crisis-center', component: CrisisListComponent },
  { path: 'hero/:id',      component: HeroDetailComponent },
  {
    path: 'heroes',
    component: HeroListComponent,
    data: { title: 'Heroes List' }
  },
  { path: '',
    redirectTo: '/heroes',
    pathMatch: 'full'
  },
  { path: '**', component: PageNotFoundComponent }
];
```

Then this should be added inside Angular.module imports
```ts
RouterModule.forRoot(appRoutes)
```

**Usage**
```html
  <a routerLink="/crisis-center" routerLinkActive="active">Crisis Center</a>	
```
routerLinkActive="active" will add active class to element when the link's route becomes active

```ts
//Navigate from code
this.router.navigate(['/heroes']);

// with parameters													
this.router.navigate(['/heroes', { id: heroId, foo: 'foo' }]);

// Receive parameters without Observable
let id = this.route.snapshot.paramMap.get('id');										
 ```
 
## CanActivate/CanDeactivate
Interface that a class can implement to be a guard deciding if a route can be activated. If all guards return true, navigation will continue. 

```ts

class AlwaysAuthGuard implements CanActivate {	
	canActivate() {
		return true;
	}
}
```
and assing it in routing module:

```ts
 {
    path: 'artist/:artistId',
    component: ArtistComponent,
    canActivate: [AlwaysAuthGuard], 
    children: [
      {path: '', redirectTo: 'tracks'},
      {path: 'tracks', component: ArtistTrackListComponent},
      {path: 'albums', component: ArtistAlbumListComponent},
    ]
  }
```

# Modules
Angular apps are modular and Angular has its own modularity system called NgModules. NgModules are containers for a cohesive block of code dedicated to an application domain, a workflow, or a closely related set of capabilities. 

## Sample module with comments

```ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';

@NgModule({
	declarations: [AppComponent], // components, pipes, directives
	imports: [BrowserModule, AppRoutingModule], // other modules
	providers: [], // services
	bootstrap: [AppComponent] // top component
})
export class AppModule { }
```

# Services
Components shouldn't fetch or save data directly and they certainly shouldn't knowingly present fake data. They should focus on presenting data and delegate data access to a service.

**Sample service with one function**
```ts
@Injectable()
export class MyService {
	public items: Item[];
	constructor() { }
	
	getSth() {
		// some implementation
	}
}
```
**Usage**
It should be injected before usage
```ts 
constructor(private dogListService: MyService) 
```

and add in module:

```ts
providers: [MyService]
```

# Animations
Animations - moving from style state to another style state. Before add BrowserModule and BrowserAnimationsModule to module

**Implementation:**
```ts
  animations: [
      trigger('openClose', [
        state('open', style({
          height: '400px',
          opacity: 1.5,
        })),
        state('closed', style({
          height: '100px',
          opacity: 0.5,
        })),
        transition('open => closed', [
          animate('1s')
        ]),
        transition('closed => open', [
          animate('1s')
        ])
      ])
    ]
```

**usage**
```html
<div [@openClose]="isShowed ? 'open' : 'closed'">
```

# Angular Forms

## Template driven forms
Form logic (validation, properties) are kept in template

**sample html**
```html
<form name="form" (ngSubmit)="f.form.valid && onSubmit()" #f="ngForm" novalidate>
                    <div class="form-group">
                        <label for="firstName">First Name</label>
                        <input type="text" class="form-control" name="firstName" [(ngModel)]="model.firstName" #firstName="ngModel" [ngClass]="{ 'is-invalid': f.submitted && firstName.invalid }" required />
                        <div *ngIf="f.submitted && firstName.invalid" class="invalid-feedback">
                            <div *ngIf="firstName.errors.required">First Name is required</div>
                        </div>
                    </div>
                    <div class="form-group">
                        <button class="btn btn-primary">Register</button>
                    </div>
                </form>
```

**sample component**
```ts
@ViewChild("f") form: any;
firstName: string = "";
langs: string[] = ["English", "French", "German"];

onSubmit() {
	if (this.form.valid) {
		console.log("Form Submitted!");
		this.form.reset();
	}
}
```

## Reactive forms
Form logic (validation, properties) are kept in component

**sample html**
```html
<form [formGroup]="registerForm" (ngSubmit)="onSubmit()">
	<div class="form-group">
		<label>Email</label>
		<input type="text" formControlName="email" class="form-control" [ngClass]="{ 'is-invalid': submitted && f.email.errors }" />
		<div *ngIf="submitted && f.email.errors" class="invalid-feedback">
                            <div *ngIf="f.email.errors.required">Email is required</div>
                            <div *ngIf="f.email.errors.email">Email must be a valid email address</div>
 		</div>
	</div>

	<div class="form-group">
		<button [disabled]="loading" class="btn btn-primary">Register</button>
	</div>
 </form>
```

**sample component**
```ts
registerForm: FormGroup;
submitted = false;

constructor(private formBuilder: FormBuilder) { }

ngOnInit() {
	this.registerForm = this.formBuilder.group({
		firstName: [{{here default value}}, Validators.required],
		lastName: ['', Validators.required],
		email: ['', [Validators.required, Validators.email]],
		password: ['', [Validators.required, Validators.minLength(6)]]
	});
}

// convenience getter for easy access to form fields
get f() { return this.registerForm.controls; }

 onSubmit() {
	 this.submitted = true;

	// stop here if form is invalid
	if (this.registerForm.invalid) {
		return;
	}

	alert('SUCCESS!! :-)')
}
```

## Custom Validator for Reactive forms

**Function**
```ts
validateUrl(control: AbstractControl) {
    if (!control.value || control.value.includes('.png') || control.value.includes('.jpg')) {
      return null;
    }
    return { validUrl: true };
  }
```

**Usage**
```ts
this.secondFormGroup = this._formBuilder.group({
      imageCtrl: ['', [Validators.required, this.validateUrl]]
});
```

**Multi-field validation**
```ts
validateNameShire(group: FormGroup) {
    if (group) {
      if (group.get('isShireCtrl').value && !group.get('nameCtrl').value.toString().toLowerCase().includes('shire')) {
	return { nameShire : true };
      }
    }
    return null;
 }
```

**Multi-field validation usage***
```ts
this.firstFormGroup.setValidators(this.validateNameShire);
```

**Error handling**
```html
<div *ngIf="firstFormGroup.controls.nameCtrl.errors.maxlength">Name is too long</div>				
<div *ngIf="firstFormGroup.errors.nameShire">Shire dogs should have "shire" in name</div>
```

## Custom Validator Directive for Template driven forms
To register our custom validation directive to NG_VALIDATORS service we have to do it like this:
(thanks to multi parameter we won't override NG_VALIDATORS but just add CustomValidator to NG_VALIDATORS)

```ts
@Directive({
	selector: '[CustomValidator]',
	providers: [{provide: NG_VALIDATORS, useExisting: CustomValidator, multi:true}]						
})
```
