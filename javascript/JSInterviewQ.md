### 1. What is the difference between undefined and not defined in JavaScript?
In JavaScript, if you try to use a variable that doesn't exist and has not been declared, then JavaScript will throw an error var name is not defined and script will stop executing. However, if you use typeof undeclared_variable, then it will return undefined.

Before getting further into this, let's first understand the difference between declaration and definition.

Let's say **var x** is a declaration because you have not defined what value it holds yet, but you have declared its existence and the need for memory allocation.

```js
var x; // declaring x
console.log(x); //output: undefined 
```

The assignment happens in order, so when we try to access a variable that is declared but not defined yet, we will get the result undefined.

```js
var x; // Declaration
if(typeof x === 'undefined') // Will return true
```

If a variable that is neither declared nor defined, when we try to reference such a variable we'd get the result not defined.

```js
console.log(y); // Output: ReferenceError: y is not defined
```

### 2. What is the drawback of creating true private methods in JavaScript?
One of the drawbacks of creating true private methods in JavaScript is that they are very memory-inefficient, as a new copy of the method would be created for each instance.

```js
var Employee = function (name, company, salary) {
    this.name = name || "";       //Public attribute default value is null
    this.company = company || ""; //Public attribute default value is null
    this.salary = salary || 5000; //Public attribute default value is null

    // Private method
    var increaseSalary = function () {
        this.salary = this.salary + 1000;
    };

    // Public method
    this.dispalyIncreasedSalary = function() {
        increaseSlary();
        console.log(this.salary);
    };
};

// Create Employee class object
var emp1 = new Employee("John","Pluto",3000);
// Create Employee class object
var emp2 = new Employee("Merry","Pluto",2000);
// Create Employee class object
var emp3 = new Employee("Ren","Pluto",2500);
```

Here each instance variable emp1, emp2, emp3 has its own copy of the increaseSalary private method.

So, as a recommendation, don’t use private methods unless it’s necessary.

### 3. What is a “closure” in JavaScript? Provide an example
A closure is a function defined inside another function (called the parent function), and has access to variables that are declared and defined in the parent function scope.

The closure has access to variables in three scopes:

* Variables declared in their own scope
* Variables declared in a parent function scope
* Variables declared in the global namespace

```js
var globalVar = "abc"; 

// Parent self invoking function 
(function outerFunction (outerArg) { // begin of scope outerFunction
    // Variable declared in outerFunction function scope 
    var outerFuncVar = 'x';    
    // Closure self-invoking function 
    (function innerFunction (innerArg) { // begin of scope innerFunction
        // variable declared in innerFunction function scope
        var innerFuncVar = "y"; 
        console.log(          
            "outerArg = " + outerArg + "\n" +
            "outerFuncVar = " + outerFuncVar + "\n" +
            "innerArg = " + innerArg + "\n" +
            "innerFuncVar = " + innerFuncVar + "\n" +
            "globalVar = " + globalVar);
 
    }// end of scope innerFunction
    )(5); // Pass 5 as parameter 
}// end of scope outerFunction 
)(7); // Pass 7 as parameter 
```

**innerFunction is closure** that is defined inside outerFunction and has access to all variables declared and defined in the outerFunction scope. In addition, the function defined inside another function as a closure will have access to variables declared in the global namespace.

Thus, the output of the code above would be:

```js
outerArg = 7
outerFuncVar = x
innerArg = 5
innerFuncVar = y
globalVar = abc
```

### 4. Write a mul function which will produce the following outputs when invoked:

```js
console.log(mul(2)(3)(4)); // output : 24 
console.log(mul(4)(3)(4)); // output : 48
```

Below is the answer followed by an explanation to how it works:

```js
function mul (x) {
    return function (y) { // anonymous function 
        return function (z) { // anonymous function 
            return x * y * z; 
        };
    };
}
```

Here the mul function accepts the first argument and returns an anonymous function, which takes the second parameter and returns another anonymous function that will take the third parameter and return the multiplication of the arguments that have been passed.

