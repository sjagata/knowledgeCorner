
### Angular CLI (Authentication, Routing)
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


### Angular structure 
### Life cycle hooks all
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
