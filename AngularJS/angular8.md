
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

### 6. Ngrx basics & Redux
`NgRx` stands for Angular Reactive Extensions. `NgRx` is a state management system that is based on the `Redux pattern`. Before we go further into details, let’s try and understand the concept of state in an Angular application.

#### State
Theoretically, application state is the entire memory of the application. In simple terms, application state is composed of data received by API calls, user inputs, presentation UI state, application preferences, etc. A simple, concrete example of an application state would be a list of customers maintained in a CRM application.


Let’s try to understand the application state in the context of an Angular application. As you are well aware, an Angular application is typically made up of many components. Each of these components has its own state and has no awareness of the state of the other components. In order to share information between parent-child components, we use `@Input` and `@Output` decorators. However, this approach is practical only if your application consists of a few components, as shown below.

![Alt text](images/ngrx1.png?raw=true "Change detection")

When the number of components grows, it becomes a nightmare to pass the information between components solely via `@Input` and `@Output` decorators. Let’s take the following figure to elaborate on this.

![Alt text](images/ngrx2.png?raw=true "Change detection")

If you have to pass information from component three to component six, you will have to hop four times and involve three other components. As you can see, it’s a very cumbersome and error-prone way of managing the state. This is where the `Redux Pattern` comes into play.

<br>
<br>

### 7. Redux
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

> Fundamental Elements of NgRx: `Store`, `Actions`, `Reducers`, `Selectors`, `Effects`

#### The store
The store is the key element in the entire state management process. It holds the state and facilitates the interaction between the components and the state. You can obtain a reference to the store via Angular dependency injection, as shown below.

```js
constructor(private store: Store<AppState>) {}
```
This store reference can be subsequently used for two primary operations:
* To dispatch actions to the store via the `store.dispatch(…)` method, which will in turn trigger reducers and effects
* To retrieve the application state via selectors


#### Actions
An action is an instruction that you dispatch to the store, optionally with some metadata (payload). Based on the action type, the store decides which operations to execute. In code, an action is represented by a plain old JavaScript object with two main attributes, namely type and payload. payload is an optional attribute that will be used by reducers to modify the state. 

#### Reducers
Reducers are responsible for modifying the state and returning a new state object with the modifications. Reducers take in two parameters, the current state and the action. Based on the received action type, reducers will perform certain modifications to the current state and produce a new state.


#### Effects
Effects allow you to perform side effects when an action is dispatched to the store. Let’s try to understand this through an example. When a user successfully logs in to an application, an action with type Login Action will be dispatched to the store with the user information in the payload. A reducer function will listen to this action and modify the state with the user information. In addition, as a side effect, you also want to save user information in the browser's local storage. An effect can be used to carry out this additional task (side effect).


#### Selectors


<br>
<br>

### 8. **15** main inbuilt functions of RXJS

#### 1. Using map() to transform data
Using `map()` on an Observable is identical to using it on an array. It:

1. Accepts a callback as an argument;
2. Executes it on every element of the array you called it on; and
3. Returns a new array with each element of the original array replaced with the result of calling the callback on it.

The only differences when using map() on Observables are that:

1. Instead of returning a new array, it returns a new Observable; and
2. It executes every time the Observable emits a new item, instead of immediately and all at once.

We can use map() to transform our stream of user data into just a list of their website names:

```js
source.
  map((user) => user.website)
  
// Here, we’ve used map to “replace” every user object in the incoming stream with each user’s website.

Hello, Rx.js!
Emails
hildegard.org
anastasia.net
ramiro.info
kale.biz
demarco.info
ola.org
elvis.io
jacynthe.com
conrad.com
ambrose.net
```

#### 2. Filtering results
Like `map()`, `filter()` is much the same on Observables as on arrays. To find every user with either a .net or a .org website address, we’d write:

```js
source.
  map((user) => user.website).
  filter((website) => (website.endsWith('net') || website.endsWith('org'));
})

// Hello, Rx.js!
// Emails
// hildegard.org
// anastasia.net
// ola.org
// ambrose.net
```

#### 3. Collecting results with reduce()
`reduce()` allows us to use all of our individual values and turn them into a single result.

`reduce()` tends to be the most confusing of the basic list operations, because, unlike `filter()` or `map()`, it behaves differently from use to use.

In general, `reduce()` takes a collection of values, and turns it into a single data point. In our case, we’ll feed it a stream of website name, and use `reduce()` to convert that stream into an object that counts how many websites we’ve found, and the sum of the lengths of their names.

```js
source.
  map((user) => user.website).
  filter((website) => (website.endsWith('net') || website.endsWith('org'))).
  reduce((data, website) => {
    return {
      count       : data.count += 1,
      name_length : data.name_length += website.length
    }
  }, { count : 0, name_length : 0 })
  
// Hello, Rx.js!
// Average Length:	11
```

Keep in mind that `reduce()` only returns a result when the source Observable completes. If you want to know the state of the accumulator every time the stream receives a new item, use `scan()` instead.

