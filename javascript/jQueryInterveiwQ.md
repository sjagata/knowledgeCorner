### Explain what the following code will do:
```js
$( "div#first, div.first, ol#items > [name$='first']" )
```

This code performs a query to retrieve any `<div>` element with the id first, plus all `<div>` elements with the class first, plus all elements which are children of the `<ol id="items">` element and whose name attribute ends with the string "first". This is an example of using multiple selectors at once. The function will return a jQuery object containing the results of the query.

<br>

### The code below is for an application that requires defining a click handler for all buttons on the page, including those buttons that may be added later dynamically.

What is wrong with this code, and how can it be fixed to work properly even with buttons that are added later dynamically?
```js
// define the click handler for all buttons
$( "button" ).bind( "click", function() {
    alert( "Button Clicked!" )
});

/* ... some time later ... */

// dynamically add another button to the page
$( "html" ).append( "<button>Click Alert!</button>" );
```

The button that is added dynamically after the call to `bind()` will not have the click handler attached. This is because the `bind()` method only attaches handlers to elements that exist at the time the call to bind() is made.

This problem is solved with functions that use “event bubbling” to match events on both current and future elements. In the past, this was done by replacing bind() with live(). live() was deprecated in jQuery 1.7 though. `delegate()` works similarly to `live()` but also provides control over how far an event must bubble up the DOM.

However, the recommended method is to use `on()`, which can behave like `bind()`, `live()`, or `delegate()` depending on syntax. The following code attaches the handler to all current and future buttons:
```js
// define the click handler for all buttons
$( document ).on( "click", "button", function() {
    alert( "Button Clicked!" )
});

/* ... some time later ... */

// dynamically add another button to the page
$( "html" ).append( "<button>Click Alert!</button>" );
```

<br>

### What’s the deal with the `$` in jQuery? What is it and what does it mean? Also, how can jQuery be used in conjunction with another JavaScript library that also uses `$` for naming? Bonus credit if you can provide two answers.

Since `$` has no special meaning in JavaScript, it is free to be used in object naming. In jQuery, it is simply used as an alias for the jQuery object and `jQuery()` function.

However, jQuery has no monopoly on use of `$`, so you may encounter situations where you want to use it in conjunction with another JS library that also uses $, which would therefore result in a naming conflict. jQuery provides the `jQuery.noConflict()` method for just this reason. Calling this method makes it necessary to use the underlying name jQuery instead in subequent references to jQuery and its functions.

Here’s an example from the jQuery documentation:
```js
<script src="other_lib.js"></script>
<script src="jquery.js"></script>
<script>
$.noConflict();
// Code that uses other library's $ can follow here.
</script>
```
Alternatively, you can also use a closure instead of the `$.noConflict()` method; e.g.:
```js
(function ($) {
  // Code in which we know exactly what the meaning of $ is
} (jQuery)); 
```

<br>

### Given the following HTML:
```html
<div id="expander"></div>
```
and the following CSS:
```css
div#expander{
  width: 100px;
  height: 100px;
  background-color: blue;
}
```
Write code in jQuery to animate the #expander div, expanding it from 100 x 100 pixels to 200 x 200 pixels over the course of three seconds.

```js
$( "#expander" ).animate(
  {
    width: "200px",
    height: "200px",
  },
  3000 );
```

<br>

### What is method chaining in jQuery? Provide an example.
```js
$( "button#play-movie" ).on( "click", playMovie )
                        .css( "background-color", "orange" )
                        .show();
```
Notice that with chaining, the button only needs to be selected one time, whereas without chaining, jQuery must search the whole DOM and find the button before each method is applied. Thus, in addition to yielding more concise code, method chaining in jQuery offers a potentially powerful performance advantage.

<br>

### Explain what the following code does:
```js
$( "div" ).css( "width", "300px" ).add( "p" ).css( "background-color", "blue" );
```
This code uses method chaining to accomplish a couple of things. First, it selects all the `<div>` elements and changes their CSS width to 300px. Then, it adds all the `<p>` elements to the current selection, so it can finally change the CSS background color for both the `<div>` and `<p>` elements to blue.

<br>

