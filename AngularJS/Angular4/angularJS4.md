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



Notes ::

* --save to mention production dependency



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
2. Add the route to top level routing (app.routing.ts) and set loadChildren. loadChildren takes absolute path from root folder followed by #{ModuleName}. RouterModule.forRoot() takes routes array and configures the router.
3. Import module specific routing in the child module.
4. In the child module routing, specify path as empty string ' ', the empty path. RouterModule.forChild again takes routes array for the child module components to load and configure router for child.
5. Then, export const routing: ModuleWithProviders = RouterModule.forChild(routes);

[plnkr](https://plnkr.co/edit/PNwh0Mn2ZJighpSoOTtw?p=info)


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
* works with multiple values over time
* cancellable
* supports map, filter, reduce and similar operators
* proposed feature for ES 2016
* use Reactive Extensions (RxJS)
* an array whose items arrive asynchronously over time

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

### Angular 2 is written entirely in Typescript and meets the ECMAScript 6 specification :
* **Component-Based** - Angular 2 is entirely component based. Controllers and $scope are no longer used. They have been replaced by components and directives.
* **Directives** - The specification for directives is considerably simplified, although they are still subject to change. With the @Directive annotation, a directive can be declared.
* **Dependency Injection** - Because of the improved dependency injection model in Angular2 there are more opportunities for component / object-based work.
* **Use of TypeScript** - TypeScript is a typed super set of JavaScript which has been built and maintained by Microsoft and chosen by the AngularJS team for development. The presence of types makes the code written in TypeScript less prone to run-time errors. In recent times, the support for ES6 has been greatly improved and a few features from ES7 have been added as well.
* **Generics** - TypeScript has generics which can be used in the frontend.
* **Lambdas with TypeScript** - In TypeScript, lambdas are available.
* **Forms and Validations** - Forms and validations are an important aspect of frontend development. Within Angular 2 the Form Builder and Control Group are defined.









