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

```angularjs
@output() somethingChanged = new EventEmitter();
```


