### What is the difference between jQuery.get() and jQuery.ajax()?
`jQuery.ajax()` is the all-encompassing Ajax request method provided by jQuery. It allows for the creation of highly-customized Ajax requests, with options for how long to wait for a response, how to handle a failure, whether the request is blocking (synchronous) or non-blocking (asynchronous), what format to request for the response, and many more options.

<br>

`jQuery.get()` is a shortcut method that uses `jQuery.ajax()` under the hood, to create an Ajax request that is typical for simple retrieval of information. Other pre-built Ajax requests are provided by jQuery, such as `jQuery.post()`, `jQuery.getScript()`, and `jQuery.getJSON()`.


<br>

### Which of the two lines of code below is more efficient? Explain your answer.
```js
document.getElementById( "logo" );
```
or
```js
$( "#logo" );
```

The first line of code, which is pure JavaScript without jQuery, is more efficient and faster. Executing the second line of code, which is jQuery, will trigger a call to the JavaScript version.



jQuery is built on top of JavaScript and uses its methods under the hood to make DOM manipulation easier, at the cost of some performance overhead. It is a good idea to remember that jQuery is not always better than plain old JavaScript. Always consider whether using jQuery really provides a useful advantage for your project.

<br>

### Explain and contrast the usage of `event.preventDefault()` and `event.stopPropagation()`. Provide an example.
`event.stopPropagation()` stops an event from bubbling up the event chain, whereas `event.preventDefault()` only precludes(prevent from happening) the browser’s default action on that event from occurring, but the event still propogates up the event chain.

For example, consider the following code snippet:
```js
// in this example, 'foo' is a div containing button 'bar'

$("#foo").click(function() {
   // mouse click on div 'foo'
});

$("#bar").click(function(e) {
   // mouse click on button 'bar'
   e.stopPropagation();
});
```
Due to the call to `stopPropagation()` in the button’s click handler, the event never propogates to the div so its click handler never fires. It effectively stops parent elements from knowing about an event on their children.

In contrast, if you replaced the above call to `stopPropagation()` with a call to `preventDefault()`, only the browser’s default action would be precluded, but the div’s click handler would still fire.

(Note: Although the `stopPropagation()` and `preventDefault()` methods are mostly used in jQuery event handling implementations, they apply to plain JavaScript as well.)


<br>

### What selector would I use to query for all elements with an ID that ends with a particular string? Also, how would I modify the selector to retrieve only `<div>` elements whose IDs end with that same string? Provide an example.
 
Let’s say you want to retrieve all elements whose IDs end with “txtTitle”. This could be done using the following selector:
```js
$("[id$='txtTitle']")
```
To retrieve only `<div>` elements whose IDs end with “txtTitle”, the selector would be:
```js
$("div[id$='txtTitle']")
```

<br>

### What is accomplished by returning false from (a) a jQuery event handler, (b) a regular JavaScript onclick event handler for an anchor tag, and (c) a regular JavaScript onclick event handler for a non-anchor tag (e.g., a div, button, etc.)?

* (a) Returning false from a jQuery event handler is effectively the same as calling both preventDefault() and stopPropagation() on the passed jQuery event object.

* (b) Returning false from a regular JavaScript onclick event handler for an anchor tag prevents the browser from navigating to the link address and stops the event from propagating through the DOM.

* (c) Returning false from a regular JavaScript onclick event handler for a non-anchor tag (e.g., a div, button, etc.) has absolutely no effect.

<br>

### Explain the difference between the .detach() and .remove() methods in jQuery.

The `.detach()` and `.remove()` methods are the same, except that `.detach()` retains all jQuery data associated with the removed elements and `.remove()` does not. `.detach()` is therefore useful when removed elements may need to be reinserted into the DOM at a later time.


<br>

### What’s the difference between `document.ready()` and `window.onload()`?

The `document.ready()` event occurs when all HTML documents have been loaded, but `window.onload()` occurs when all content (including images) has been loaded. So generally the `document.ready()` event fires first.

<br>

### What’s the difference between prop() and attr()?
Both `prop()` and `attr()` are used to get or set the value of the specified property of an element attribute, but `attr()` returns the default value of a property whereas `prop()` returns the current value.




