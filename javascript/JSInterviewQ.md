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