#### 4. Limiting results with take()
`take()` and `takeWhile()` round out the basic functions on simple streams.

`take(n)` reads n values from a stream, and then unsubscribes.

We can use `scan()` to emit the our object every time we receive a website, and only `take()` the first two values.

```js
source.
  map((user) => user.website).
  filter((website) => (website.endsWith('net') || website.endsWith('org'))).
  scan((data, website) => {
      return {
        count       : data.count += 1,
        name_length : data.name_length += website.length
      }
    }, { count : 0, name_length : 0 }).
  take(2);
  
// Hello, Rx.js!
// Average Length: 13
```

RxJS also offers `takeWhile()`, which allows you to take values until some boolean test holds true. We can write the above stream with `takeWhile()` like this:

```js
source.
  map((user) => user.website).
  filter((website) => (website.endsWith('net') || website.endsWith('org'))).
  scan((data, website) => {
    return {
      count       : data.count += 1,
      name_length : data.name_length += website.length
    }
  }, { count : 0, name_length : 0 }).
  takeWhile((data) =>  data.count < 3)
```

#### 5. Squashing streams with flatMap()
We made calls to `fromPromise()` and `flatMap()` when we defined our source stream:

```js

'use strict';

// Helper Method
const ENDPOINT = 'users',
  ROOT = 'https://jsonplaceholder.typicode.com';

const makeRequest = function makeRequest(path, item) {
  return new Promise(function(resolve, reject) {
    // Assumes jQuery
    path ? (path = '/' + path) : path = '/';
    item ? (item = '/' + item) : item = '/';
    const url = ROOT + path + item;

    $.getJSON(url)
      .done(function(data) {
      console.log(data);
        resolve(data);
      })
      .fail(function() {
        reject();
      })
  });
};

// BOILERPLATE
const source   =
    // Take a Promise and convert it to an Observable
    Rx.Observable.fromPromise(makeRequest(ENDPOINT))
      // Flatten Promise
      .flatMap(Rx.Observable.from);
      
const PROMISE = makeRequest(ENDPOINT),
  source = Rx.Observable.fromPromise(PROMISE)
             .flatMap(Rx.Observable.from);

source.
  map(user => user.website).
  filter(website => website.endsWith('net') || website.endsWith('org')).
  scan((data, website) => {
    return {
      data: website,
      count: data.count += 1,
      name_length: data.name_length += website.length
    }
  }, {
    data: '',
    count: 0,
    name_length: 0
  }).
  take(1).
    /* With takeWhile:
    takeWhile((data) => data.count < 3).
    */
  subscribe(data => {
  console.log(data);
    const average_length = data.name_length / data.count;
    $('#average-length').html(average_length);
  });


```


#### 6. Using flatMap()

This process is called flattening, which flatMap() takes care of. It has a number of overloads, but we’ll only use the simplest and the most common of them.

When using `flatMap()`, we:

1. Call `flatMap()` on an Observable that emits the single-value resolution or rejection of a Promise; and
Pass it a function to create a new Observable with.

2. In our case, we pass `Rx.Observable.from()`, which creates a sequence from the values of an array:

In our case, we pass `Rx.Observable.from()`, which creates a sequence from the values of an array:

```js
Rx.Observable.from([1, 2, 3]).
  subscribe(
      onNext (value) => console.log(`Next: ${value}`))

// Prints: 
//  Next: 1
//  Next: 2
//  Next: 3
```

That covers the code in our little prelude:

```js
const source =
  // Create an Observable emitting the VALUE or REJECTION of a Promise...
  Rx.Observable.fromPromise(makeRequest(ENDPOINT))
    // ...And turn it into a new Observable that emits every item of the
    //  array the Promise resolves to.
    .flatMap(Rx.Observable.from)

```


#### 7. Combining streams with concat() and merge()
Concatenation and merging are two of the most common ways to combine streams.

Concatenation creates a new stream by emitting the values of a first stream until it completes, and then emitting the values of a second stream.

Merging creates a new stream from many streams by emitting values from whichever stream is active

Think of talking to two people at once on Facebook Messenger. `concat()` is the scenario where you get messages from both, but finish your conversation with one person before responding to the other. `merge()` is like creating a group chat and receiving both streams of messages simultaneously.

