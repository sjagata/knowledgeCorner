### 2 week sprint on AGILE / Asynchronous & synchronous Development // Reactive Form & Templets etc..

### Protractor (Locators, Elements, Structure)

### CSS Selectors


### 1. Scope chain
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


### 2. Event loop


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



### 3. Execution context 


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


### 4. Prototypal inheritance 

![Alt text](img/proto.png?raw=true "Title")
	
> Inheritance : One Object gets access to the properties and methods of another object.

```js
var person = {
    firstname: 'Default',
    lastname: 'Default',
    getFullName: function() {
	return this.firstname + ' ' + this.lastname;  
    }
}

var john = {
    firstname: 'John',
    lastname: 'Doe'
}

// don't do this EVER! for demo purposes only!!!
john.__proto__ = person;
console.log(john.getFullName()); // John Doe
console.log(john.firstname); // John

var jane = {
    firstname: 'Jane'   
}

jane.__proto__ = person;
console.log(jane.getFullName()); // Jane Default

person.getFormalFullName = function() {
    return this.lastname + ', ' + this.firstname;   
}

console.log(john.getFormalFullName()); // Doe, John
console.log(jane.getFormalFullName()); // Default, Jane
```


### 5. Closures

> Whenever you use function inside another function, a closure is used.

> Whenever you use eval() inside a function, a closure is used. The text you eval can reference local variables of the function, and within eval you can even create new local variables by using eval('var foo = …')

> When you use new Function(…) (the Function constructor) inside a function, it does not create a closure. (The new function cannot reference the local variables of the outer function.)

> A closure in JavaScript is like keeping a copy of all the local variables, just as they were when a function exited.

> It is probably best to think that a closure is always created just an entry to a function, and the local variables are added to that closure.

> A new set of local variables is kept every time a function with a closure is called (given that the function contains a function declaration inside it, and a reference to that inside function is either returned or an external reference is kept for it in some way).

> Two functions might look like they have the same source text, but have completely different behaviour because of their 'hidden' closure. I don't think JavaScript code can actually find out if a function reference has a closure or not.

> If you are trying to do any dynamic source code modifications (for example: myFunction = Function(myFunction.toString().replace(/Hello/,'Hola'));), it won't work if myFunction is a closure (of course, you would never even think of doing source code string substitution at runtime, but...).

> It is possible to get function declarations within function declarations within functions — and you can get closures at more than one level.

> I think normally a closure is the term for both the function along with the variables that are captured. Note that I do not use that definition in this article!

```js
function greet(whattosay) {

   return function(name) {
       console.log(whattosay + ' ' + name);
   }

}

var sayHi = greet('Hi');
sayHi('Tony');

```	

```js
function buildFunctions() {

    var arr = [];

    for (var i = 0; i < 3; i++) {

	arr.push(
	    function() {
		console.log(i);   
	    }
	)

    }

    return arr;
}

var fs = buildFunctions();

fs[0](); // 3
fs[1](); // 3
fs[2](); // 3
// All three point at the same memory spot going up the scope 
// When executed it all childern function can tell only their parents value in the memory right 
// since we are executing then right now after it execution context is poped out 


function buildFunctions2() {
    var arr = [];
    for (var i = 0; i < 3; i++) {
	 let j = i; // with ES6
	 arr.push(
	 function() {
	    console.log(j);   
	  }
	)
    }
    return arr;
}
var fs2 = buildFunctions2();
fs2[0]();
fs2[1]();
fs2[2]();

function buildFunctions2() {

    var arr = [];

    for (var i = 0; i < 3; i++) {
	arr.push(
	    (function(j) {
		return function() {
		    console.log(j);   
		}
	    }(i))
	)

    }

    return arr;
}

var fs2 = buildFunctions2();

fs2[0]();
fs2[1]();
fs2[2]();
```

![Alt text](img/closur.png?raw=true "Title")

> Callback Function 

> :- A function you give to another fucntion, to be run when the other function is finished

> So the function you call (i.e. invoke), 'calls back' by calling function you gave it when it finishes.
	
```js
function sayHiLater() {
    var greeting = 'Hi!';

    setTimeout(function() {
	console.log(greeting);
    }, 3000);
}

sayHiLater();

// jQuery uses function expressions and first-class functions!
//$("button").click(function() {
//    
//});

function tellMeWhenDone(callback) {
    var a = 1000; // some work
    var b = 2000; // some work

    callback(); // the 'callback', it runs the function I give it!
}

tellMeWhenDone(function() {
    console.log('I am done!');
});

tellMeWhenDone(function() {
    console.log('All done...');
});
```






### 6. This keyword variant 
### 7. Functions and objects 


### 8. Call bind apply 

> bind() - creates a copy and won't executes it.

> call() - will take aruments and executes

> apply() - same as call() but it takes arguments in array
	
> By using them we can borrow/currying functions from other objects 
	
> Function Currying :- Creating a copy of a function but with some preset parameters
	
```js
var person = {
    firstname: 'John',
    lastname: 'Doe',
    getFullName: function() {
	var fullname = this.firstname + ' ' + this.lastname;
	return fullname;
    }
}

var logName = function(lang1, lang2) {
    console.log('Logged: ' + this.getFullName());
    console.log('Arguments: ' + lang1 + ' ' + lang2);
    console.log('-----------');
}

var logPersonName = logName.bind(person);
logPersonName('en');

logName.call(person, 'en', 'es');
logName.apply(person, ['en', 'es']);

(function(lang1, lang2) {
    console.log('Logged: ' + this.getFullName());
    console.log('Arguments: ' + lang1 + ' ' + lang2);
    console.log('-----------');
}).apply(person, ['es', 'en']);

// -----------------------------------------------------

// function borrowing
var person2 = {
    firstname: 'Jane',
    lastname: 'Doe'
}

console.log(person.getFullName.apply(person2));

// function currying
function multiply(a, b) {
    return a*b;   
}

var multipleByTwo = multiply.bind(this, 2);
console.log(multipleByTwo(4));

var multipleByThree = multiply.bind(this, 3);
console.log(multipleByThree(4));
```

![Alt text](img/cab.png?raw=true "Title")




### 9. Function Constructors 
### 10. The new keyword
### 11. arguments 
### 12. Spread
### 13. Arrow function behavior changes 
 
