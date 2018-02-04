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

<br>

<hr>

<br>


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


### Operator
> A Special function that is syntactically written differently

[Operator_Precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

* equals assotivity is right-left
```js
var a=1, b=2, c=3;

a = b = c;

console.log(a); //4
console.log(b); //4
console.log(c); //4
```


### Coercion
> Converting a value from one type to another
```js
var a = 1 + '2';
console.log(a); // 12
```

### Comparison Operators
```js
console(1 < 2 < 3); // true (1<2) = true < 3 (1<3) = true
console(3 < 2 < 1); // true (3<2) = false < 1 (0<1) = true

// true is coerced to 1
// false is coerced to 0
```

* 99% try to use `===` for comparision to avoid serious bugs

[Equality_comparisons_and_sameness](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)


### Existance and booleans
a is coerced as Boolean(undefined) == false, Boolean(null) == false, Boolean("") == false

```js
var a;

// goes to internet and looks for a value

if (a || a === 0 ) {
    console.log('Something is there.');
}

Boolean(undefined) // false
Boolean(null) // false 
Boolean("") // false

// Not for 0 
// Boolean(0) // fasle but if a = 0 then above if condition will be true
```

### Default Values

```js
function greet(name) {
    name = name || 'No Name';
    console.log('Hello ' + name);    
}

greet('Tony');
greet();
```

<br>

<hr>

<br>

## Objects and functions

1. Objects and Dot
	```js
	var person = new Object();

	person["firstname"] = "Tony";
	person["lastname"] = "Alicea";

	var firstNameProperty = "firstname";

	console.log(person);
	console.log(person[firstNameProperty]);

	console.log(person.firstname);
	console.log(person.lastname);

	person.address = new Object();
	person.address.street = "111 Main St.";
	person.address.city = "New York";
	person.address.state = "NY";

	console.log(person.address.street);
	console.log(person.address.city);
	console.log(person["address"]["state"]);
	```

2. 







