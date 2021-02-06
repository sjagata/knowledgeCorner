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


#### Event loop
#### Execution context 
#### Prototypal inheritance 
#### Closures
#### This keyword variant 
#### Functions and objects 
#### Call bind apply 

#### Function Constructors 
#### The new keyword
#### arguments 
#### Spread
#### Arrow function behavior changes 
 
