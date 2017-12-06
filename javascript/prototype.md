# Understanding JavaScript Prototypes.

### What is a prototype?

A prototype is an object from which other objects inherit properties

### Can any object be a prototype?

Yes.

### Which objects have prototypes?

Every object has a prototype by default. Since prototypes are themselves objects, every prototype has a prototype too. (There is only one exception, the default object prototype at the top of every prototype chain. More on prototype chains later)

### OK back up, what is an object again?

An object in JavaScript is any unordered collection of key-value pairs. If it’s not a primitive (undefined, null, boolean, number or string) it’s an object.

### You said every object has a prototype. But when I write ({}).prototype I get undefined. Are you crazy?

Forget everything you learned about the prototype property – it’s probably the biggest source of confusion about prototypes. The true prototype of an object is held by the internal [[Prototype]] property. ECMA 5 introduces the standard accessor Object.getPrototypeOf(object) which to-date is implemented in Firefox, Safari, Chrome and IE9. In addition all browsers except IE support the non-standard accessor __proto__. Failing that we can ask the object’s constructor for its prototype property.

```js
var a = {};
 
Object.getPrototypeOf(a); //[object Object]
 
a.__proto__; //[object Object]
 
//all browsers
//(but only if constructor.prototype has not been replaced and fails with Object.create)
a.constructor.prototype; //[object Object]
```

### Example

```js
//Constructor. &lt;em&gt;this&lt;/em&gt; is returned as new object and its internal [[prototype]] property will be set to the constructor's default prototype property
var Circle = function(radius) {
this.radius = radius;
//next line is implicit, added for illustration only
//this.__proto__ = Circle.prototype;
}
 
//augment Circle's default prototype property thereby augmenting the prototype of each generated instance
Circle.prototype.area = function() {
return Math.PI*this.radius*this.radius;
}
 
//create two instances of a circle and make each leverage the common prototype
var a = new Circle(3), b = new Circle(4);
a.area().toFixed(2); //28.27
b.area().toFixed(2); //50.27
```

If I modify the existing prototype’s property then this is true, because a.__proto__ is a reference to the object defined by A.prototype at the time it was created.

```js
var A = function(name) {
this.name = name;
}
 
var a = new A('alpha');
a.name; //'alpha'
 
A.prototype.x = 23;
 
a.x; //23
```

But if I replace the prototype property with a new object, a.__proto__ still references the original object.

```js
var A = function(name) {
this.name = name;
}
 
var a = new A('alpha');
a.name; //'alpha'
 
A.prototype = {x:23};
 
a.x; //null
```

<br>
<br>

```js
const food = {
 init: function(type){
  this.type = type;
 },
 eat: function(){
  console.log(" I ate " + this.type)
 }
}

const waffle = Object.create(food);
waffle.init('waffle');
waffle.eat();


const carrot = Object.create(food);
waffle.init('carrot');
waffle.eat();

// Output:
// I ate waffle
// I ate carrot

```

<br>

[ref](https://javascriptweblog.wordpress.com/2010/06/07/understanding-javascript-prototypes/)