In JavaScript, a function defined inside another one has access to the outer function's variables. Therefore, a function is a first-class object that can be returned by other functions as well and be passed as an argument in another function.

*  function is an instance of the Object type
* A function can have properties and has a link back to its constructor method
* A function can be stored as a variable
* A function can be pass as a parameter to another function
* A function can be returned from another function

### 5. How to empty an array in JavaScript?
For instance,

```js
var arrayList =  ['a','b','c','d','e','f'];
```

```js
//method1
arrayList = []

//method2
arrayList.length = 0;

//method3
var arrayList = ['a','b','c','d','e','f']; // Created array 
var anotherArrayList = arrayList;  // Referenced arrayList by another variable 
arrayList.splice(0, arrayList.length); // Empty the array by setting length to 0
console.log(anotherArrayList); // Output []

//method4
while(arrayList.length){
  arrayList.pop();
}
```

### 6. How do you check if an object is an array or not?
The best way to find out whether or not an object is an instance of a particular class is to use the toString method from Object.prototype:

```js
 var arrayList = [1,2,3];
 
 if( Object.prototype.toString.call( arrayList ) === '[object Array]' ) {
    console.log('Array!');
}
```

If you are using jQuery, then you can also use the jQuery isArray method:

```js
if($.isArray(arrayList)){
    console.log('Array');
}else{
  	console.log('Not an array');
}
```

```js
Array.isArray(arrayList);

// Array.isArray is supported by Chrome 5, Firefox 4.0, IE 9, Opera 10.5 and Safari 5
```

### 7. What will be the output of the following code?

```js
var output = (function(x){
    delete x;
    return x;
  })(0);
  
  console.log(output);
```

The output would be 0. The delete operator is used to delete properties from an object. Here x is not an object but a local variable. delete operators don't affect local variables.

```js
var x = { foo : 1};
var output = (function(){
    delete x.foo;
    return x.foo;
  })();
  
  console.log(output); // undefined
  ```

### 8. What will be the output of the code below?

1. Question1

```js
var Employee = {
  company: 'xyz'
}
var emp1 = Object.create(Employee);
delete emp1.company
console.log(emp1.company);
```

The output would be xyz. Here, emp1 object has company as its prototype property. The delete operator doesn't delete prototype property.

emp1 object doesn't have company as its own property. You can test it console.log(emp1.hasOwnProperty('company')); //output : false. However, we can delete the company property directly from theEmployee object using delete Employee.company. Or, we can also delete the emp1 object using the __proto__ property delete emp1.__proto__.company.


2. Question2 

```js
var bar = true;
console.log(bar + 0);   
console.log(bar + "xyz");  
console.log(bar + true);  
console.log(bar + false);  
```

The code will output 1, "truexyz", 2, 1. Here's a general guideline for addition operators:

* Number + Number -> Addition
* Boolean + Number -> Addition
* Boolean + Number -> Addition
* Number + String -> Concatenation
* String + Boolean -> Concatenation
* String + String -> Concatenation

3. Question4 

```js
var z = 1, y = z = typeof y;
console.log(y);  


//The output would be undefined. According to the associativity rule, operators with the same precedence are processed based on the associativity property of the operator. Here, the associativity of the assignment operator is Right to Left, so typeof y will evaluate first , which is undefined. It will be assigned to z, and then y would be assigned the value of z and then z would be assigned the value 1
```

### 9. What is undefined x 1 in JavaScript?

```js
var trees = ["redwood","bay","cedar","oak","maple"];
delete trees[3];
```

When you run the code above and type console.log(trees); into your Chrome developer console, you will get
["redwood", "bay", "cedar", undefined × 1, "maple"]. When you run the code in Firefox's browser console, you will get ["redwood", "bay", "cedar", undefined, "maple"]. Thus, it's clear that the Chrome browser has its own way of displaying uninitialised indexes in arrays. However, when you check trees[3] === undefined in both browsers, you will get similar output as true.

Note: Please remember you do not need to check for the uninitialised index of array in trees[3] === 'undefined × 1', as it will give you an error. 'undefined × 1' is just way of displaying an array's uninitialised index in Chrome.

