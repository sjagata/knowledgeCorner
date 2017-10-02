# Closures Are Not Magic

**Two one sentence summaries:**

* A closure is one way of supporting first-class functions; it is an expression that can reference variables within its scope (when it was first declared), be assigned to a variable, be passed as an argument to a function, or be returned as a function result.
* Or, a closure is a stack frame which is allocated when a function starts its execution, and not freed after the function returns (as if a 'stack frame' were allocated on the heap rather than the stack!).


```js
function sayHello2(name) {
  var text = 'Hello ' + name; // Local variable
  var say = function() { console.log(text); }
  return say;
}
var say2 = sayHello2('Bob');
say2(); // logs "Hello Bob"
```

The above code has a closure because the anonymous function `function() { console.log(text); }` is declared inside another function, `sayHello2()` in this example. In JavaScript, if you use the `function keyword inside another function, you are creating a closure.

In JavaScript, if you declare a function within another function, then the local variables can remain accessible after returning from the function you called. This is demonstrated above, because we call the function say2() after we have returned from sayHello2(). Notice that the code that we call references the variable text, which was a local variable of the function sayHello2().

```js
function() { console.log(text); } // Output of say2.toString();
```

Looking at the output of `say2.toString()`, we can see that the code refers to the variable text. The anonymous function can reference `text` which holds the value `'Hello Bob'` because the local variables of `sayHello2()` are kept in a closure.

The magic is that in JavaScript a function reference also has a secret reference to the closure it was created in — similar to how delegates are a method pointer plus a secret reference to an object.

#### Example 1

This example shows that the local variables are not copied — they are kept by reference. It is kind of like keeping a stack-frame in memory when the outer function exits!

```js
function say667() {
  // Local variable that ends up within closure
  var num = 42;
  var say = function() { console.log(num); }
  num++;
  return say;
}
var sayNumber = say667();
sayNumber(); // logs 43
```

#### Example 2

All three global functions have a common reference to the same closure because they are all declared within a single call to `setupSomeGlobals()`.

```js
var gLogNumber, gIncreaseNumber, gSetNumber;
function setupSomeGlobals() {
  // Local variable that ends up within closure
  var num = 42;
  // Store some references to functions as global variables
  gLogNumber = function() { console.log(num); }
  gIncreaseNumber = function() { num++; }
  gSetNumber = function(x) { num = x; }
}

setupSomeGlobals();
gIncreaseNumber();
gLogNumber(); // 43
gSetNumber(5);
gLogNumber(); // 5

var oldLog = gLogNumber;

setupSomeGlobals();
gLogNumber(); // 42

oldLog() // 5
```

The three functions have shared access to the same closure — the local variables of `setupSomeGlobals()` when the three functions were defined.

Note that in the above example, if you call `setupSomeGlobals()` again, then a new closure (stack-frame!) is created. The old `gLogNumber`, `gIncreaseNumber`, `gSetNumber` variables are overwritten with new functions that have the new closure. (In JavaScript, whenever you declare a function inside another function, the inside function(s) is/are recreated again each time the outside function is called.)

#### Example 3
This one is a real gotcha for many people, so you need to understand it. Be very careful if you are defining a function within a loop: the local variables from the closure do not act as you might first think.

```js
function buildList(list) {
    var result = [];
    for (var i = 0; i < list.length; i++) {
        var item = 'item' + i;
        result.push( function() {console.log(item + ' ' + list[i])} );
    }
    return result;
}

function testList() {
    var fnlist = buildList([1,2,3]);
    // Using j only to help prevent confusion -- could use i.
    for (var j = 0; j < fnlist.length; j++) {
        fnlist[j]();
    }
}

 testList() //logs "item2 undefined" 3 times

```


#### Example 4 

This final example shows that each call creates a separate closure for the local variables. There is not a single closure per function declaration. There is a closure for each call to a function.

```js
function newClosure(someNum, someRef) {
    // Local variables that end up within closure
    var num = someNum;
    var anArray = [1,2,3];
    var ref = someRef;
    return function(x) {
        num += x;
        anArray.push(num);
        console.log('num: ' + num +
            '; anArray: ' + anArray.toString() +
            '; ref.someVar: ' + ref.someVar + ';');
      }
}
obj = {someVar: 4};
fn1 = newClosure(4, obj);
fn2 = newClosure(5, obj);
fn1(1); // num: 5; anArray: 1,2,3,5; ref.someVar: 4;
fn2(1); // num: 6; anArray: 1,2,3,6; ref.someVar: 4;
obj.someVar++;
fn1(2); // num: 7; anArray: 1,2,3,5,7; ref.someVar: 5;
fn2(2); // num: 8; anArray: 1,2,3,6,8; ref.someVar: 5;
```



### Final points:

* Whenever you use `function` inside another function, a closure is used.
* Whenever you use `eval()` inside a function, a closure is used. The text you `eval` can reference local variables of the function, and within `eval` you can even create new local variables by using `eval('var foo = …')`
* When you use `new Function(…)` (the Function constructor) inside a function, it does not create a closure. (The new function cannot reference the local variables of the outer function.)
* **A closure in JavaScript is like keeping a copy of all the local variables, just as they were when a function exited.**
* It is probably best to think that a closure is always created just an entry to a function, and the local variables are added to that closure.
* A new set of local variables is kept every time a function with a closure is called (given that the function contains a function declaration inside it, and a reference to that inside function is either returned or an external reference is kept for it in some way).
* Two functions might look like they have the same source text, but have completely different behaviour because of their 'hidden' closure. I don't think JavaScript code can actually find out if a function reference has a closure or not.
* If you are trying to do any dynamic source code modifications (for example: `myFunction = Function(myFunction.toString().replace(/Hello/,'Hola'));)`, it won't work if myFunction is a closure (of course, you would never even think of doing source code string substitution at runtime, but...).
* It is possible to get function declarations within function declarations within functions — and you can get closures at more than one level.
* I think normally a closure is the term for both the function along with the variables that are captured. Note that I do not use that definition in this article!
* I suspect that closures in JavaScript differ from those normally found in functional languages.



<br>
<br>

[@article](https://stackoverflow.com/questions/111102/how-do-javascript-closures-work)









