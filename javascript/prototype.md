# Understanding JavaScript Prototypes.

What is a prototype?

A prototype is an object from which other objects inherit properties

Can any object be a prototype?

Yes.

Which objects have prototypes?

Every object has a prototype by default. Since prototypes are themselves objects, every prototype has a prototype too. (There is only one exception, the default object prototype at the top of every prototype chain. More on prototype chains later)

OK back up, what is an object again?

An object in JavaScript is any unordered collection of key-value pairs. If it’s not a primitive (undefined, null, boolean, number or string) it’s an object.

You said every object has a prototype. But when I write ({}).prototype I get undefined. Are you crazy?

Forget everything you learned about the prototype property – it’s probably the biggest source of confusion about prototypes. The true prototype of an object is held by the internal [[Prototype]] property. ECMA 5 introduces the standard accessor Object.getPrototypeOf(object) which to-date is implemented in Firefox, Safari, Chrome and IE9. In addition all browsers except IE support the non-standard accessor __proto__. Failing that we can ask the object’s constructor for its prototype property.