```js
var trees = ["xyz","xxxx","test","ryan","apple"];
delete trees[3];
  
  console.log(trees.length);
  ```
  
  The output would be 5. When we use the delete operator to delete an array element, the array length is not affected from this. This holds even if you deleted all elements of an array using the delete operator.

In other words, when the delete operator removes an array element, that deleted element is not longer present in array. In place of value at deleted index undefined x 1 in chrome and undefined is placed at the index. If you do console.log(trees) output ["xyz", "xxxx", "test", undefined × 1, "apple"] in Chrome and in Firefox ["xyz", "xxxx", "test", undefined, "apple"].

### 10. How JavaScript Event Delegation Works?
Let's say that we have a parent **UL** element with several child elements:

```js
<ul id="parent-list">
	<li id="post-1">Item 1</li>
	<li id="post-2">Item 2</li>
	<li id="post-3">Item 3</li>
	<li id="post-4">Item 4</li>
	<li id="post-5">Item 5</li>
	<li id="post-6">Item 6</li>
</ul>
```

when the event bubbles up to the UL element, you check the event object's target property to gain a reference to the actual clicked node.  Here's a very basic JavaScript snippet which illustrates event delegation:

```js
// Get the element, add a click listener...
document.getElementById("parent-list").addEventListener("click", function(e) {
	// e.target is the clicked element!
	// If it was a list item
	if(e.target && e.target.nodeName == "LI") {
		// List item found!  Output the ID!
		console.log("List item ", e.target.id.replace("post-", ""), " was clicked!");
	}
});
```

```js
// Get the parent DIV, add click listener...
document.getElementById("myDiv").addEventListener("click",function(e) {
	// e.target was the clicked element
  if (e.target && e.target.matches("a.classA")) {
    console.log("Anchor element clicked!");
	}
});
```

### 11. What is the difference between e.target and e.currentTarget?

**Event.currentTarget** identifies the current target for the event, as the event traverses the DOM. It always refers to the element to which the event handler has been attached, as opposed to event.target which identifies the element on which the event occurred.

`event.currentTarget` is interesting to use when attaching the same event handler to several elements.

```js
function hide(e){
  e.currentTarget.style.visibility = "hidden";
  console.log(e.currentTarget);
  // When this function is used as an event handler: this === e.currentTarget
}

var ps = document.getElementsByTagName('p');

for(var i = 0; i < ps.length; i++){
  // console: print the clicked <p> element 
  ps[i].addEventListener('click', hide, false);
}
// console: print <body>
document.body.addEventListener('click', hide, false);

// click around and make paragraphs disappear
```

### 12. What is Window.postMessage() and where it can be used?
The `window.postMessage()` method safely enables cross-origin communication. Normally, scripts on different pages are allowed to access each other if and only if the pages that executed them are at locations with the same protocol (usually both https), port number (443 being the default for https), and host (modulo Document.domain being set by both pages to the same value). window.postMessage() provides a controlled mechanism to circumvent this restriction in a way which is secure when properly used.

```js
// Syntax:
otherWindow.postMessage(message, targetOrigin, [transfer]);
```

`otherWindow` can listen for dispatched messages by executing the following JavaScript:

```js
window.addEventListener("message", receiveMessage, false);

function receiveMessage(event)
{
  if (event.origin !== "http://example.org:8080")
    return;

  // ...
}
```

```js
/*
 * In window A's scripts, with A being on <http://example.com:8080>:
 */

var popup = window.open(...popup details...);

// When the popup has fully loaded, if not blocked by a popup blocker:

// This does nothing, assuming the window hasn't changed its location.
popup.postMessage("The user is 'bob' and the password is 'secret'",
                  "https://secure.example.net");

// This will successfully queue a message to be sent to the popup, assuming
// the window hasn't changed its location.
popup.postMessage("hello there!", "http://example.com");

function receiveMessage(event)
{
  // Do we trust the sender of this message?  (might be
  // different from what we originally opened, for example).
  if (event.origin !== "http://example.com")
    return;

  // event.source is popup
  // event.data is "hi there yourself!  the secret response is: rheeeeet!"
}
window.addEventListener("message", receiveMessage, false);
```

