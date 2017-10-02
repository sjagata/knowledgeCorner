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

Looking at the output of say2.toString(), we can see that the code refers to the variable text. The anonymous function can reference text which holds the value 'Hello Bob' because the local variables of sayHello2() are kept in a closure.

The magic is that in JavaScript a function reference also has a secret reference to the closure it was created in — similar to how delegates are a method pointer plus a secret reference to an object.


### Final points:

* Whenever you use function inside another function, a closure is used.
* Whenever you use eval() inside a function, a closure is used. The text you eval can reference local variables of the function, and within eval you can even create new local variables by using eval('var foo = …')
* When you use new Function(…) (the Function constructor) inside a function, it does not create a closure. (The new function cannot reference the local variables of the outer function.)
* **A closure in JavaScript is like keeping a copy of all the local variables, just as they were when a function exited.**
* It is probably best to think that a closure is always created just an entry to a function, and the local variables are added to that closure.
* A new set of local variables is kept every time a function with a closure is called (given that the function contains a function declaration inside it, and a reference to that inside function is either returned or an external reference is kept for it in some way).
* Two functions might look like they have the same source text, but have completely different behaviour because of their 'hidden' closure. I don't think JavaScript code can actually find out if a function reference has a closure or not.
* If you are trying to do any dynamic source code modifications (for example: myFunction = Function(myFunction.toString().replace(/Hello/,'Hola'));), it won't work if myFunction is a closure (of course, you would never even think of doing source code string substitution at runtime, but...).
* It is possible to get function declarations within function declarations within functions — and you can get closures at more than one level.
* I think normally a closure is the term for both the function along with the variables that are captured. Note that I do not use that definition in this article!
* I suspect that closures in JavaScript differ from those normally found in functional languages.













