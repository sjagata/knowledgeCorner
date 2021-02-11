
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

[link](https://www.youtube.com/watch?v=f97ICOaekNU&ab_channel=Fireship)

![Alt text](images/ngrx.png?raw=true "Change detection")

> Fundamental Elements of NgRx: `Store`, `Actions`, `Reducers`, `Selectors`, `Effects`

#### The store [Acts like a angular service]
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
Protractor is an end-to-end test framework for Angular and AngularJS applications. Protractor runs tests against your application running in a real browser, using Selenium.

In order to run your first test with protractor you will need to :
1. get update webdriver-manager
2. write the test
3. set the configuration to run the test
4. run it!

The `configuration file` tells Protractor how to set up the `Selenium Server`, `which tests to run`, how to set up the `browsers`, and `which test framework to use`. The configuration file can also include one or more global settings. The config file provides explanations for all of the Protractor configuration options. Default settings include the standalone Selenium Server, the Chrome browser, and the Jasmine test framework.

`Spec file` is the one where we write actual test code. It contains the logic and locators to interact with an application.

```js
//protractor.conf.js
exports.config = {
  seleniumAddress: 'http://127.0.0.1:4444/wd/hub',
  getPageTimeout: 60000,
  allScriptsTimeout: 500000,
  framework: 'custom',
  // path relative to the current config file
  frameworkPath: require.resolve('protractor-cucumber-framework'),
  capabilities: {
    'browserName': 'chrome'
  },

  // Spec patterns are relative to this directory.
  specs: [
    'features/*.feature'
  ],

  baseURL: 'http://localhost:8080/',

  cucumberOpts: {
    require: 'features/step_definitions/stepDefinitions.js',
    tags: false,
    format: 'pretty',
    profile: false,
    'no-source': true
  }
};


//test.spec.js
describe('Protractor Test', function() {  
  var addField = element(by.css('[placeholder="add new todo here"]'));  
  var checkedBox = element(by.model('todo.done'));  
  var addButton = element(by.css('[value="add"]'));  

  it('should navigate to the AngularJS homepage', function() {  
    browser.get('https://angularjs.org/'); //overrides baseURL  
  });  
});
```

#### Cucumber Setup
First, you need to install Cucumber with `npm install -g cucumber`. Make sure it is installed in the same place as Protractor. Next, you’ll have to install the protractor-cucumber-framework with `npm install --save-dev protractor-cucumber-framework`. This iteration is designed with Protractor 3.x in mind. When the installation completes, you can write out a feature. In the project, create a features folder with a test.feature feature file. All of your features will be housed in this folder.

```js
#features/test.feature
Feature: Running Cucumber with Protractor
    As a user of Protractor
    I should be able to use Cucumber
    In order to run my E2E tests

    Scenario: Protractor and Cucumber Test
        Given I go to "https://angularjs.org/"
        When I add "Be Awesome" in the task field
        And I click the add button
        Then I should see my new task in the list
```

Save the file and run cucumber.js to see how Cucumber processes the feature. Below is a snippet:

```js
Feature: Running Cucumber with Protractor
    As a user of Protractor
    I should be able to use Cucumber
    In order to run my E2E tests

    Scenario: Protractor and Cucumber Test
        Given I go to "https://angularjs.org/"
        When I add "Be Awesome" in the task field
        And I click the add button
        Then I should see my new task in the list

1) Scenario: Protractor and Cucumber Test - features/test.feature:6
   Step: Given I go to "https://angularjs.org/" - features/test.feature:7
   Message:
     Undefined. Implement with the following snippet:

       this.Given(/^I go to "([^"]*)"$/, function (arg1, callback) {
         // Write code here that turns the phrase above into concrete actions
         callback(null, 'pending');
       });
1 scenario (1 undefined)
3 steps (3 undefined)
0m00.000s
```

#### Assertions: Chai and Chais-As-Promised
Since you’re using the custom framework option with Protractor you’ll need to add an assertion library like Chai — a popular choice. Chai allows us to write assertions in a simple, readable style — such as the familiar expect syntax in `expect(element.getText()).to.eventually.equal('Name');`.

```js
//features/step_definitions/my_step_definitions.js
var chai = require('chai');
var chaiAsPromised = require('chai-as-promised');

chai.use(chaiAsPromised);
var expect = chai.expect;

module.exports = function() {
  this.Given(/^I go to "([^"]*)"$/, function(site) {
    browser.get(site);
  });

  this.When(/^I add "([^"]*)" in the task field$/, function(task) {
    element(by.model('todoList.todoText')).sendKeys(task);
  });

  this.When(/^I click the add button$/, function() {
    var el = element(by.css('[value="add"]'));
    el.click();
  });

  this.Then(/^I should see my new task in the list$/, function(callback) {
    var todoList = element.all(by.repeater('todo in todoList.todos'));
    expect(todoList.count()).to.eventually.equal(3);
    expect(todoList.get(2).getText()).to.eventually.equal('Do not Be Awesome')
      .and.notify(callback);
  });
};
```


#### What are the locators in Protractor?

Protractor supports all the element location strategies given by Selenium and it also has unique set of locators particularly to identify elements based on AngularJS attributes.

> Selenium locators:

* by.className
* by.css
* by.cssContainingText
  **Advantages**
    * It’s faster than XPath.
    * It’s much easier to learn and implement.
    * You have a high chance of finding your elements.
    * It’s compatible with most browsers to date.
  ```js
  element(by.cssContainingText('.col-sm-8', 'Account Information'))
  ```
* by.id
* by.linkText
* by.name
* by.partialLinkText
* by.tagName
* by.xpath
  XPath stands for XML Path. It’s a query language that helps identify elements from an XML document.
  **Advantages**
  * XPath allows you to navigate up the DOM when looking for elements to test or scrape.
  * It’s compatible with old browsers (or it was at time of publishing—including older versions of Internet Explorer, which some corporations still use).
  * Creating in XPath is more flexible than in CSS Selector.
  * When you don’t know the name of an element, you can use contains to search for possible matches.
  ```js
  element(by.xpath('//div[contains(text(), "Account Information: ")]')
  ```
   | Elements               |      CSS 3      |         XPath                      |
   |------------------------|:---------------:|:-----------------------------------|
   | All Elements           |  *              |      //*                            |
   | All P Elements         |  P              |      //p                            |
   | All Child Elements     |  p>*            |      //p/*                         |
   | Element By ID          |  #foo           |      //*[@id=’foo’]                |
   | Element By Class       |  .foo           |      //*[contains(@class,’foo’)]   |
   | Element With Attribute      |  *[title]           |      //*[@title]   |
   | First Child of All P      |  p>*:first-child           |      //p/*[0]   |
   | All P with an A child      |  Not possible          |      //p[a]  |
   | Next Element     |  p + *          |      //p/following-sibling::*[0]  |
   | Previous Element     |  Not possible          |      //p/preceding-sibling::*[0] |
   
    

> Angular Specific Locators

* by.binding
* by.exactBinding
* by.model
* by.repeater
* by.exactRepeater
* by.options

> Other element locator’s introduced in Protractor:

* by.buttonText
* by.paritalButtonText
* by.cssContainingText
* by.deepCss

<br>
<br>

### 10. Dependency injection 
Angular components are meant to be the user interface and nothing more. They display data and enable user interaction, react on user clicks and inputs. The application logic should be done in services. When you need a service in a component, you usually don’t create an instance yourself using new. You mark the service as injectable and you add it as a parameter to the component’s constructor. The Angular Dependency Injection (DI) will take care of creating an instance and will inject it for you.

It is common not to think too much about this process. When you create a service to fetch data from the server, you need only one instance of it, and it doesn’t really matter to you where it lives. But you sometimes need services to be available only inside a module, or even a component and its children. You might need to inject different instances of the service in different components. That is why a good understanding of how the Angular DI works is an important quality for an Angular developer.

#### @Inject and @Injectable
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

#### Injectors

Injectors are responsible for creating instances of the service classes and injecting them in the components that request them. Services are singletons inside an injector scope, there can be at most only one instance of a service.

Injectors are created by Angular. **A root injector is created in the bootstrap process.** Angular will also create injectors for components, pipes or directives, but they stay empty unless you declare a providers array in their decorators. Each lazy-loaded module also gets its own injector.

Injectors are inherited. When you request a service in a component, Angular will look in the injector of the component, then in the one of its parent, then of its parent’s parent’s… etc, until it either finds it or runs out of ancestors. If it hasn’t found it in the element injectors, Angular starts looking in the modules injectors, until it finds a provider (or runs out of injectors).

#### Providers
Injectors create instances and inject them but you need to tell them how to create these instances. When you inject a service in a component, you give a DI Token to the closest injector. By default the token is the service class, TestService in the example below. The injector has a map token-provider, the token is the key. The provider of a service is usually the class itself:

```js
import { Component, OnInit } from '@angular/core';
import { TestService } from 'src/app/services/test.service';

@Component({
  selector: 'app-test',
  templateUrl: './test.component.html',
  styleUrls: ['./test.component.scss'],
  providers: [{ provide: TestService, useClass: TestService }]
})
export class TestComponent implements OnInit {
  text: string;

  constructor(
    private testService: TestService,
  ) { }

  ngOnInit() {
    this.text = this.testService.getTest();
  }
}
```

```js
import { Injectable } from '@angular/core';

@Injectable()
export class TestService {
  getTest(): string {
    return 'test';
  }
}
```

In this example the service is provided only in the TestComponent and we tell Angular to use the class TestService to create an instance when injecting TestService. This is such a common behaviour that Angular gives you a shortcut for it:

```js
providers: [TestService]
```

That also means that we can tell the injector to use some other class when injecting TestService. In the following example, we tell the injector to return an instance of the HelloWorldService when being requested the TestService.

```js
import { Injectable } from '@angular/core';

@Injectable()
export class HelloWorldService {
  getTest(): string {
    return 'Hello World!';
  }
}
```

```js
import { Component, OnInit } from '@angular/core';
import { TestService } from 'src/app/services/test.service';
import { HelloWorldService } from 'src/app/services/hello-world.service';

@Component({
  selector: 'app-test',
  templateUrl: './test.component.html',
  styleUrls: ['./test.component.scss'],
  providers: [{ provide: TestService, useClass: HelloWorldService }]
})
export class TestComponent implements OnInit {
  text: string;

  constructor(
    private testService: TestService,
  ) { }

  ngOnInit() {
    this.text = this.testService.getTest();
  }
}
```

#### Root Injector

You might not be providing services in your components that regularly. By default when you create a service with the Angular cli, the service is provided in the root injector.

```js
import { Component, OnInit } from '@angular/core';
import { TestService } from 'src/app/services/test.service';
import { HelloWorldService } from 'src/app/services/hello-world.service';

@Component({
  selector: 'app-test',
  templateUrl: './test.component.html',
  styleUrls: ['./test.component.scss'],
})
export class TestComponent implements OnInit {
  text: string;

  constructor(
    private testService: TestService,
  ) { }

  ngOnInit() {
    this.text = this.testService.getTest();
  }
}
```

```js
import { Injectable } from '@angular/core';

@Injectable({ providedIn: 'root' })
export class TestService {
  getTest(): string {
    return 'test';
  }
}
```
In this case, we don’t need to provide the service in the component’s injector. An instance of the service will be created in the root injector and injected in our component. This instance will be available everywhere in the application.


<br>
<br>


### 11. Difference between an Annotation and a Decorator in Angular
Although Annotations and Decorators both share the same @ symbol in Angular, they both are different language features.

**Annotations**: This are hard-coded language feature. Annotations are only metadata set on the class that is used to reflect the metadata library. When user annotates a class, the compiler creates an attribute on that class called annotations, stores an annotation array in it, then tries to instantiate an object with the same name as the annotation, passing the metadata into the constructor. Annotations are not predefined in AngularJs so we can name them on our own.


```js
@Component({selector: "my-app", template: 'Hello world!' })
class AppComponent
```
```html
<my-app>Working</my-app> // Hello world!
```


**Decorators**: A decorator is a function that adds metadata to a class, its members, or its method arguments. A decorator is just a function that gives you access to the target that needs to be decorated. There are four type of decorators all of them arem mentioned below:


Types of Decorators:

* Class decorators like @Component, @NgModule
* Property decorators like @Input and @Output
* Method decorators like @HostListener
* Parameter decorators like @Injectable

Features of Decorators:

* Decorators are predefined in AngularJs.
* Decorators are used by TypeScript compiler.
* Decorators are used to attach metadata to a class,objects and method.

<br>
<br>

### 11. SCSS css
<br>
<br>

### 12. Angular material 

<br>
<br>

### 13. Routing 
Routing is a mechanism which enables user to navigate between views/components. Angular 2 simplifies the routing and provide flexibility to configure and define at module level (Lazy loading).

The angular application has single instance of the Router service and whenever URL changes, corresponding Route is matched from the routing configuration array. On successful match, it applies redirects and the router builds a tree of ActivatedRoute objects and contains the current state of the router. Before redirection, the router will check whether new state is permitted by running guards (CanActivate). Route Guards is simply an interface method that router runs to check the route authorization. After guard runs, it will resolve the route data and activate the router state by instantiation the required components into .

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

### 14. Authentication and Authorization

#### Authentication

`Authentication` is the act of validating that users are whom they claim to be. This is the first step in any security process. 

Giving someone permission to download a particular file on a server or providing individual users with administrative access to an application are good examples of authentication.

Complete an authentication process through:

* `Passwords`. Usernames and passwords are the most common authentication factors. If a user enters the correct data, the system assumes the identity is valid and grants access.
* `One-time pins`. Grant access for only one session or transaction.
* `Authentication apps`. Generate security codes via an outside party that grants access.
* `Biometrics`. A user presents a fingerprint or eye scan to gain access to the system. 

In some instances, systems require the successful verification of more than one factor before granting access. This multi-factor authentication (MFA) requirement is often deployed to increase security beyond what passwords alone can provide.

#### Authorization

Authorization in a system security is the process of giving the user permission to access a specific resource or function. This term is often used interchangeably with access control or client privilege.

In secure environments, authorization must always follow authentication. Users should first prove that their identities are genuine before an organization’s administrators grant them access to the requested resources.

![Alt text](images/auth.png?raw=true "Authorization")

![Alt text](images/auth1.png?raw=true "Authorization")

<br>
<br>

### 15. JWT tokens 

The general idea standing behind JWT is to securely transmit information between parties. In our case, it is the user’s identity along with his rights, transmitted between the client (browser) and the server. When the user logs in, sending login query to the server, he receives back a JWT (aka access token) signed by the server with a `private key`. This private key should be known only to the server as it allows the server later to verify that the token is legitimate. When JWT is transmitted between the browser and the server, it is encoded with Base64 algorithm, that makes it look like a string of random characters (nothing could be further from the truth!). If you take a JWT and decode it with Base64 you will find a JSON object. Below you can find a decoded content of a JWT from our example application. On jwt.io you can play with JWT online.



All Auth0-issued JWTs have JSON Web Signatures (JWSs), meaning they are signed rather than encrypted. A JWS represents content secured with digital signatures or Message Authentication Codes (MACs) using JSON-based data structures.

A well-formed JWT consists of three concatenated Base64url-encoded strings, separated by dots (.):

**JOSE Header**: The `header` defines the type of the token and the used algorithm. 

JSON object containing the parameters describing the cryptographic operations and parameters employed. The JOSE (JSON Object Signing and Encryption) Header is comprised of a set of Header Parameters that typically consist of a name/value pair: the hashing algorithm being used (e.g., HMAC SHA256 or RSA) and the type of the JWT.

```js
  {
      "alg": "HS256",
      "typ": "JWT"
    }
```

**JWS payload (set of claims)**: The `payload` is the place where we put the data we want to securely transmit. In this case, we have a username, role, issuing timestamp (iat) and expiration timestamp (exp).

The payload contains statements about the entity (typically, the user) and additional entity attributes, which are called claims. In this example, our entity is a user.

```js
{
      "sub": "1234567890",
      "name": "John Doe",
      "admin": true
    }
```

**JWS signature**: The last block (HMACSHA256 function) is a signature generated with HMAC and SHA-256 algorithms. The signature guarantees not only that the token was created by a known party, but also the token’s integrity.

For example, if you are creating a signature for a token using the HMAC SHA256 algorithm, you would do the following:

```js
HMACSHA256(
      base64UrlEncode(header) + "." +
      base64UrlEncode(payload),
      secret)
```



<br>
<br>

### 16. Promises Vs Observable
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

### 18. Custom directive and pipes 
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

<br>
<br>

### 20. Component data sharing types 
### 21. Auth guard 

<br>
<br>

### 22. Query Params & Params 
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

### 24. Services 

<br>
<br>

### 25. Modules 
**@NgModule** is a decorator function. A decorator function allows users to mark something as Angular 2 thing (could be a module or component or something else) and it enables you to provide additional data that determines how this Angular 2 thing will be processed, instantiated and used at the runtime. So, whenever user writes @NgModule, it tells the Angular 2 module, what’s going to be included and used in and using this module.


<br>
<br>

### 26. Modular structure division 

<br>
<br>

### 27. Lazy Loading
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

### 28. Hoisting in JavaScript
Hoisting is JavaScript's default behavior of moving declarations to the top.

In JavaScript, a variable can be declared after it has been used.

In other words; a variable can be used before it has been declared.

<br>
<br>

### 29. Testbed
Configures and initializes environment for unit testing and provides methods for creating components and services in unit tests.

```js
import {TestBed, ComponentFixture} from '@angular/core/testing';
import {LoginComponent} from './login.component';
import {AuthService} from "./auth.service";

describe('Component: Login', () => {

  let component: LoginComponent;
  let fixture: ComponentFixture<LoginComponent>; (1)
  let authService: AuthService;

  beforeEach(() => {
    TestBed.configureTestingModule({
      declarations: [LoginComponent],
      providers: [AuthService]
    });

    // create component and test fixture
    fixture = TestBed.createComponent(LoginComponent); (2)

    // get test component from the fixture
    component = fixture.componentInstance; (3)

    // UserService provided to the TestBed
    authService = TestBed.get(AuthService); (4)

  });
});

it('needsLogin returns true when the user has not been authenticated', () => {
    spyOn(authService, 'isAuthenticated').and.returnValue(false);
    expect(component.needsLogin()).toBeTruthy();
    expect(authService.isAuthenticated).toHaveBeenCalled();
});

it('needsLogin returns false when the user has been authenticated', () => {
    spyOn(authService, 'isAuthenticated').and.returnValue(true);
    expect(component.needsLogin()).toBeFalsy();
    expect(authService.isAuthenticated).toHaveBeenCalled();
});
```

<br>
<br>

### 30. Spread Operator in JavaScript
check JS MD file
<br>
<br>

### 31. Debugging
The debugger keyword stops the execution of JavaScript, and calls (if available) the debugging function.

This has the same function as setting a breakpoint in the debugger.

If no debugging is available, the debugger statement has no effect.

With the debugger turned on, this code will stop executing before it executes the third line.

```js
var x = 15 * 5;
debugger;
document.getElementById("demo").innerHTML = x;
```

<br>
<br>

### 32. Pure & Impure Pipe in Angular Custom pipe.

#### What is Pipes? Why use Pipes?
Pipes are feature built into angular to which bascially allows you to transform output in your template
Something like filters in angular 1


#### What is a pure and impure pipe?
Filter pipe wont trigger while updating Arrays or Objects 
We can enforce the pipe to be updated whenever the data changes by adding a second property to the pipe **(pure: false)**
```js
@Pipe({
  name: 'filter',
  pure: false
})
```
This is a performance hit

#### What is Async Pipe?
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


#### How to create and use a custom Pipes?
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
#### Pipes Example
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

### 33. Classical Inheritance & Prototypal Inheritance

JavaScript’s class inheritance uses the prototype chain to wire the child `Constructor.prototype` to the parent `Constructor.prototype` for delegation. Usually, the `super()` constructor is also called. Those steps form single-ancestor parent/child hierarchies and create the tightest coupling available in OO design.

Class Inheritance: A class is like a blueprint — a description of the object to be created. Classes inherit from classes and create subclass relationships: hierarchical class taxonomies.

Prototypal Inheritance: A prototype is a working object instance. Objects inherit directly from other objects.

```js
function Person() {
}

var will = new Person();
```

```js
var human = {
    species: "human",
    saySpecies: function() {
        console.log(this.species);
    },
    sayName: function() {
        console.log(this.name);
    }
};

var musician = Object.create(human);
musician.playInstrument = function() {
    console.log("playss..." + this.instrument);
};

var will = Object.create(musician);
will.name = "Will";
will.instrument = "Drums";

// {name: "Will", instrument: "Drums"}
// instrument: "Drums"
// name: "Will"
// __proto__:
// playInstrument: ƒ ()
// __proto__:
// sayName: ƒ ()
// saySpecies: ƒ ()
// species: "human"
// __proto__: Object


//prototypal inheritance
var human = {
 species: "human",
 create: function(values) {
  var instance = Object.create(this);
  Object.keys(values).forEach(function(key) {
    instance[key] = values[key];
  });
  return instance;
 },
 saySpecies: function() {
  console.log(this.species);
 },
 sayName: function() {
  console.log(this.name);
 }
};

var musician = human.create({
  species: "musician",
  playInstrument: function() {
    console.log("plays " + this.instrument);
  }
});

var will = musician.create({
  name: "Will",
  instrument: "drums"
});

will.playInstrument(); // plays drums
will.sayName(); //will



```

<br>
<br>

### 34. Structural Directives
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

<br>
<br>

### 35. Directives and Components
In Angular, a Component is a special kind of directive that uses a simpler configuration which is suitable for a component-based application structure.

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

### 36. Just in Time & Ahead/Arrived in Time

> JIT - Compile TypeScript just in time for executing it.

* Compiled in the browser.
* Each file compiled separately.
* No need to build after changing your code and before reloading the browser page.
* Suitable for local development.

> AOT - Compile TypeScript during build phase.

* Compiled by the machine itself, via the command line (Faster).
* All code compiled together, inlining HTML/CSS in the scripts.
* No need to deploy the compiler (Half of Angular size).
* More secure, original source not disclosed.
* Suitable for production builds.

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


### 40. Different Ways To Communicate Between Components In Angular
1. Binding (@Input & @Output)

2. Reference (@ViewChild & @ContentChild)
`@ContentChild` and `@ContentChildren` queries will return directives existing inside the element of your view, whereas `@ViewChild` and `@ViewChildren` only look at elements that are on your view template directly.

`ViewChild` element can be read after the view is initialized (ngAfterViewInit).

`ContentChild` is used to query the reference of the DOM within ng-content. Content Child are set before the ngAfterContentInit lifecycle hook.

```js
<input type="text" #username required ... />

@ViewChild('username') username: HTMLInputElement;
```

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

3. Provider (Service)

4. Template Outlet

### 43. PrimeNG Library In Angular Material
### 44. How Do You Divide Modules
### 45. Service Worker Module Of Angular

<br>
<br>

### 46. Attribute Binding Vs Two Way Binding

It is recommended that you set an element property with a property binding whenever possible. However, sometimes you don't have an element property to bind. In those situations, you can use attribute binding.

```js
<p [attr.attribute-you-are-targeting]="expression"></p>
```

Two-way binding gives components in your application a way to share data. Use two-way binding to listen for events and update values simultaneously between parent and child components.

Angular's two-way binding syntax is a combination of square brackets and parentheses, `[()]`. The `[()]` syntax combines the brackets of property binding, `[]`, with the parentheses of event binding, `()`, as follows.

```js
<app-sizer [(size)]="fontSizePx"></app-sizer>
```

<br>
<br>


### 48. Have you used Forms in Angular ?

<br>
<br>

### 49. What is Form Control ?
Two Approaches:

1. Template-Driven : Angular infers the Form Object from the DOM 
2. Reactive [model driven] : Form is created programamatically and synchronized with the DOM 

<br>
<br>

### 50. Difference NG4 & NgF
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
<br>
<br>

### 51. Trackby concept
An optional function passed into the NgForOf directive that defines how to track changes for items in an iterable. The function takes the iteration index and item ID. When supplied, Angular tracks changes by the return value of the function.

On each `ngDoCheck` triggered for the ngForOf directive Angular checks what objects have changed. It uses differs for this process and each differ uses trackBy function to compare the current object with the new one. The default trackBy function tracks items by identity:

```js
const trackByIdentity = (index: number, item: any) => item;
```


<br>
<br>

### 52. Differential Loading

Differential loading is a process by which the browser chooses between modern or legacy JavaScript based on its own capabilities. We now take advantage of this by default by performing a modern build (es2015) and a legacy build (es5) of your application. When users load your application, they’ll automatically get the bundle they need.

If you use ng update, we update your tsconfig.jsonfor you to take advantage of this. Our CLI looks at the target JS level in your tsconfig.json to determine whether or not to take advantage of Differential Loading.

```js
{
  "compilerOptions": {
  …
  "module": "esnext",
  "moduleResolution": "node",
  …
  "target": "es2015",
  …
},
```

<br>
<br>
