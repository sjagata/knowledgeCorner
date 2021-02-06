
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

<br>

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


### Change detection 
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
