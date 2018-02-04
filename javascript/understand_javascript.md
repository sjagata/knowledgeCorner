### Javascript Objects :
> A Collection of Name-Value pairs.

> Window and this are global objects.

### Execution Context consists:
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

### Functions, Context and Variable Enviornments 
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

### Scope Chain
```js
function a() {
    
    function b() {
        console.log(myVar);
    }
    
	b();
}

var myVar = 1;
a();
```


### Scope
> Where a variable is available in your code 
> `let' - can be used instead of var. let allows javascript engine to use what's called block scoping.

```js
if( a > b ){
 let c = true;
}
```

![Alt text](img/scope.png?raw=true "Title")

### Asynchronous
> Asynchronous more than one at a time

<hr>

## Types & Operators

> Javascript is Dynamically typed
```js
var isNew = true; // no errors
isNew = 'yep!';
isNew = 1;
```

### Primitive Type
> A type of data that reperesents a single value <br> That is, not an object

1. `UNDEFINED` - represents lack of existence (you shouldn't set a variable to this)
2. `NULL` - represents lack of existence (you can set a variable to this)
3. `BOOLEAN` - true or false
4. `NUMBER` - *floating point* number (there's always some decimals). Unlike other languages, there's only one 'number' type... and it can make math weird
5. `STRING` - a sequence of characters (both '' and "" can be used)
6. `SYMBOL` - Used in ES6 (the next version of javascript)
























