
### 1. Angular CLI (Authentication, Routing)
Routing is a mechanism which enables user to navigate between views/components. Angular 2 simplifies the routing and provide flexibility to configure and define at module level (Lazy loading). 

The angular application has single instance of the Router service and whenever URL changes, corresponding Route is matched from the routing configuration array. On successful match, it applies redirects and the router builds a tree of ActivatedRoute objects and contains the current state of the router. Before redirection, the router will check whether new state is permitted by running guards (CanActivate). 

Route Guards is simply an interface method that router runs to check the route authorization. After guard runs, it will resolve the route data and activate the router state by instantiation the required components into `<router-outlet> </router-outlet>`.

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

<br>
<br>

### 2. Angular structure 
![Alt text](images/structure.png?raw=true "Angular Structure")

![alt text](https://angular.io/generated/images/guide/architecture/overview2.png)

<br>
<br>

### 3. Life cycle hooks all
#### Constructor:

1. The **constructor** is a default method runs when component is being constructed.
2. The constructor is a **typescript feature** and it is used only for a class instantiations and nothing to do with Angular2.
3. The constructor called **first time before the ngOnInit()**.

#### ngOnInit():

1. The **ngOnInit** event is an Angular 2 life-cycle event method that is **called after the first ngOnChanges** and the ngOnInit method is use to parameters defined with @Input otherwise the constructor is OK.
2. The ngOnInit is **called after** the **constructor** and ngOnInit is **called after** the **first ngOnChanges.**
3. The **ngOnChanges** is called **when an input or output binding value changes.**


#### Explain the life cycle hooks of Angular 2 application
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


### 4. Change detection 
Two of Angular’s main goals are to be predictable and performant. The framework needs to replicate the state of our application on the UI by combining the state and the template:

![Alt text](images/data-template-dom.png?raw=true "Change detection")

It is also necessary to update the view if any changes happen to the state. This mechanism of syncing the HTML with our data is called “Change Detection”. Each frontend framework uses its implementation, e.g. React uses Virtual DOM, Angular uses change detection and so on. I can recommend the article [Change And Its Detection In JavaScript Frameworks](https://teropa.info/blog/2015/03/02/change-and-its-detection-in-javascript-frameworks.html) which gives a good general overview of this topic.

> Change Detection: The process of updating the view (DOM) when the data has changed

As developers, most of the time we do not need to care about change detection until we need to optimize the performance of our application. Change detection can decrease performance in larger applications if it is not handled correctly.

#### How Change Detection Works
A change detection cycle can be split into two parts:

Developer updates the application model
Angular syncs the updated model in the view by re-rendering it
Let us take a more detailed look at this process:

Developer updates the data model, e.g. by updating a component binding
Angular detects the change
Change detection checks every component in the component tree from top to bottom to see if the corresponding model has changed
If there is a new value, it will update the component’s view (DOM)
The following GIF demonstrates this process in a simplified way:

![Alt text](images/cd-cycle.gif?raw=true "Change detection")


The picture shows an Angular component tree and its change detector (CD) for each component which is created during the application bootstrap process. This detector compares the current value with the previous value of the property. If the value has changed it will set isChanged to true. Check out the implementation in the framework code which is just a === comparison with special handling for NaN.

> Change Detection does not perform a deep object comparison, it only compares the previous and current value of properties used by the template

#### Zone.js
In general, a zone can keep track and intercept any asynchronous tasks.

A zone normally has these phases:

it starts stable
it becomes unstable if tasks run in the zone
it becomes stable again if the tasks completed
Angular patches several low-level browser APIs at startup to be able to detect changes in the application. This is done using zone.js which patches APIs such as EventEmitter, DOM event listeners, XMLHttpRequest, fs API in Node.js and more.

In short, the framework will trigger a change detection if one of the following events occurs:

any browser event (click, keyup, etc.)
setInterval() and setTimeout()
HTTP requests via XMLHttpRequest
Angular uses its zone called NgZone. There exists only one NgZone and change detection is only triggered for async operations triggered in this zone.




<br>
<br>

### View Encapsulation 
### Ngrx basics 
### Redux
### 15 main inbuilt functions of RXJS
### Protractor 
### Dependency injection 
### SCSS css
### Angular material 
### Routing 
### Authentication and authorization 
### JWT tokens 
### Observable 
### Promises 
### Custom directive and pipes 
### Bindings
### Component data sharing types 
### Auth guard 
### Query Params
### Params 
### Services 
### Modules 
### Modular structure division 
### Lazy Loading
### Hoisting in JavaScript
### Testbed
### Spread Operator in JavaScript
### Debugging
### Pure & Impure Pipe in Angular Custom pipe.
### Classical Inheritance & Prototypal Inheritance
### Structural Directives
### Directives and Components
### Just in Time & Ahead/Arrived in Time
### Closure In Java Script Functions In Javascript
### Scope Chain In Javascript
### Java Classes
### Different Ways To Communicate Between Components In Angular
### Promises Vs Observable
### Change Deduction Mechanism In Angular
### Life Cycle Hooks In Angular
### Angular Material
### PrimeNG Library In Angular Material
### How Do You Divide Modules
### Service Worker Module Of Angular
### Attribute Binding Vs Two Way Binding
### Arrow Function And Anonymous Function
### Have you used Forms in Angular ?
### What is Form Control ?
### Difference NG4 & NgF
### Trackby concept
### Differential Loading