```js
/*
 * In the popup's scripts, running on <http://example.com>:
 */

// Called sometime after postMessage is called
function receiveMessage(event)
{
  // Do we trust the sender of this message?
  if (event.origin !== "http://example.com:8080")
    return;

  // event.source is window.opener
  // event.data is "hello there!"

  // Assuming you've verified the origin of the received message (which
  // you must do in any case), a convenient idiom for replying to a
  // message is to call postMessage on event.source and provide
  // event.origin as the targetOrigin.
  event.source.postMessage("hi there yourself!  the secret response " +
                           "is: rheeeeet!",
                           event.origin);
}

window.addEventListener("message", receiveMessage, false);
```

### 13. How to check whether a key exist in a JavaScript object or not.
Let say we have person object with property name and age

```js
var person = {
	name: 'Nishant',
	age: 24
}
```

Method 1: We can use `in` operator on objet to check own property or inherited property.

```js
console.log('name' in person); // checking own property print true 
console.log('salary' in person); // checking undefined property print false
```

`in` operator also look into inherited property if it doesn't find property defined as own property. For instance If I check existence of toString property as we know that we haven't declared this property on person object so in operator look into there base property.

Here

```js
console.log('toString' in person); // Will print true
```

If we want to test property of object instance not inherited properties then we will use `hasOwnProperty` method of object instance.

```js
console.log(person.hasOwnProperty('toString')); // print false
console.log(person.hasOwnProperty('name')); // print true
console.log(person.hasOwnProperty('salary')); // print false
```

### 14. Best way to detect reference values of any type in JavaScript ?
Detecting object using typeof operator

```js
console.log(typeof {});           // object
console.log(typeof []);           // object
console.log(typeof new Array());  // object
console.log(typeof null);         // object 
console.log(typeof new RegExp()); // object
console.log(typeof new Date());   // object
```

The best way to detect an object of specific reference type using instanceof operator.

> Syntax : value instanceof constructor

```js
//Detecting an array
if(value instanceof Array){
	console.log("value is type of array");
}
```

### 15.How we can prevent modification of object in JavaScript ?

>ECMAScript 5 introduce several methods to prevent modification of object which lock down object to ensure that no one, >accidentally or otherwise, change functionality of Object.

**1: Prevent extensions :**

```js
var employee = {
	name: "javascript"
};

// lock the object 
Object.preventExtensions(employee);

// Now try to change the employee object property name
employee.name = "John Doe"; // work fine 

//Now try to add some new property to the object
employee.age = 24; // fails silently unless it's inside the strict mode
```

**2: Seal :**

>It is same as prevent extension, in addition to this also prevent existing properties and methods from being deleted.

To seal an object, we use **_Object.seal()_** method. you can check whether an object is sealed or not using **_Object.isSealed();_**

```js
var employee = {
	name: "Javascript"
};

// Seal the object 
Object.seal(employee);

console.log(Object.isExtensible(employee)); // false
console.log(Object.isSealed(employee)); // true

delete employee.name // fails silently unless it's in strict mode

// Trying to add new property will give an error
employee.age = 30; // fails silently unless in strict mode
```

**3. Freeze:**

>Same as seal, In addition to this prevent existing properties methods from being modified (All properties and methods are >read only).

```js
var employee = {
	name: "Javascript"
};

//Freeze the object
Object.freeze(employee); 

// Seal the object 
Object.seal(employee);

console.log(Object.isExtensible(employee)); // false
console.log(Object.isSealed(employee));     // true
console.log(Object.isFrozen(employee));     // true


employee.name = "xyz"; // fails silently unless in strict mode
employee.age = 30;     // fails silently unless in strict mode
delete employee.name   // fails silently unless it's in strict mode
```

### 16. Write a log function which will add prefix (your message) to every message you log using console.log ?

