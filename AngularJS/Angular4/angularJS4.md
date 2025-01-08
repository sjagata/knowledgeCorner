![alt text](https://angular.io/generated/images/guide/architecture/overview2.png)


### What is TypeScript?
TypeScript is a superset to JavaScript, which means, that it compiles into pure JavaScript in
the end. Why do we use it then?
First, it provides ‘strong typing’ (that’s where the name comes from). This means that we can
(and should) assign types to our variables and class members. These types won’t compile to
JavaScript (as JS does not know types) but we will get compilation errors if we assign wrong
types or make any other type-related errors. This is a HUGE help in the daily development
work and should not be underestimated!
Second, TypeScript introduces some nice features, JS does not have out of the box (at least
in the ES5 specification). This includes classes (‘class’ keyword), interfaces, generics and
modules. Being able to use these constructs makes our code cleaner, easier to read and
helps us avoid nasty errors. Especially in combination with the strong typing we are really
able to write high quality code and track down errors quickly.

### Where can I learn all the TypeScript fundamentals?
There are a lot of great resources out there which will get you started very quickly.
The official documentation is not too bad to be honest, so you may give it a try:
http://www.typescriptlang.org/Handbook

### Can we mix TypeScript and JavaScript?
Yes, we can. No one is preventing us from not setting types, using ‘var’ instead of ‘let’ or
using pure JavaScript libraries (i.e. libraries which don’t offer a TypeScript version/
implementation).

### Can’t I use ‘normal’ JavaScript to write Angular 2 applications?
You can absolutely do that. But currently finding good documentation and examples on
Angular 2 using plain JavaScript is extremely hard. And to be honest: TypeScript will be the
standard ‘language’ to be used when developing Angular 2 applications. So I definitely
recommend using TypeScript

### What is Traceur compiler?
Traceur compiler compiles ECMAScript Edition 6 (ES6) (including classes, generators and so on) code on the fly to regular Javascript (ECMAScript Edition 5 [ES5]) to make it compatible for the browser.

**angular-cli:** This is a command line tool for Angularjs 2.0 application development which support live coding and deployment instantly. This is much easier and much straight forward.


Notes ::

* --save to mention production dependency

<br>
<br>

### Key Differences - Constructor Vs. ngOnInit

#### Constructor:

1. The **constructor** is a default method runs when component is being constructed.
2. The constructor is a **typescript feature** and it is used only for a class instantiations and nothing to do with Angular2.
3. The constructor called **first time before the ngOnInit()**.

#### ngOnInit():

1. The **ngOnInit** event is an Angular 2 life-cycle event method that is **called after the first ngOnChanges** and the ngOnInit method is use to parameters defined with @Input otherwise the constructor is OK.
2. The ngOnInit is **called after** the **constructor** and ngOnInit is **called after** the **first ngOnChanges.**
3. The **ngOnChanges** is called **when an input or output binding value changes.**


<br>
<br>

### Explain the life cycle hooks of Angular 2 application
Angular 2 component/directive has lifecycle events, managed by @angular/core. It creates the component, renders it, creates and renders its children, processes changes when its data-bound properties change, and then destroys it before removing its template from the DOM. Angular provides a set of lifecycle hooks(special events) which can be tapped into this lifecycle and perform operations when required. The constructor executes prior to all lifecycle events. Each interface has a single hook method prefixed with ng. For example, ngOnint interface has Oninit method that must be implemented in the component. 

**Some of the events are applicable for both component/directives while few are specific to components:**

* **ngOnChanges** - called after a bound input property changes
* **ngOnInit** - called once the component is initialized
* **ngDoCheck** - called during every change detection run
* **ngOnDestroy** - Called once the componenet is about to be destory // used for clean up

**Component-specific hooks:**

* **ngAfterContentInit** - called after content (ng-content)has been projected into view
* **ngAfterContentChecked** - called every time the projected content has been checked
* **ngAfterViewInit** - called after the componenet's view(and child views) has been initialized
* **ngAfterViewChecked** - Called everytime the view (and child views) has beed checked

Angular2 Lifecycle Events Log:-
1. onChanges
2. onInit
3. doCheck
4. afterContentInit
5. afterContentChecked
6. afterViewInit
7. afterViewChecked
8. doCheck
9. afterContentChecked
10. afterViewChecked
11. onChanges
12. doCheck
13. afterContentChecked
14. afterViewChecked
15. onDestroy

<br>
<br>

### How routing works in Angular 2.
Routing is a mechanism which enables user to navigate between views/components. Angular 2 simplifies the routing and provide flexibility to configure and define at module level (Lazy loading). 

The angular application has single instance of the Router service and whenever URL changes, corresponding Route is matched from the routing configuration array. On successful match, it applies redirects and the router builds a tree of ActivatedRoute objects and contains the current state of the router. Before redirection, the router will check whether new state is permitted by running guards (CanActivate). Route Guards is simply an interface method that router runs to check the route authorization. After guard runs, it will resolve the route data and activate the router state by instantiation the required components into <router-outlet> </router-outlet>.

```js
import { NgModule } from "@angular/core";
import { RouterModule, Routes } from "@angular/router";
import { Users } from "./users";
import { CreateUser } from "./createUser";

let routes: Routes = [
    { path: "", redirectTo: "/users", pathMatch: 'full' },
    { path: 'users', component: Users },
    { path: 'createUser', component: CreateUser },
    { path: 'editUser/:id', component: CreateUser }
];
@NgModule({
    imports: [RouterModule.forRoot(routes)],
    exports: [RouterModule]
})
export class UserRoutes { }
```
```js
export class EditUser{
    constructor(route: ActivatedRoute){
        console.log("User selected:", route.params.value.id);
    }
}
```

[Article](https://www.codeproject.com/Articles/1164813/Angular-Routing)
[Article2](https://vsavkin.com/angular-2-router-d9e30599f9ea)

<br>
<br>

### What are Event Emitters and how it works in Angular 2?
Angular 2 doesn’t have bi-directional digest cycle, unlike angular 1. In angular 2, any change occurred in the component always gets propagated from the current component to all its children in hierarchy. If the change from one component needs to be reflected to any of its parent component in hierarchy, we can emit the event by using Event Emitter api.

In short, EventEmitter is class defined in @angular/core module which can be used by components and directives to emit custom events.

```js
@output() somethingChanged = new EventEmitter();
```
We use somethingChanged.emit(value) method to emit the event. This is usually done in setter when the value is being changed in the class.
This event emit can be subscribed by any component of the module by using subscribe method.
```js
myObj.somethingChanged.subscribe(val) => this.myLocalMethod(val));
```

[Article](https://stackoverflow.com/questions/36076700/what-is-the-proper-use-of-an-eventemitter)
[API](https://angular.io/api/core/EventEmitter)

<br>
<br>

### What is the use of codelyzer in angular 2 application.
All enterprise applications follows a set of coding conventions and guidelines to maintain code in better way. Codelyzer is an open source tool to run and check whether the pre-defined coding guidelines has been followed or not. Codelyzer does only static code analysis for angular and typescript project.

Codelyzer runs on top of tslint and its coding conventions are usually defined in tslint.json file. Codelyzer can be run via angular cli or npm directly. Editors like Visual Studio Code and Atom also supports codelyzer just by doing a basic settings.

To set up the codelyzer in Visual Studio code, we can go to File -> Preferences -> User Settings and add the path for tslint rules.

<br>
<br>

### What is lazy loading and How to enable lazy loading in angular 2?
Most of the enterprise application contains various modules for specific business cases. Bundling whole application code and loading will be huge performance impact at initial call. Lazy lading enables us to load only the module user is interacting and keep the rest to be loaded at runtime on demand.

Lazy loading speeds up the application initial load time by splitting the code into multiple bundles and loading them on demand.

Every Angular application must have one main module say AppModule. The code should be splitted into various child modules (NgModule) based on the application business case.

1. We don't require to import or declare lazily loading module in root module.
2. Add the route to top level routing (app.routing.ts) and set **loadChildren**. loadChildren takes **absolute path from root folder followed by #{ModuleName}.** **RouterModule.forRoot()** takes routes array and configures the router.
3. Import module specific routing in the child module.
4. In the child module routing, specify path as empty string ' ', the empty path. **RouterModule.forChild** again takes routes array for the child module components to load and configure router for child.
5. Then, export const routing: `ModuleWithProviders = RouterModule.forChild(routes);`

```js
const routes: Routes = [
  { path: '', redirectTo: 'eager', pathMatch: 'full' },
  { path: 'eager', component: EagerComponent },
  { path: 'lazy', loadChildren: 'app/lazy/lazy.module#LazyModule' }
];

export const routing: ModuleWithProviders = RouterModule.forRoot(routes);
```
```js
import { NgModule } from '@angular/core';

import { LazyComponent }   from './lazy.component';
import { routing } from './lazy.routing';

@NgModule({
  imports: [routing],
  declarations: [LazyComponent]
})
export class LazyModule {}
```
```js
const routes: Routes = [
  { path: '', component: LazyComponent }
];

export const routing: ModuleWithProviders = RouterModule.forChild(routes);
```

[plnkr](https://plnkr.co/edit/PNwh0Mn2ZJighpSoOTtw?p=info)

<br>
<br>

### @Inject and @Injectable
`@Inject()` is a manual mechanism for letting Angular know that a parameter must be injected. It can be used like so 
```js
import { Component, Inject } from '@angular/core';
import { ChatWidget } from '../components/chat-widget';

@Component({
  selector: 'app-root',
  template: `Encryption: {{ encryption }}`
})
export class AppComponent {
  encryption = this.chatWidget.chatSocket.encryption;

  constructor(@Inject(ChatWidget) private chatWidget) { }
}
```
In the above we've asked for chatWidget to be the **singleton** Angular associates with the class symbol ChatWidget by calling `@Inject(ChatWidget)`. It's important to note that we're using ChatWidget for its typings and as a reference to its singleton. We are not using ChatWidget to instantiate anything, Angular does that for us behind the scenes.

`@Injectable()` lets Angular know that a class can be used with the dependency injector.

`@Injectable()` is not strictly required if the class has other Angular decorators on it or does not have any dependencies. What is important is that any class that is going to be injected with Angular is decorated. However, best practice is to decorate injectables with `@Injectable()`, as it makes more sense to the reader.

Here's an example of ChatWidget marked up with `@Injectable`:
```js
import { Injectable } from '@angular/core';
import { AuthService } from './auth-service';
import { AuthWidget } from './auth-widget';
import { ChatSocket } from './chat-socket';

@Injectable()
export class ChatWidget {
  constructor(
    public authService: AuthService,
    public authWidget: AuthWidget,
    public chatSocket: ChatSocket) { }
}
```
In the above example Angular's injector determines what to inject into ChatWidget's constructor by using type information. This is possible because these particular dependencies are typed, and are not primitive types. In some cases Angular's DI needs more information than just types.

<br>
<br>

### What are the security threats should we be aware of in angular 2 application?
Just like any other client side or web application, angular 2 application should also follow some of the basic guidelines to mitigate the security risks. Some of them are:

1. Avoid using/injecting dynamic Html content to your component.
2. If using external Html, that is coming from database or somewhere outside the application, sanitize it.
3. Try not to put external urls in the application unless it is trusted. Avoid url re-direction unless it is trusted.
4. Consider using AOT compilation or offline compilation.
5. Try to prevent XSRF attack by restricting the api and use of the app for known or secure environment/browsers.


<br>
<br>

### What is AOT compilation?
AOT compilation stands for Ahead Of Time compilation, in which the angular compiler compiles the angular components and templates to native JavaScript and HTML during the build time. The compiled Html and JavaScript is deployed to the web server so that the compilation and render time can be saved by the browser.

#### Advantages

* **Faster download:** Since the app is already compiled, many of the angular compiler related libraries are not required to be bundled, the app bundle size get reduced. So, the app can be downloaded faster.
* **Lesser No. of Http Requests:** If the app is not bundled to support lazy loading (or whatever reasons), for each associated html and css, there is a separate request goes to the server. The pre-compiled application in-lines all templates and styles with components, so the number of Http requests to the server would be lesser.
* **Faster Rendering:** If the app is not AOT compiled, the compilation process happens in the browser once the application is fully loaded. This has a wait time for all necessary component to be downloaded, and then the time taken by the compiler to compile the app. With AOT compilation, this is optimized.
* **Detect error at build time:** Since compilation happens beforehand, many compile time error can be detected, providing a better degree of stability of application.

#### Disadvantages

* Works only with HTML and CSS, other file types need a previous build step
* No watch mode yet, must be done manually (bin/ngc-watch.js) and compiles all the files
* Need to maintain AOT version of bootstrap file (might not be required while using tools like cli)
* Needs cleanup step before compiling

<br>
<br>

### What are the core differences between Observables and Promises?
A **Promise** handles a **single event** when an async operation completes or fails.

Note: There are Promise libraries out there that support cancellation, but ES6 Promise doesn't so far.

An **Observable** is like a **Stream** (in many languages) and allows to pass zero or more events where the callback is called for each event. Often Observable is preferred over Promise because it provides the features of Promise and more. With Observable it doesn't matter if you want to handle 0, 1, or multiple events. You can utilize the same API in each case. Observable also has the advantage over Promise to be **cancelable**. If the result of an HTTP request to a server or some other expensive async operation isn't needed anymore, the Subscription of an Observable allows to cancel the subscription, while a Promise will eventually call the success or failed callback even when you don't need the notification or the result it provides anymore. Observable provides **operators** like map, forEach, reduce, ... similar to an array. There are also powerful operators like retry(), or replay(), ... that are often quite handy.

#### Promises vs Observables

#### Promises:
* returns a single value
* not cancellable

#### Observables:
Observable:
Various Data sources (User Input) events, Http Requests, Triggered in code,..

Observable might emit a couple normal data packages, it might have been an error or eventually it might get completed and the respective code is then executed in observer

Observer:
You write the code which gets executed!
Handle Data, Handle Error, Handle Completion

Both **Promises and Observables** provide us with abstractions that help us deal with the **asynchronous nature of our applications.** 

However, there are important differences between the two:
* As seen in the example above, **Observables** can define both the setup and teardown aspects of asynchronous behavior.
* Observables are cancellable.
* Moreover, **Observables** can be retried using one of the retry operators provided by the API, such as **retry** and **retryWhen**. On the other hand, **Promises** require the caller to have access to the original function that returned the promise in order to have a retry capability.


* works with multiple values over time
* cancellable
* supports map, filter, reduce and similar operators
* proposed feature for ES 2016
* use Reactive Extensions (RxJS)
* an array whose items arrive asynchronously over time

Ex: params is a observable

```js
  ngOnInit() {
    this.user = {
      id: this.route.snapshot.params['id'],
      name: this.route.snapshot.params['name']
    };
    this.paramsSubscription = this.route.params
      .subscribe(
        (params: Params) => {
          this.user.id = params['id'];
          this.user.name = params['name'];
        }
      );
  }

  ngOnDestroy() {
    this.paramsSubscription.unsubscribe();
  }
```
    

<br>
<br>

### Angular 2 is written entirely in Typescript and meets the ECMAScript 6 specification :
* **Component-Based** - Angular 2 is entirely component based. Controllers and $scope are no longer used. They have been replaced by components and directives.
* **Directives** - The specification for directives is considerably simplified, although they are still subject to change. With the @Directive annotation, a directive can be declared.
* **Dependency Injection** - Because of the improved dependency injection model in Angular2 there are more opportunities for component / object-based work.
* **Use of TypeScript** - TypeScript is a typed super set of JavaScript which has been built and maintained by Microsoft and chosen by the AngularJS team for development. The presence of types makes the code written in TypeScript less prone to run-time errors. In recent times, the support for ES6 has been greatly improved and a few features from ES7 have been added as well.
* **Generics** - TypeScript has generics which can be used in the frontend.
* **Lambdas with TypeScript** - In TypeScript, lambdas are available.
* **Forms and Validations** - Forms and validations are an important aspect of frontend development. Within Angular 2 the Form Builder and Control Group are defined.

<br>
<br>

### What Is The Need Of Angular2?
Angular 2 is not just a typical upgrade but a totally new development. The whole framework is rewritten from the ground. Angular 2 got rid of many things like $scope, controllers, DDO, jqLite, angular.module etc.

It uses components for almost everything. Imagine that even the whole app is now a component. Also it takes advantage of ES6 / TypeScript syntax. Developing Angular 2 apps in TypeScript has made it even more powerful.

Apart from that, many things have evolved and re-designed like the template engine and many more.

<br>
<br>

### What Is @ngmodule?
**@NgModule** is a decorator function. A decorator function allows users to mark something as Angular 2 thing (could be a module or component or something else) and it enables you to provide additional data that determines how this Angular 2 thing will be processed, instantiated and used at the runtime. So, whenever user writes @NgModule, it tells the Angular 2 module, what’s going to be included and used in and using this module.

<br>
<br>

### What Is Component In Angularjs 2 ?
In Angular, a Component is a special kind of directive that uses a simpler configuration which is suitable for a component-based application structure.

<br>
<br>

### What Is @inputs In Angular 2?
**@Input** allows you to pass data into your controller and templates through html and defining custom properties. This allows you to easily reuse components and have them display different values for each instance of the renderer.
* **@Input** is used to define an input for a component, we use the @Input decorator.

<br>
<br>

### What Is @outputs In Angular?
Components push out events using a combination of an **@Output** and an EventEmitter. This allows a clean separation between reusable Components and application logic.
**@Output** decorator is used to binds a property of a component to send the data from child component to parent component and this is a one-way communication.

<br>
<br>

### What is hidden property in Angular2?
Angular 2 [hidden] is a special case binding to hidden property.
It is closest cousin of `ng-show` and `ng-hide`.
It is more powerful to bind any property of elements. Both the ng-show and ng-hide are used to manage the visibility of elements using ng-hide css class. It is also set the display property “display:none”.
```js
import { Component } from 'angular2/core';

@Component({
  selector: 'demo',
  templateUrl: 'app/component.html'
})
export class MainComponent {
  Ishide: true;
}
```
```html
<div [hidden]="Ishide">
     Hey, I’m using hidden attribute.
</div>
```

<br>
<br>

### What is the Best way to Declare and Access a Global Variable in Angular 2?
* Create Global Variables :- “app.global.ts”
```js
import { Injectable } from '@angular/core';

@Injectable()
export class AppGlobals {
    readonly baseAppUrl: string = 'http://localhost:57431/';
    readonly baseAPIUrl: string = 'https://api.github.com/';
}

```

* Import and Use the Global Variables in the Component.
```js

import { Component, Injectable} from '@angular/core';
import { CommonModule } from '@angular/common';
import { HttpModule, Http } from '@angular/http';
import { UserService } from '../service/user.service';
import { AppGlobals } from '../shared/app.globals';


@Component({
    selector: 'user',
    templateUrl: './user.component.html',
    styleUrls: ['./user.component.css'],
    providers: [UserService, AppGlobals]
})

export class UserComponent {
    //USERS DECLARATIONS.
    users = [];

    //HOME COMPONENT CONSTRUCTOR
    constructor(private userService: UserService, private _global: AppGlobals) { }

    //GET USERS SERVICE ON PAGE LOAD.
    ngOnInit() {
        this.userService.getAPIUsers(this._global.baseAPIUrl + 'users/hadley/orgs').subscribe(data => this.users = data);
        this.userService.getAppUsers(this._global.baseAppUrl + 'api/User/GetUsers').subscribe(data => console.log(data));  
    }
}
//END BEGIN – USERCOMPONENT

“user.server.ts” :-

import { Injectable, InjectionToken } from '@angular/core';
import { Http, Response } from '@angular/http';
import 'rxjs/add/operator/map';

//BEGIN-REGION - USERSERVICE
@Injectable()
export class UserService {
    constructor(private _http: Http) {
    }

    getAPIUsers(apiUrl) {
        return this._http.get(apiUrl).map((data: Response) => data.json());
    }

    getAppUsers(apiUrl) {
        return this._http.get(apiUrl).map((data: Response) => data);
    }
}
//END BEGIN – USERSERVICE
```

<br>
<br>

### Angular 2 components vs directives
* A @Component requires a view whereas a @Directive does not.

#### Directives
* Directives add behaviour to an existing DOM element or an existing component instance. One example use case for a directive would be to log a click on an element.
```js
import {Directive} from '@angular/core';

@Directive({
    selector: "[logOnClick]",
    hostListeners: {
        'click': 'onClick()',
    },
})
class LogOnClick {
    constructor() {}
    onClick() { console.log('Element clicked!'); }
}
```
```html
<button logOnClick>I log when clicked!</button>
```

#### Components
* A component, rather than adding/modifying behaviour, actually creates its own view (hierarchy of DOM elements) with attached behaviour. An example use case for this might be a contact card component:
```js
import {Component, View} from '@angular/core';

@Component({
  selector: 'contact-card',
  template: `
    <div>
      <h1>{{name}}</h1>
      <p>{{city}}</p>
    </div>
  `
})
class ContactCard {
  @Input() name: string
  @Input() city: string
  constructor() {}
}
```
```html
<contact-card [name]="'foo'" [city]="'bar'"></contact-card>
```
`ContactCard` is a reusable UI component that we could use anywhere in our application, even within other components. These basically make up the UI building blocks of our applications.


* Write a **component** when you want to create a reusable set of DOM elements of UI with custom behaviour. 
* Write a **directive** when you want to write reusable behaviour to supplement existing DOM elements.

<br>
<br>

### How do we display errors in a component view with Angular 2?
the ngModel provides error objects for each of the built-in input validators. You can access these errors from a reference to the ngModel itself then build useful messaging around them to display to your users.

<br>
<br>

### ElementRef vs Renderer - Angular 2
ElementRef vs. Renderer -
In Angular Renderer and ElementRef are used for DOM Manipulation and Renderer and ElementRef are used together to get full platform abstraction.

#### Renderer –
Renderer is a class that is a partial abstraction done the DOM manipulations and the DOM manipulating is not breaking server side rendering or web workers.

#### ElementRef –
ElementRef is a class that is a partial abstraction done the DOM Manipulations without breakable environments and it also can hold a reference to a DOM elements.

If “ElementRef” is injected to a component, the injected instance is a reference to the host element of the current component.

The ways to get an ElementRef instance looks like,
1. @ViewChild()
2. @ViewChildren()
3. @ContentChild()
4. @ContentChildren()

In this case the ElementRef is a reference to the matching elements in the templates.

Do notice that you should refrain from using ElementHref as it flagged with a security risk?
If you allow direct access to the DOM, it can make your application more vulnerable to XSS attacks. So make sure, when you are using to ElementRef in your app code.

What is the point of calling renderer.invokeElementMethod(rendererEl, methodName)?

<br>
<br>



### Explain local reference variables, ViewChild, and ContentChild.
Local template variables in angular2 is used to refer HTML elements and use their properties to access siblings or children.

Let’s consider you have an input field named username.
```html
<input type="text" required ... />
```

This HTMLInputField can be made available to the template using # symbol with a variable name say username.
```html
 <input type="text" #username required ... />
```

Now, this HTMLInputElement can be accessed from anywhere in the current template for example, checking validation and showing appropriate message based on the validation rule. But, username HTML reference is not accessible in the component/directive.

To access this in the component, angular 2 provides @ViewChild decorator which accepts the local reference variable.
```js
@ViewChild('username') username: HTMLInputElement;
```

**ViewChild** element can be read after the view is initialized (`ngAfterViewInit`).

**ContentChild** is used to query the reference of the DOM within ng-content. Content Child are set before the `ngAfterContentInit` lifecycle hook.

```js
// <code>app.component.ts</code>
<my-component>
   <p #contentRef>{{test}}</p>
</my-component>
 
// MyComponent.component.ts
@Component({
   selector: ‘my-component',
   template: `
    <ng-content></ng-content>
    <div>ContentChild Example </div>`
})
export class LifecycleComponent implements ngAfterContentInit{
  @ContentChild(‘contentRef’)   childContent: HTMLElement;
  
  ngAfterContentInit() {
    this.log('ngAfterContentInit');
    console.log(this.childContent);
  }
}
```

<br>
<br>

### What's the difference between @ViewChild and @ContentChild?
`@ContentChild` and `@ContentChildren` queries will return directives existing inside the <ng-content></ng-content> element of your view, whereas `@ViewChild` and  `@ViewChildren` only look at elements that are on your view template directly.


<br>
<br>

### What is router-outlet directive in AngularJS2?
`<router-outlet> </router-outlet>` is used to instantiation the required components into it
* To load the coponent of the currently selected route.

<br>
<br>

### What is a structural directive?
#### Attribute Directives :
Because they set on elements just like attribute 
Never destroy an element from the DOM it only change the properties of that element, example: back-ground color
1. Looks like a normal HTML attribute(possibly with databinding or event binding)
2. Only affect/change the element they are added to.
Example : `ngClass`, `ngStyle`

#### Structural Directives :
Basically do the same but they also changes the structure of the DOM around this element
Ex: `*ngIf` removing and showing the DOM elements, `*ngFor`
1. Look like a normal HTML attribute but have a leading `*`(for desugaring)
2. Affect a whole area in the DOM(elements get added/removed)

* we cannot have two structural directive on single element

`@HostBinding`
`@HostListner`

`@HostBinding` and `@HostListener` are two decorators in Angular that can be really useful in custom directives. `@HostBinding` lets you **set properties on the element or component** that hosts the directive, and `@HostListener` lets you **listen for events on the host element or component.**

```js
import {
  Directive,
  Renderer2,
  OnInit,
  ElementRef,
  HostListener,
  HostBinding,
  Input
} from '@angular/core';

@Directive({
  selector: '[appBetterHighlight]'
})
export class BetterHighlightDirective implements OnInit {
  @Input() defaultColor: string = 'transparent';
  @Input('appBetterHighlight') highlightColor: string = 'blue';
  @HostBinding('style.backgroundColor') backgroundColor: string;

  constructor(private elRef: ElementRef, private renderer: Renderer2) { }

  ngOnInit() {
    this.backgroundColor = this.defaultColor;
    // this.renderer.setStyle(this.elRef.nativeElement, 'background-color', 'blue');
  }

  @HostListener('mouseenter') mouseover(eventData: Event) {
    // this.renderer.setStyle(this.elRef.nativeElement, 'background-color', 'blue');
    this.backgroundColor = this.highlightColor;
  }

  @HostListener('mouseleave') mouseleave(eventData: Event) {
    // this.renderer.setStyle(this.elRef.nativeElement, 'background-color', 'transparent');
    this.backgroundColor = this.defaultColor;
  }

}
```

### routerLink
Router link is able to parse the string that which we pass and loads component.
* It handles the click differently 
* It helps to maintain the state
* It catches to click on the element precents the default which would be to send the request and instead analyzes what we passed to the router link directive and checks the fitting route in configuration

```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <ul class="nav nav-tabs">
        <li role="presentation"
            routerLinkActive="active"
            [routerLinkActiveOptions]="{exact: true}">
          <a routerLink="/">Home</a>
        </li>
        <li role="presentation"
            routerLinkActive="active">
          <a routerLink="servers">Servers</a>
        </li>
        <li role="presentation"
            routerLinkActive="active">
          <a [routerLink]="['users']">Users</a>
        </li>
      </ul>
    </div>
  </div>
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <router-outlet></router-outlet>
    </div>
  </div>
</div>
```

### routerLinkActive
routerLinkActive - sets the class if that url is opted. <br>

routerLinkActiveOptions - tells angular that if the url is full exact means, slash the set true

```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <ul class="nav nav-tabs">
        <li role="presentation"
            routerLinkActive="active"
            [routerLinkActiveOptions]="{exact: true}">
          <a routerLink="/">Home</a>
        </li>
        <li role="presentation"
            routerLinkActive="active">
          <a routerLink="servers">Servers</a>
        </li>
        <li role="presentation"
            routerLinkActive="active">
          <a [routerLink]="['users']">Users</a>
        </li>
      </ul>
    </div>
  </div>
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <router-outlet></router-outlet>
    </div>
  </div>
</div>
```

### Navigate Programically and pass queryparams and fragment

* use `router.navigate` to navigate programatically.
```js
export class HomeComponent implements OnInit {

  constructor(private router: Router, private authService: AuthService) { }

  ngOnInit() {
  }

  onLoadServer(id: number) {
    // complex calculation
    this.router.navigate(['/servers', id, 'edit'], {queryParams: {allowEdit: '1'}, fragment: 'loading'});
  }
}
```
* `ActivatedRoute` is to pass the current route
```js
  constructor(private serversService: ServersService,
      private router: Router,
      private route: ActivatedRoute) {
  }
this.router.navigate(['servers'], {relativeTo: this.route});
```

### queryParams & fragment
on click url be :

localhost:4200/servers/5/edit?allowEdit=1#loading

```html
    <div class="list-group">
      <a
        [routerLink]="['/servers', server.id]"
        [queryParams]="{allowEdit: server.id === 3 ? '1' : '0'}"
        fragment="loading"
        href="#"
        class="list-group-item"
        *ngFor="let server of servers">
        {{ server.name }}
      </a>
    </div>
  </div>
```

* Retreving/Accessing queryParams & fragment using ActivatedRoute
```js
  constructor(private serversService: ServersService,
      private route: ActivatedRoute,
      private router: Router) {
  }
  
  console.log(this.route.snapshot.queryParams);
  console.log(this.route.snapshot.fragment);
  this.route.queryParams
      .subscribe(
        (queryParams: Params) => {
          this.allowEdit = queryParams['allowEdit'] === '1' ? true : false;
        }
      );
  this.route.fragment.subscribe();
```

### Child(Nested) Routes:
```js
const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent, children: [
    { path: ':id/:name', component: UserComponent }
  ] },
  {
    path: 'servers',
    // canActivate: [AuthGuard],
    canActivateChild: [AuthGuard],
    component: ServersComponent,
    children: [
    { path: ':id', component: ServerComponent, resolve: {server: ServerResolver} },
    { path: ':id/edit', component: EditServerComponent, canDeactivate: [CanDeactivateGuard] }
  ] },
  // { path: 'not-found', component: PageNotFoundComponent },
  { path: 'not-found', component: ErrorPageComponent, data: {message: 'Page not found!'} },
  { path: '**', redirectTo: '/not-found' }
];

@NgModule({
  imports: [
    // RouterModule.forRoot(appRoutes, {useHash: true})
    RouterModule.forRoot(appRoutes)
  ],
  exports: [RouterModule]
})
export class AppRoutingModule {

}
```

<br>
<br>

### FORMS

Two Approaches:

1. Template-Driven : Angular infers the Form Object from the DOM
2. Reactive : Form is created programamatically and synchronized with the DOM


<br>
<br>

### Pipes

### What is Pipes? Why use Pipes?
Pipes are feature built into angular to which bascially allows you to transform output in your template
Something like filters in angular 1


### What is a pure and impure pipe?
Pure Pipes: Default behavior. Executed only when the input data changes.
Example: Formatting text, filtering a static list.

Impure Pipes: Set pure: false in the pipe decorator. Executed every change detection cycle.
Example: A pipe working with dynamic or mutable data like an array updated by reference.

Filter pipe wont trigger while updating Arrays or Objects 
We can enforce the pipe to be updated whenever the data changes by adding a second property to the pipe **(pure: false)**
```js
@Pipe({
  name: 'filter',
  pure: false
})
```
This is a performance hit

### What is Async Pipe?
* This is used to help us transform data we gat asynchronously and output in the template.


Without **async** it will display [object object](since promise is a object) because angular doesn't know
But we know after 2 seconds it gonna be a string
So here we can use buil-in pipe called **async**

* It recognizes that this is a promise and a side note it would also work ith observables there it would subscribe automatically and after 2 seconds it would simply reconize that something changed that the promise resolved or inthe case of an observable that data was sent from the subscription 

```js
  appStatus = new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('stable');
    }, 2000);
  });
```
```html
 <h2>App Status: {{ appStatus | async}}</h2>
 ```


### How to create and use a custom Pipes?
By implementing PipeTransform

```js
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'shorten'
})
export class ShortenPipe implements PipeTransform {
  transform(value: any, limit: number) {
    if (value.length > limit) {
      return value.substr(0, limit) + ' ...';
    }
    return value;
  }
}
```
### Pipes Example
```js
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'filter',
  pure: false
})
export class FilterPipe implements PipeTransform {

  transform(value: any, filterString: string, propName: string): any {
    if (value.length === 0 || filterString === '') {
      return value;
    }
    const resultArray = [];
    for (const item of value) {
      if (item[propName] === filterString) {
        resultArray.push(item);
      }
    }
    return resultArray;
  }

}
```
```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <input type="text" [(ngModel)]="filteredStatus">
      <br>
      <button class="btn btn-primary" (click)="onAddServer()">Add Server</button>
      <br><br>
      <h2>App Status: {{ appStatus | async}}</h2>
      <hr>
      <ul class="list-group">
        <li
          class="list-group-item"
          *ngFor="let server of servers | filter:filteredStatus:'status'"
          [ngClass]="getStatusClasses(server)">
          <span
            class="badge">
            {{ server.status }}
          </span>
          <strong>{{ server.name | shorten:15 }}</strong> |
          {{ server.instanceType | uppercase }} |
          {{ server.started | date:'fullDate' | uppercase }}
        </li>
      </ul>
    </div>
  </div>
</div>
```

<br>
<br>

### HTTP CLient

### How HTTP Client interact with AngularJs2 servers?
check below example
We have to import HttpModule otherwise Http service will not be possible.

```js
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

import { AppComponent } from './app.component';
import { ServerService } from './server.service';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule
  ],
  providers: [ServerService],
  bootstrap: [AppComponent]
})
export class AppModule { }
```


### What is the best way to inject once service into another service?
**@Injectable** decorator is used to inject a service into another a service. 
* so instead dispose method of the built in HTTP service here will only an observable so we have simple return 
* Transform responses easily with Observable Operators(map()).
* catch operator is used catch errors and we have to return Observables.throw() method.
* Pipes is used to help us transform data we gat asynchronously and output in the template. - if you see we are not returning Observable - it automatically transform the data

```js
return this.http.post('https://udemy-ng-http.firebaseio.com/data.json',
```
and subscribe it in component
```js
this.serverService.storeServers(this.servers)
  .subscribe(
    (response) => console.log(response),
    (error) => console.log(error)
  );
```

Angular is using observables behind the scene
```js
import { Injectable } from '@angular/core';
import { Headers, Http, Response } from '@angular/http';
import 'rxjs/Rx';
import { Observable } from 'rxjs/Observable';

@Injectable()
export class ServerService {

  constructor(private http: Http) {}
  
  storeServers(servers: any[]) {
    const headers = new Headers({'Content-Type': 'application/json'});
    // return this.http.post('https://udemy-ng-http.firebaseio.com/data.json',
    //   servers,
    //   {headers: headers});
    return this.http.put('https://udemy-ng-http.firebaseio.com/data.json',
      servers,
      {headers: headers});
  }
  getServers() {
    return this.http.get('https://udemy-ng-http.firebaseio.com/data')
      .map(
        (response: Response) => {
          const data = response.json();
          for (const server of data) {
            server.name = 'FETCHED_' + server.name;
          }
          return data;
        }
      )
      .catch(
        (error: Response) => {
          return Observable.throw('Something went wrong');
        }
      );
  }
  getAppName() {
    return this.http.get('https://udemy-ng-http.firebaseio.com/appName.json')
      .map(
        (response: Response) => {
          return response.json();
        }
      );
  }
}
```
```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <h1>{{ appName | async }}</h1>
      <input type="text" #serverName>
      <button class="btn btn-primary" (click)="onAddServer(serverName.value)">Add Server</button>
      <br><br>
      <button class="btn btn-primary" (click)="onSave()">Save Servers</button>
      <button class="btn btn-primary" (click)="onGet()">Get Servers</button>
      <hr>
      <ul class="list-group" *ngFor="let server of servers">
        <li class="list-group-item">{{ server.name }} (ID: {{ server.id }})</li>
      </ul>
    </div>
  </div>
</div>
```
```js
import { Component } from '@angular/core';
import { Response } from '@angular/http';

import { ServerService } from './server.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  appName = this.serverService.getAppName();
  servers = [
    {
      name: 'Testserver',
      capacity: 10,
      id: this.generateId()
    },
    {
      name: 'Liveserver',
      capacity: 100,
      id: this.generateId()
    }
  ];
  constructor(private serverService: ServerService) {}
  onAddServer(name: string) {
    this.servers.push({
      name: name,
      capacity: 50,
      id: this.generateId()
    });
  }
  onSave() {
    this.serverService.storeServers(this.servers)
      .subscribe(
        (response) => console.log(response),
        (error) => console.log(error)
      );
  }
  onGet() {
    this.serverService.getServers()
      .subscribe(
        (servers: any[]) => this.servers = servers,
        (error) => console.log(error)
      );
  }
  private generateId() {
    return Math.round(Math.random() * 10000);
  }
}
```

<br>
<br>

### Whats new in Angular4
* Improved `*ngIf` and `*ngFor`
    * You can now use an if/else style syntax, and assign local variables such as when unrolling an observable.
```html
<div *ngIf="userList | async as users; else loading">
  <user-profile *ngFor="let user of users; count as count; index as i" [user]="user">
    User {{i}} of {{count}}
  </user-profile>
</div>
<ng-template #loading>Loading...</ng-template>
```
* renderer2
deprecated but still works but will remove in furture
```js
this.renderer.setElementStyle(element, 'background-color', 'red');
```
to 
```js
this.renderer.setStyle(element, 'background-color', 'red');
```

* email validator - we can remove pattern and simple use 'email' in input field
* typescript 2 support
* animation packages
earlier we used to get trigger, state, transition from angular/core now angular/animations import changed and also we have to add BrowserAnimationModule 























