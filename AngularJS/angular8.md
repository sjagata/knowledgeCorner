
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

### 3. Life Cycle Hooks In Angular
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


The picture shows an Angular component tree and its change detector (CD) for each component which is created during the application bootstrap process. This detector compares the current value with the previous value of the property. If the value has changed it will set isChanged to true. Check out [the implementation in the framework code](https://github.com/angular/angular/blob/885f1af509eb7d9ee049349a2fe5565282fbfefb/packages/core/src/util/comparison.ts#L13) which is just a === comparison with special handling for NaN.

> Change Detection does not perform a deep object comparison, it only compares the previous and current value of properties used by the template

#### Zone.js
In general, a zone can keep track and intercept any asynchronous tasks.

A zone normally has these phases:

* it starts stable
* it becomes unstable if tasks run in the zone
* it becomes stable again if the tasks completed

Angular patches several low-level browser APIs at startup to be able to detect changes in the application. This is done using zone.js which patches APIs such as `EventEmitter`, DOM event listeners, `XMLHttpRequest`, fs API in Node.js and more.

In short, the framework will trigger a change detection if one of the following events occurs:

* any browser event (click, keyup, etc.)
* `setInterval()` and `setTimeout()`
* HTTP requests via `XMLHttpRequest`

Angular uses its zone called `NgZone`. There exists only one NgZone and change detection is only triggered for async operations triggered in this zone.

[ref](https://www.mokkapps.de/blog/the-last-guide-for-angular-change-detection-you-will-ever-need/)

<br>
<br>

### 5. View Encapsulation 
In Angular, component CSS styles are encapsulated into the component's view and don't affect the rest of the application.

To control how this encapsulation happens on a per component basis, you can set the view encapsulation mode in the component metadata. Choose from the following modes:

* `ShadowDom` view encapsulation uses the browser's native shadow DOM implementation (see [Shadow DOM](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM)) to attach a shadow DOM to the component's host element, and then puts the component view inside that shadow DOM. The component's styles are included within the shadow DOM.

* `Emulated` view encapsulation (the default) emulates the behavior of shadow DOM by preprocessing (and renaming) the CSS code to effectively scope the CSS to the component's view.

* `None` means that Angular does no view encapsulation. Angular adds the CSS to the global styles. The scoping rules, isolations, and protections discussed earlier don't apply. This is essentially the same as pasting the component's styles into the HTML.

To set the component's encapsulation mode, use the encapsulation property in the component metadata:

```js
// src/app/quest-summary.component.ts

// warning: few browsers support shadow DOM encapsulation at this time
encapsulation: ViewEncapsulation.ShadowDom
```

<br>
<br>

### 6. Ngrx basics 
`NgRx` stands for Angular Reactive Extensions. `NgRx` is a state management system that is based on the `Redux pattern`. Before we go further into details, let’s try and understand the concept of state in an Angular application.

### State
Theoretically, application state is the entire memory of the application. In simple terms, application state is composed of data received by API calls, user inputs, presentation UI state, application preferences, etc. A simple, concrete example of an application state would be a list of customers maintained in a CRM application.


Let’s try to understand the application state in the context of an Angular application. As you are well aware, an Angular application is typically made up of many components. Each of these components has its own state and has no awareness of the state of the other components. In order to share information between parent-child components, we use @Input and@Output decorators. However, this approach is practical only if your application consists of a few components, as shown below.

![Alt text](images/ngrx1.png?raw=true "Change detection")

When the number of components grows, it becomes a nightmare to pass the information between components solely via @Input and @Output decorators. Let’s take the following figure to elaborate on this.

![Alt text](images/ngrx2.png?raw=true "Change detection")

If you have to pass information from component three to component six, you will have to hop four times and involve three other components. As you can see, it’s a very cumbersome and error-prone way of managing the state. This is where the Redux Pattern comes into play.

#### Redux
Redux is a pattern that’s used to simplify the state management process in JavaScript applications (not just for Angular). Redux is primarily based on three main principles.

* Single source of truth 
* Read-only state 
* State is modified with pure functions

Single source of truth — This means the state of your application is stored in an object tree within a single store. The store is responsible for storing the data and providing the data to components whenever requested. (I’m referring to Angular applications here. But Redux can be applied to any JavaScript application in general.) According to this architecture, data flows between the store and the components, instead of from component to component. The following figure illustrates this concept.

![Alt text](images/ngrx3.png?raw=true "Change detection")

Read-only state — In other words, state is immutable. This doesn’t necessarily mean that state is always constant and cannot be changed. It only implies that you are not allowed to change the state directly. In order to make changes in the state, you have to dispatch `actions` (which we will discuss in detail later) from different parts of your application to the store.

State is modified with pure functions — Dispatching actions will trigger a set of pure functions called `reducers`. Reducers are responsible for modifying the state in different ways based on the action received. A key thing to note here is that a reducer always returns a new state object with the modifications.

#### NgRx
`NgRx` is a group of libraries inspired by the Redux pattern. As the name suggests, NgRx is written specifically for Angular application as a state management solution. We will dive into the fundamental building blocks of NgRx library in the next section. Please note that I will be using NgRx version 8 for all the sample codes.


<br>
<br>

### 7. Redux

<br>
<br>

### 8. **15** main inbuilt functions of RXJS

<br>
<br>

### 9. Protractor 
<br>
<br>

### 10. Dependency injection 
<br>
<br>

### 11. SCSS css
<br>
<br>

### 12. Angular material 
### 13. Routing 
### 14. Authentication and authorization 
### 15. JWT tokens 
### 16. Observable 
### 17. Promises 
### 18. Custom directive and pipes 
### 19. Bindings
### 20.Component data sharing types 
### 21. Auth guard 
### 22. Query Params
### 23. Params 
### 24. Services 
### 25. Modules 
### 26. Modular structure division 
### 27. Lazy Loading
### 28. Hoisting in JavaScript
### 29. Testbed
### 30. Spread Operator in JavaScript
### 31. Debugging
### 32. Pure & Impure Pipe in Angular Custom pipe.
### 33. Classical Inheritance & Prototypal Inheritance
### 34. Structural Directives
### 35. Directives and Components
### 36. Just in Time & Ahead/Arrived in Time
### 37. Closure In Java Script Functions In Javascript
### 38. Scope Chain In Javascript
### 39. Java Classes
### 40. Different Ways To Communicate Between Components In Angular
### 41. Promises Vs Observable
### 42. Change Deduction Mechanism In Angular
### 43. Angular Material
### 44. PrimeNG Library In Angular Material
### 45. How Do You Divide Modules
### 46. Service Worker Module Of Angular
### 47. Attribute Binding Vs Two Way Binding
### 48. Arrow Function And Anonymous Function
### 49. Have you used Forms in Angular ?
### 50. What is Form Control ?
### 51. Difference NG4 & NgF
### 52. Trackby concept
### 53. Differential Loading
