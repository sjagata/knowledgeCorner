### Appened an array to another array

 1. `spread operator` feature of ES6:
 ```js
 let fruits = [ 'apple', 'banana'];
const moreFruits = [ 'orange', 'plum' ];

fruits.push(...moreFruits); // ["apple", "banana", "orange", "plum"]
```

2. Add pushArray to `Array's` prototype:
```js
Array.prototype.pushArray = function(arr) {
    this.push.apply(this, arr);
};

var newArray = [];
newArray.pushArray(dataArray1);
newArray.pushArray(dataArray2);
```

3. ... or emulate the original push() method by allowing multiple parameters using the fact that concat(), like push(), allows multiple parameters:
```
Array.prototype.pushArray = function() {
    this.push.apply(this, this.concat.apply([], arguments));
};

var newArray = [];
newArray.pushArray(dataArray1, dataArray2);
```

4. Here's a loop-based version of the last example, suitable for large arrays and all major browsers, including IE <= 8:
```
Array.prototype.pushArray = function() {
    var toPush = this.concat.apply([], arguments);
    for (var i = 0, len = toPush.length; i < len; ++i) {
        this.push(toPush[i]);
    }
};
```