```js
source1.
  concat(source2).
  subscribe(
    onNext(value) => console.log(`Next: ${value}`))
    // Prints 'Source 1' values first, THEN 'Source 2'

source1.
  merge(source2).
  subscribe(
    onNext(value) => console.log(`Next: ${value}`))
    // INTERLEAVES 'Source 1' and 'Source 2' values
    
    
    
'use strict';

const source1 =
  Rx.Observable.interval(100)
    .map(val => `Source 1: ${val}`)
    .take(5);

const source2 =
  Rx.Observable.interval(100)
    .map(val => `Source 2: ${val * 10}`)
    .take(5);

const concat_table = $('#concat-table-body'),
      merge_table  = $('#merge-table-body');

source1
  .concat(source2)
  .subscribe(value => {
    const row = document.createElement('tr');
    row.innerHTML = value;

    // Source 1 values populate BEFORE Source 2 
    concat_table.append(row);
  });

source1
  .merge(source2)
  .subscribe(value => {
    const row = document.createElement('tr');
    row.innerHTML = value;

    // Source 1 values INTERLEAVE with Source 2
    merge_table.append(row);
  });
  
Hello, Rx.js!
Concatenated Stream
Source 1: 0
Source 1: 1
Source 1: 2
Source 1: 3
Source 1: 4
Source 2: 0
Source 2: 10
Source 2: 20
Source 2: 30
Source 2: 40
Merged Stream
Source 1: 0
Source 2: 0
Source 1: 1
Source 2: 10
Source 1: 2
Source 2: 20
Source 1: 3
Source 2: 30
Source 1: 4
Source 2: 40
```

#### 8. Using switch()

Often, we want to listen to an Observable emitting Observables, but only pay attention to the latest emission from the source.

To extend the Facebook Messenger analogy further, `switch()` is the case where you . . . Well, switch who you respond to, based on who’s currently sending messages.

For this, RxJS provides `switch`.

User interfaces furnish several good use cases for `switch()`. If our app fires off a request every time a user selects what they want to search for, we can assume they only want to see results from the latest selection. So, we use `switch()` to listen to only the result from the latest selection.

While we’re at it, we should make sure not to waste bandwitdh by only hitting the server for the last selection a user makes every second. The function we use for this is called `debounce()`

If you want to go in the other direction, and only honor the first selection, you’d use `throttle()`. It has the same API, but opposite behavior.

```js
'use strict';

// Helper Method
const ENDPOINT = 'users',
    ROOT     = 'https://jsonplaceholder.typicode.com';

const makeRequest = function makeRequest(path, item) {
return new Promise(function(resolve, reject) {
  // Assumes jQuery
  path ? (path = '/' + path) : path = '/';
  item ? (item = '/' + item) : item = '/';
  const url = ROOT + path + item;
  
  $.getJSON(url)
    .done(function (data) {
      resolve(data);
    })
    .fail(function () {
      reject();
    })
});
};
  
// Code goes here
const select    = document.getElementById('js-select-endpoint'),
    id_select = document.getElementById('js-select-id'),
    response_box = document.getElementById('js-response-box');

// STREAM of button clicks on ENDPOINT selection
const endpoint_stream = 
  Rx.Observable.fromEvent(select, 'click').
    map(event  => event.target).
    map(target => (target.options[target.selectedIndex].text.toLowerCase()));


const id_stream = 
  Rx.Observable.fromEvent(id_select, 'click').
    map(event  => event.target).
    map(target => (target.options[target.selectedIndex].text.toLowerCase()));
    
const request_stream  = 
  // To wait until BOTH fields get updated, use zip:
  //   endpoint_stream.zip(id_stream) 
  endpoint_stream.combineLatest(id_stream).
    // Emits ARRAY: First element is from endpoint_stream, second is from id_stream
    map(data => makeRequest(data[0], data[1]))
    // Only hit server for DIFFERENT requests
    .distinctUntilChanged()
    // Take only the last selections made every second
    .debounce(1000)
    // Listen to the most RECENT selection
    .switch()
    .subscribe(response => {
      response_box.innerHTML = JSON.stringify(response, null, 2);
    })
```

[codePen](https://codepen.io/SitePoint/pen/akEXwZ)


#### 9. Coordinating streams

What if we want to allow the user to search for a post or user with a specific ID?

To demonstrate, we’ll create another dropdown, and allow users to choose the ID of the item they want to retrieve.

There are two scenarios. We kick off a request when the user:

1. Changes either selection; or
2. Changes both selections.

##### Respond to changes to either stream with combineLatest()
In the former case, we need to create a stream that fires a network request with:

1. Whichever endpoint the user most recently selected; and
2. Whichever ID the user most recently selected.

. . . And do so whenever the user updates either selection.

This is what combineLatest() is for:
```js
// User's selection for either POSTS or USERS data
const endpoint_stream = 
  Rx.Observable.fromEvent(select_endpoint, 'click').
    map(event  => event.target).
    map(target => (target.options[target.selectedIndex].text.toLowerCase()));

// Which item ID the user wants to retrieve
const id_stream = 
  Rx.Observable.fromEvent(select_id, 'click').
    map(event  => event.target).
    map(target => (target.options[target.selectedIndex].text));

// Emits a pair of the most recent selections from BOTH streams 
//   when EITHER emits a value
const complete_endpoint_stream = 
  endpoint_stream.combineLatest(id_stream);
```

#### 10. takeUntil
Finally, `takeUntil()` allows us to listen to a first stream until a second one starts emitting values.

```js
source1.
  takeUntil(source2);
```

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