```js
function appLog() {
  var args = Array.prototype.slice.call(argument);
  args.unshift('your app name');
  console.log.apply(console, args);
}

console.log(appLog("Some error message")); 
//output of above console: 'your app name Some error message'
```

### 17. What is non-enumerable property in JavaScript and how can create ?

To create a non-enumerable property we have to use Object.defineProperty(). This is a special method for creating non-enumerable property in JavaScript.

```js
var person = {
	name: 'John'
};
person.salary = '10000$';
person['country'] = 'USA';

// Create non-enumerable property
Object.defineProperty(person, 'phoneNo',{
	value : '8888888888',
	enumerable: false
})

Object.keys(person); // ['name', 'salary', 'country']
```

In above example phoneNo property didn't show up because we made it non-enumerable by setting enumerable:false

Changing non-enumerable property value will return error in strict mode. In non-strict mode it won't through any error but it won't change the value of phoneNo.


### 18. Explain the difference between “==” and “===”?
“==” checks only for equality in value whereas “===” is a stricter equality test and returns false if either the value or the type of the two variables are different.

### 19. Explain how to detect the operating system on the client machine?
In order to detect the operating system on the client machine, the `navigator.appVersion` string (property) should be used.

### 20. What are JavaScript Cookies?
Cookies are the small test files stored in a computer and it gets created when the user visits the websites to store information that they need. Example could be User Name details and shopping cart information from the previous visits.

### 21. Which keywords are used to handle exceptions?

```js
Try{
 
Code
 
}
 
Catch(exp){
 
Code to throw an exception
 
}
 
Finally{
 
Code runs either it finishes successfully or after catch
 
}
```

### 22. What is unshift method in JavaScript?
Unshift method is like push method which works at the beginning of the array.  This method is used to prepend one or more elements to the beginning of the array.

### 23. What is the ‘Strict’ mode in JavaScript and how can it be enabled?
The short and most important answer here is that `use strict` is a way to voluntarily enforce stricter parsing and error handling on your JavaScript code at runtime. Code errors that would otherwise have been ignored or would have failed silently will now generate errors or throw exceptions. In general, it is a good practice.

```js
function myfunction(){
“use strict";
 
var v = “This is a strict mode function";
 
}
```

Some of the key benefits of strict mode include:

