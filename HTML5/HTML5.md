### What is the relationship between SGML,HTML , XML and XHTML?
SGML (Standard generalized markup language) is a standard which tells how to specify document markup. It’s only a Meta language which describes how a document markup should be. HTML is a markup language which is described using SGML.

So by SGML they created DTD which the HTML refers and needs to adhere to the same. So you will always find “DOCTYPE” attribute at the top of HTML page which defines which DTD is used for parsing purpose.

```html
<!--!doctype-->
```

Now parsing SGML was a pain so they created XML to make things better. XML uses SGML. For example in SGML you have to start and end tags but in XML you can have closing tags which close automatically (“”).

XHTML was created from XML which was used in HTML 4.0. So for example in SGML derived HTML “
” is not valid but in XHTML it’s valid. You can refer XML DTD as shown in the below code snippet.

```html
<!--!doctype--><!--!doctype-->
```

<br>
<br>

### What is HTML 5?
HTML 5 is a new standard for HTML whose main target is to deliver everything without need to any additional plugins like flash, Silverlight etc. It has everything from animations, videos, rich GUI etc.
HTML5 is cooperation output between World Wide Web Consortium (W3C) and the Web Hypertext Application Technology Working Group (WHATWG).

<br>
<br>

### If I do not put <! DOCTYPE html> will HTML 5 work?
No, browser will not be able to identify that it’s a HTML document and HTML 5 tags will not function properly.

<br>
<br>

### HTML 5 elements
* `<header>`: Represents header data of HTML.
* `<footer>`: Footer section of the page.
* `<nav>`: Navigation elements in the page.
* `<article>`: Self-contained content.
* `<section>`: Used inside article to define sections or group content in to sections.
* `<aside>`: Represent side bar contents of a page.

<br>
<br>

### What is datalist in HTML 5?
Datalist element in HTML 5 helps to provide autocomplete feature in a textbox as shown below.
```html
<input list="Country">
<datalist id="Country">
  <option value="India">
  <option value="Italy">
  <option value="Iran">
  <option value="Israel">
  <option value="Indonesia">
</datalist>
```

<br>
<br>

### What are the different new form element types in HTML 5?
There are 10 important new form elements introduced in HTML 5:-
1. Color - If you want to show color picker dialog box.
2. Date - If you want to show calendar dialog box.
3. Datetime-local - If you want to show calendar with local time.
4. Email - If you want to create a HTML text with email validation we can set the type as “email”.
5. Time
6. Url - For URL validation set the type as “url” as shown in the below HTML code.
7. Range - If you want to display a range control you can use type as range.
8. Telephone - If you want to make text box to accept telephone numbers.
9. Number - If you want to display textbox with number range you can set type to number.
10. Search - Want to make text box as search engine box.

<br>
<br>

### What is SVG?
SVG stands for scalable vector graphics. It’s a text based graphic language which draws images using text, lines, dots etc. This makes it lightweight and renders faster.
```html
<svg id="svgelem" height="[object SVGAnimatedLength]" xmlns="http://www.w3.org/2000/svg">
<line style="stroke: rgb(255, 0, 0); stroke-width: 2px;" y2="[object SVGAnimatedLength]" x2="[object SVGAnimatedLength]" y1="[object SVGAnimatedLength]" x1="[object SVGAnimatedLength]">
</line>
```
1. Here’s it’s like draw and remember. In other words any shape drawn by using SVG can be remembered and manipulated and browser can render it again.
2. SVG is good for creating graphics like CAD software’s where once something is drawn the user wants to manipulate it.
3. This is slow as it needs to remember the co-ordinates for later manipulations.
4. We can have event handler associated with the drawing object.
5. Resolution independent.

### What is canvas in HTML 5?
Canvas is an HTML area on which you can draw graphics.
* Define the Canvas area.
```html
<canvas height=""500"" id=""mycanvas"" solid="" style=""border:1px" width=""600""></canvas>  
```
* Get access to canvas context area.
```js
var c=document.getElementById("mycanvas");
var ctx=c.getContext("2d"); 
```
* Draw the graphic.
```html
<a name="WhatisthedifferencebetweenCanvasandSVGgraphics">What is the difference between Canvas and SVG graphics? </a>
```
1. Canvas is like draw and forget. Once something is drawn you cannot access that pixel and manipulate it.
2. Canvas is good for draw and forget scenarios like animation and games.
3. This is faster as there is no intention of remembering things later.
4. Here we cannot associate event handlers with drawing objects as we do not have reference of them.
5. 	Resolution dependent.

