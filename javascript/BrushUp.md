### 2 week sprint on AGILE / Asynchronous & synchronous Development // Reactive Form & Templets etc..

### Protractor (Locators, Elements, Structure)

### CSS Selectors


### Scope chain
> When a variable is used in JavaScript, the JavaScript engine will try to find the variable’s value in the current scope. If it could not find the variable, it will look into the outer scope and will continue to do so until it finds the variable or reaches global scope.

> If it’s still could not find the variable, it will either implicitly declare the variable in the global scope (if not in strict mode) or return an error.

For example:

```js
let foo = 'foo';
function bar() {
  let baz = 'baz';
  // Prints 'baz'
  console.log(baz);
  // Prints 'foo'
  console.log(foo);
  number = 42;
  console.log(number);  // Prints 42
}
bar();
```

> Where a variable is available in your code. 
> `let' - can be used instead of var. let allows javascript engine to use what's called block scoping.

```js
function a() {
    
    function b() {
        console.log(myVar);
    }
    
	b();
}

var myVar = 1;
a();

if( a > b ){
 let c = true;
}
```

![Alt text](img/scope.png?raw=true "Title")

#### How Does Scope and Scope Chain Work?
> Up until now, we have discussed what scope is and types of scope. Now let’s understand how JavaScript engine determines the scope of variables and perform variable lookups under the hood.
> In order to understand how JavaScript engine performs variable lookups, we have to understand the concept of lexical environment in JavaScript.

##### What is a Lexical Environment?
> A lexical environment is a structure that holds identifier-variable mapping. (here identifier refers to the name of variables/functions, and the variable is the reference to actual object [including function object and array object] or primitive value).
> Simply put, a lexical environment is a place where variables and references to the objects are stored.
> Note — Don’t confuse lexical scope with the lexical environment, lexical scope is a scope that is determined at compile time and a lexical environment is a place where variables are stored during the program execution.

```js
Conceptually a lexical environment looks like this:
lexicalEnvironment = {
  a: 25,
  obj: <ref. to the object>
}
```
> A new lexical environment is created for each lexical scope but only when the code in that scope is executed. The lexical environment also has a reference to its outer lexical environment ( i.e outer scope). For example:
```js
lexicalEnvironment = {
  a: 25,
  obj: <ref. to the object>
  outer: <outer lexical environemt>
}
```
### Event loop

> Your JavaScript code runs single threaded. There is just one thing happening at a time.

> This is a limitation that’s actually very helpful, as it simplifies a lot how you program without worrying about concurrency issues.

> You just need to pay attention to how you write your code and avoid anything that could block the thread, like synchronous network calls or infinite loops.

> In general, in most browsers there is an event loop for every browser tab, to make every process isolated and avoid a web page with infinite loops or heavy processing to block your entire browser.

> The environment manages multiple concurrent event loops, to handle API calls for example. Web Workers run in their own event loop as well.

> You mainly need to be concerned that your code will run on a single event loop, and write code with this thing in mind to avoid blocking it.

##### Blocking the event loop

> Any JavaScript code that takes too long to return back control to the event loop will block the execution of any JavaScript code in the page, even block the UI thread, and the user cannot click around, scroll the page, and so on.

> Almost all the I/O primitives in JavaScript are non-blocking. Network requests, Node.js filesystem operations, and so on. Being blocking is the exception, and this is why JavaScript is based so much on callbacks, and more recently on promises and async/await.

##### The call stack

> The call stack is a LIFO queue (Last In, First Out).

> The event loop continuously checks the call stack to see if there’s any function that needs to run.

### Execution context 
1. Global Object
2. 'this'
3. Outer Enviornment
4. your code

> ### Hoisting:
> Setup memory space for variabes and functions 

> ### Synchronous Execution:
> Single threaded: one command at a time.

> Javascript is Single threaded execution

> ### Invocation:
> Running a function 

#### Functions, Context and Variable Enviornments 
```js
function b() {
	var myVar; // myVar = undefined
    console.log(myVar);
}

function a() {
	var myVar = 2; // myVar = 2
    console.log(myVar);
	b();
}

// 1. Global execution context (created and code is executed) // myVar = 1
var myVar = 1; // global execution context
console.log(myVar);

// 2. Execution context (created and execute)
a(); // execution context

console.log(myVar); // after completing a() myVar is global execution
```
> Every execution context has its own variable enviornment 

### Prototypal inheritance 
### Closures
### This keyword variant 
### Functions and objects 
### Call bind apply 

### Function Constructors 
### The new keyword
### arguments 
### Spread
### Arrow function behavior changes 
 
