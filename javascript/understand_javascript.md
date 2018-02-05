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

2. Object Literals
	```js
	var Tony = { 
	    firstname: 'Tony', 
	    lastname: 'Alicea',
	    address: {
		street: '111 Main St.',
		city: 'New York',
		state: 'NY'
	    }
	};

	function greet(person) {
	    console.log('Hi ' + person.firstname);
	}

	greet(Tony);

	greet({ 
	    firstname: 'Mary', 
	    lastname: 'Doe' 
	});

	Tony.address2 = {
	    street: '333 Second St.'
	}
	```

3. Faking Namespaces
	```js
	var greet = 'Hello!';
	var greet = 'Hola!'; 

	console.log(greet);

	var english = { 
	    greetings: { 
		basic: 'Hello!' 
	    } 
	};

	var spanish = {};

	spanish.greet = 'Hola!';

	console.log(english);
	```

4. JSON and Object Literals
	> JSON is inspired by Object literals in JavaScript. Both are different.
	> XML is a huge amount of wasted download bandwith with 
	
	```js
	var objectLiteral = {
	    firstname: 'Mary',
	    isAProgrammer: true
	}

	console.log(JSON.stringify(objectLiteral));

	var jsonValue = JSON.parse('{ "firstname": "Mary", "isAProgrammer": true }');

	console.log(jsonValue);
	```
4. Functions are Objects
	```js
	function greet() {
	    console.log('hi');   
	}

	greet.language = 'english';
	console.log(greet.language); //english
	```

![Alt text](img/functions.png?raw=true "Title")

5. Function Statements and Function Expressions
	> Expression - A unit of code that results in a value
	
	```js
	greet();

	// function statement
	function greet() {
	    console.log('hi');   
	}
	
	// anonymousGreet(); // this will throw undefined is not a function we are invoking a variable which is undefined, Javascript hoisted only variable until it executes below lines 

	// function expression
	var anonymousGreet = function() {
	    console.log('hi');   
	}

	anonymousGreet();

	function log(a) {
	   a();    
	}

	log(function() {
	    console.log('hi');   
	});
	```

6. By Value vs By Reference
	> All primitives are by value
	> All functions are by reference
	
	> Mutate - To change something
	> Immutable - can't be changed
	
	```js
	// by value (primitives)
	var a = 3;
	var b;

	b = a;
	a = 2;

	console.log(a); // 2
	console.log(b); // 3

	// by reference (all objects (including functions))
	var c = { greeting: 'hi' };
	var d;

	d = c;
	c.greeting = 'hello'; // mutate

	console.log(c); // {greeting: "hello"}
	console.log(d); // {greeting: "hello"}

	// by reference (even as parameters)
	function changeGreeting(obj) {
	    obj.greeting = 'Hola'; // mutate   
	}

	changeGreeting(d);
	console.log(c); // {greeting: "Hola"}
	console.log(d); // {greeting: "Hola"}

	// equals operator sets up new memory space (new address)
	c = { greeting: 'howdy' };
	console.log(c); // { greeting: 'howdy' }
	console.log(d); //  { greeting: 'Hola' }
	```

![Alt text](img/byvalue.png?raw=true "Title")

![Alt text](img/byref.png?raw=true "Title")


7. Objects, Functions and this
	> When a function is invoked a new execution context is created
	
	```js
	function a() {
	    console.log(this);
	    this.newvariable = 'hello';
	}

	var b = function() {
	    console.log(this);   
	}

	a();

	console.log(newvariable); // not good!

	b();

	var c = {
	    name: 'The c object',
	    log: function() {
		var self = this;

		self.name = 'Updated c object';
		console.log(self);

		var setname = function(newname) {
		    self.name = newname;   
		}
		setname('Updated again! The c object');
		console.log(self);
	    }
	}

	c.log();

	```

8. Arrays - Collections of Anything
	```js
	var arr = [
	    1, 
	    false, 
	    {
		name: 'Tony',
		address: '111 Main St.'
	    },
	    function(name) {
		var greeting = 'Hello ';
		console.log(greeting + name);
	    },
	    "hello"
	];

	console.log(arr); // (5) [1, false, {…}, ƒ, "hello"]
	arr[3](arr[2].name); // Hello Tony
	```

9. Arguments and spread
	> The Parameters you pass to a function
	> 'arguments' acts like an array but it is not javascript array
	
	```js
	function greet(firstname, lastname, language) {

	    language = language || 'en';
	    
	    console.log(Array.isArray(arguments)); // false

	    if (arguments.length === 0) {
		console.log('Missing parameters!');
		console.log('-------------');
		return;
	    }

	    console.log(firstname);
	    console.log(lastname);
	    console.log(language);
	    console.log(arguments);
	    console.log('arg 0: ' + arguments[0]);
	    console.log('-------------');

	}

	greet(); // 'Missing parameters!'
	greet('John'); 
	// John 
	// undefined 
	// en 
	// Arguments ["John", callee: ƒ, Symbol(Symbol.iterator): ƒ]
	// arg 0: John
	// -------------
	
	greet('John', 'Doe');
	// John 
	// Doe 
	// en 
	// Arguments(2) ["John", "Doe", callee: ƒ, Symbol(Symbol.iterator): ƒ]
	// arg 0: John
	// -------------
	
	greet('John', 'Doe', 'es');
	// John 
	// Doe 
	// es 
	// Arguments(3) ["John", "Doe", "es", callee: ƒ, Symbol(Symbol.iterator): ƒ]
	// arg 0: John
	// -------------

	// in ES6 I can do:  function greet(firstname, ...other)
	// and 'other' will be an array that contains the rest of the arguments
	```

![Alt text](img/execontext.png?raw=true "Title")

10. Function Overloading
	```js
	function greet(firstname, lastname, language) {

	    language = language || 'en';

	    if (language === 'en') {
		console.log('Hello ' + firstname + ' ' + lastname);   
	    }

	    if (language === 'es') {
		console.log('Hola ' + firstname + ' ' + lastname);   
	    }

	}

	function greetEnglish(firstname, lastname) {
	    greet(firstname, lastname, 'en');   
	}

	function greetSpanish(firstname, lastname) {
	    greet(firstname, lastname, 'es');   
	}

	greetEnglish('John', 'Doe');
	greetSpanish('John', 'Doe');
	```
11. Automatic Semicolon Insertion
	> All keep your semicolon 
	
	```js
	function getPerson() {
	    return 
	    {
		firstname: 'Tony'
	    }
	    // vs
	    //return {
	    //  firstname: 'Tony'
	    //}
	    
	}
	console.log(getPerson()); // undefined
	```