* `Makes debugging easier.` Code errors that would otherwise have been ignored or would have failed silently will now generate errors or throw exceptions, alerting you sooner to problems in your code and directing you more quickly to their source.
* `Prevents accidental globals.` Without strict mode, assigning a value to an undeclared variable automatically creates a global variable with that name. This is one of the most common errors in JavaScript. In strict mode, attempting to do so throws an error.
* `Eliminates this coercion.` Without strict mode, a reference to a `this` value of null or undefined is automatically coerced to the global. This can cause many headfakes and pull-out-your-hair kind of bugs. In strict mode, referencing a `this` value of null or undefined throws an error.
* `Disallows duplicate parameter values.` Strict mode throws an error when it detects a duplicate named argument for a function (e.g., `function foo(val1, val2, val1){})`, thereby catching what is almost certainly a bug in your code that you might otherwise have wasted lots of time tracking down.
 **_Note: It used to be (in ECMAScript 5) that strict mode would disallow duplicate property names (e.g. `var object = {foo: "bar", foo: "baz"};)` but as of ECMAScript 2015 this is no longer the case._**
* `Makes eval() safer.` There are some differences in the way `eval()` behaves in strict mode and in non-strict mode. Most significantly, in strict mode, variables and functions declared inside of an `eval()` statement are not created in the containing scope (they are created in the containing scope in non-strict mode, which can also be a common source of problems).
* `Throws error on invalid usage of **delete.**` The `delete` operator (used to remove properties from objects) cannot be used on non-configurable properties of the object. Non-strict code will fail silently when an attempt is made to delete a non-configurable property, whereas strict mode will throw an error in such a case.


### 24. HTML5 Local storage vs. Session storage?
`localStorage` and `sessionStorage` both extend `Storage`. There is no difference between them except for the intended "non-persistence" of `sessionStorage`.

That is, the data stored in `localStorage` persists until explicitly deleted. Changes made are saved and available for all current and future visits to the site.

For `sessionStorage`, changes are only available per window (or tab in browsers like Chrome and Firefox). Changes made are saved and available for the current page, as well as future visits to the site on the same window. Once the window is closed, the storage is deleted.

* `localStorage` - use for long term use.
* `sessionStorage` - use when you need to store somthing that changes or somthing temporary

[@articl1](https://stackoverflow.com/questions/19867599/what-is-the-difference-between-localstorage-sessionstorage-session-and-cookies)

[@article2](https://stackoverflow.com/questions/5523140/html5-local-storage-vs-session-storage)

### 25. Explain window.onload and onDocumentReady?
The `onload` function is not run until all the information on the page is loaded. This leads to a substantial delay before any code is executed.

`onDocumentReady` loads the code just after the DOM is loaded. This allows early manipulation of the code.

* `window.load()` - is a standard event in the DOM, will runs once the entire page(images, iframes, scripts, links etc..) not just DOM
* `$(document).ready()` - will only runs once the page DOM is ready for **JAVASCRIPT** code to execute. Fires first.

### 26. What is the difference between .call() and .apply()?

The function `.call()` and `.apply()` are very similar in their usage except a little difference. 

* `.call()` is used when the number of the function’s arguments are known to the programmer, as they have to be mentioned as arguments in the call statement. 
* `.apply()` is used when the number is not known. The function .apply() expects the argument to be an array.

The basic difference between `.call()` and `.apply()` is in the way arguments are passed to the function. Their usage can be illustrated by the given example.

```js
var someObject = {
 
myProperty : 'Foo',
 
myMethod : function(prefix, postfix) {
 
alert(prefix + this.myProperty + postfix);
 
}
 
};
 
someObject.myMethod('<', '>'); // alerts '<Foo>'
 
var someOtherObject  = {
 
myProperty : 'Bar'
 
};
 
someObject.myMethod.call(someOtherObject, '<', '>'); // alerts '<Bar>'
 
someObject.myMethod.apply(someOtherObject, ['<', '>']); // alerts '<Bar>'
```

### 27. Define event bubbling?
JavaScript allows DOM elements to be nested inside each other. In such a case, if the handler of the child is clicked, the handler of parent will also work as if it were clicked too.

### 28. How to stop event bubbling on click

> `event.stopPropagation()` - Stops the bubbling of an event to parent elements, preventing any parent handlers from being notified of the event.


> `event.preventDefault()` - Prevents the browser from executing the default action. Use the method isDefaultPrevented to know whether this method was ever called (on that event object).

* `event.stopPropagation()` :- stops an event from bubbling uo the event.
* `event.preventDefault` :- only precludes the brower's default action on that event from occuring.

### 29. Define unescape() and escape() functions?
The `escape ()` function is responsible for coding a string so as to make the transfer of the information from one computer to the other, across a network.

```js
document.write(escape(“Hello? How are you!”)); // Output: Hello%3F%20How%20are%20you%21
```

The `unescape()` function is very important as it decodes the coded string.

```js
document.write(unescape(“Hello%3F%20How%20are%20you%21”)); // Output: Hello? How are you!
```
 
 ### 30. What are the decodeURI() and encodeURI()?
 `EncodeURl()` is used to convert URL into their hex coding. And `DecodeURI()` is used to convert the encoded URL back to normal.

```js
var uri="my test.asp?name=ståle&car=saab";
document.write(encodeURI(uri)+ "<br>");
document.write(decodeURI(uri));
```


### 31. How do you clone an object?

```js
var obj = {a: 1 ,b: 2}
var objclone = object.assign({},obj);
```

Now the value of objclone is `{a: 1 ,b: 2}` but points to a different object than `obj`.






























<br>
<br>
<br>

[ref](https://github.com/nishant8BITS/123-Essential-JavaScript-Interview-Question)