<br>
<br>

### What are web workers and why do we need them ?
Consider the below heavy for loop code which runs above million times.
```js
function  SomeHeavyFunction(){
  for (i = 0; i < 10000000000000; i++){
    x = i + x;
  }
} 
```
Let’s say the above for loop code is executed on a HTML button click. Now this method execution is synchronous. In other words the complete browser will wait until the for loop completes.
```html
<input type="button" onclick="SomeHeavyFunction();" /> 
```
This can further lead to browser getting freezed and unresponsive with an error message.

So if we can move this heavy for loop in a JavaScript file and run it asynchronously that means the browser does need to wait for the loop then we can have a more responsive browser. That’s what web worker are for.

**Web worker** helps to execute JavaScript file asynchronously.

<br>
<br>

### What is local storage concept in HTML 5?
Many times we would like to store information about the user locally in the computer. For example let’s say user has half-filled a long form and suddenly the internet connection breaks off. So the user would like you to store this information locally and when the internet comes back.He would like to get that information and send it to the server for storage.

Modern browsers have storage called as **Local storage** in which you can store this information.

<br>
<br>

### How can we add and remove data from local storage?
Data is added to local storage using “key” and “value”. Below sample code shows country data “India” added with key value “Key001”.
```js
localStorage.setItem("Key001","India");

// You can also store JavaScript object’s in the local storage using the below code.
var country = {};
country.name = "India";
country.code = "I001";
localStorage.setItem("I001", country);
var country1 = localStorage.getItem("I001"); 

// If you want to store in JSON format you can use “JSON.stringify” function as shown in the below code.
localStorage.setItem("I001",JSON.stringify(country)); 
```

<br>
<br>

### What is the lifetime of local storage?
Local storage does not have a life time it will stay until either the user clear it from the browser or you remove it using JavaScript code.

<br>
<br>

### What is the difference between local storage and cookies?
#### 	Cookies
* Client side / Server side: Data accessible both at client side and server side. Cookie data is sent to the server side with every request.
* Size: 4095 bytes per cookie.	5 MB per domain.
* Expiration:	Cookies have expiration attached to it. So after that expiration the cookie and the cookie data get’s deleted.

#### 	Local storage
* Client side / Server side: Data is accessible only at the local browser side. Server cannot access local storage until deliberately sent to the server via POST or GET.
* Size: 5 MB per domain.
* Expiration: There is no expiration data. Either the end user needs to delete it from the browser or programmatically using JavaScript we need to remove the same.

#### What is session storage and how can you create one?
Session storage is same like local storage but the data is valid for a session. In simple words the data is deleted as soon as you close the browser. To create a session storage you need to use
* Local storage data persists forever but session storage is valid until the browser is open, as soon as the browser closes the session variable resets.

<br>
<br>

### What is WebSQL?
WebSQL is a structured relational database at the client browser side. It’s a local RDBMS inside the browser on which you can fire SQL queries.

### Is WebSQL a part of HTML 5 specification?
No, many people label it as HTML 5 but it’s not part of HTML 5 specification. The specification is based around SQLite.

### So how can we use WebSQL?
* The first step we need to do is open the database by using “OpenDatabase” function as shown below. The first argument is the name of the database, the next is the version, then a simple textual title and finally the size of the database.
```js
var db = openDatabase('dbCustomer','1.0','Customer app’, 2 * 1024 * 1024);
```
* To execute SQL we then need to use “transaction” function and call “executeSql” function to fire SQL.
```js
db.transaction(function (tx) {
  tx.executeSql('CREATE TABLE IF NOT EXISTS tblCust(id unique, customername)');
  tx.executeSql('INSERT INTO tblcust (id, customername) VALUES(1, "shiv")');
  tx.executeSql('INSERT INTO tblcust (id, customername) VALUES (2, "raju")');
} 
```

<br>
<br>

### What is application cache in HTML5?
HTML5 introduces application cache, which means that a web application is cached, and accessible without an internet connection.

Application cache gives an application three advantages:

1. Offline browsing - users can use the application when they're offline
2. Speed - cached resources load faster
3. Reduced server load - the browser will only download updated/changed resources from the server

* The manifest attribute should be included on every page of your web application that you want cached.
* The manifest file is a simple text file that lists the resources the browser should cache for offline access.
```html
<!DOCTYPE HTML>
<html manifest="demo.appcache">
  <head>
    <title>Title of the document</title>
  </head>

  <body>
   The content of the document......
  </body>

</html>
```














