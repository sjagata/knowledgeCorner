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

### What is the use of Drag and Drop in HTML5?
Drag and drop is a very common feature and convenient to users. Simply, you need to grab an object and put it at the place you want. This feature is commonly used by many of the online examination websites wherein you have the options to pick up the correct answer, drag it to the answers place holder and drop it.

The Drag and Drop API comes with seven new events to track a drag and drop. The events are dragstart, drag, dragend, dragenter, dragleave, dragover and drop that are triggered during the various stages of the drag and drop operation. These events are listed below: 

* dragstart : triggered when dragging a draggable element.
* drag : triggered when draggable element is moved.
* dragend: triggered when drag and drop ends.
* dragenter: triggered when the dragglable element is dragged over the target element
* dragleave: triggered when the user's cursor leaves the target element while dragging
* dragover: triggered when a draggable object is moved inside an element
* drop: triggered when a draggle object is dropped


* Elements that are dragged during Drag and Drop can trigger three events. These events are dragstart, drag, dragend. 
* Elements in which we drop the draggable elements can trigger four events. These events are dragenter, dragleave, dragover and drop.

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
6. In SVG, each drawn shape is remembered as an object.

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
5. Resolution dependent.
6. Canvas is rendered pixel by pixel.

<br>
<br>

### In HTML5 you can use many APIs. Some of them are: 
* Web Workers API
* Server-sent Events API
* WebSocket API
* Cross-document Messaging API
* Drawing
* Audio/Video
* Drag and drop
* Autofocus
* Editable
* Client-side storage
* Geolocation

<br>
<br>

### What is Vibration API in HTML5?
Vibration is a simple, a nice way of alert when you get a new message or a phone call. It is especially useful when you are in a noisy environment or the place where you feel the ringing would be a distraction to others.

<br>
<br>

### What is the use of Geolocation API of HTML5?
The Geolocation API of HTML5 helps to identify the user’s location. It can be used to provide location-specific information. For privacy reasons, the user is asked for permission to report location information. The HTML 5 Geolocation API provides the geographical location of the user. There are many techniques used to identify the location of the user. A desktop browser generally uses WiFi or IP based positioning techniques whereas a mobile browser uses cell triangulation, GPS and A-GPS (Assistive GPS) to triangulate between mobile phone towers and public masts to determine the location and WiFi based positioning techniques and so on. 

The Geolocation API will use any of these techniques to identify the user’s location. The Geolocation API protects the user’s privacy by mandating that the user permission should be sought and obtained before sending the location information of the user to any website. Hence, the user will be prompted with a popover or dialog requesting for the user’s permission to share the location information. The user can accept or deny the request.

#### Geolocation Object
The Geolocation API is published through the navigator.geolocation object. If this object is present then the geolocation service works. 
```js
var geolocation=navigator.geolocation;
```
The geolocation object is a service object that allows widgets to retrieve information about the geographic location of the device.

<br>
<br>

### What is a meter tag? What is the difference between progress tag and a meter tag?
The meter tag is used to represent a scalar measurement within a known range. The value can be fractional. 

Examples: 
Disk uses, the relevance of a query result, the fraction of a voting population to have selected a specific candidate.

#### Difference between progress tag and meter tag
A progress tag represents the completion progress of a task whereas the meter tag is used to represent gauges. We can think that a progress tag represents a dynamic data whereas a meter tag represents a static data. 

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

### Which JavaScript objects are not accessible to web worker?
Following JavaScript objects are not accessible to web worker:

1. The window object
2. The document object
3. The parent object

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

HTML5 Web Storage, also known as DOM Storage is a way to preserve state on either the client or server which makes it much easier to work against the stateless nature of HTTP.

#### Advantages of HTML5 Web Storage:
1. It can store 5 to 10 MB data. That is far more than what cookies have.
2. Web storage data is never transferred with HTTP request, so it increases the performance of the application.
Web Storage Strengths and Weaknesses

#### Strengths
* Apps can work both online and offline.
* API is easy to learn and use.
* Has the ability to hook in to the browser events such as offline, online and storage change.
* Has less overhead than cookies; no extra header data is sent with the browser requests.
* Provides more space than what cookies offer so increasingly complex information can be kept.

#### Weaknesses
* Data is stored as a simple string; manipulation is needed to store objects of different types such as Booleans, Objects, Ints and Floats.
* It has a default 5MB limit; more storage can be allowed by the user, if required.
* It can be disabled by the user or systems administrator.
* Storage can be slow with the complex sets of data.

#### HTML5 Web Storage Methods
* **setItem(key,value):** Adds a key/value pair to the sessionStorage object.
* **getItem(key):** Retrieves the value for a given key.
* **clear():** Removes all key/value pairs for the sessionStorage object.
* **removeItem(key):** Removes a key/value pair from the sessionStorage object.
* **key(n):** Retrieves the value for a key.

<br>
<br>

### What are the types of Web Storage in HTML5?
There are two types of Web Storage,

1. Session Storage
As its name implies, it stores data of current session only which means the data stored in session storage clears when the browser is closed.

2. Local Storage
Local Storage is a second type of HTML Web Storage. Like Session Storage, it also stores data in KEY / VALUE pair of strings. The following points helps to compare Session Storage and Local Storage.

* Session Storage stores the data for only current session of the browser, when the browser closes data in, Session Storage clears. On the other hand, the data stored in Local Storage is not deleted automatically when the current browser window is closed. Data in Local Storage clears only when it is manually deleted.

* The data in Session Storage is accessible only in current window of the browser but the data in the Local Storage can be shared between multiple windows of the browser.

* We can only store strings in Local Storage. To save objects in Local Storage, first convert the object into JSON string and then store this string in Local Storage as shown below:
```js
localStorage.setItem (‘object’, JSON.stringify(object));
```

<br>
<br>

### What is the difference between local storage and cookies?
#### 	Cookies
* Client side / Server side: Data accessible both at client side and server side. Cookie data is sent to the server side with every request.
* Size: 4095 bytes per cookie.
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

There are three sections of a Manifest file:
1. **CACHE MANIFEST** - Files listed here are cached after they are downloaded for the first time.
2. **NETWORK** - Files listed here require a connection to the server, and are never cached.
3. **FALLBACK** - Files listed here specify fallback pages if a page is inaccessible.

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

<br>
<br>

### What is the Geolocation API in HTML5?
HTML5’s Geolocation API lets users share their physical location with chosen web sites. JavaScript can capture a user’s latitude and longitude and can send it to the back-end web server to enable location-aware features like finding local businesses or showing their location on a map.

Today, most browsers and mobile devices support the Geolocation API. The Geolocation API works with a new property of the global `navigator` object.

A Geolocation object can be created as follows:
```js
var geolocation = navigator.geolocation;
```

The `geolocation` object is a service object that allows widgets to retrieve information about the geographic location of the user’s device.

<br>
<br>

### What is the use of WebSocket API?
WebSockets provide a rich protocol to perform **bi-directional communication** and we can create a full-duplex communication channel that can be operated through a single socket over the Web and for that reason its more attractive for the things like games, messaging apps and for real-time updates in both directions.

WebSocket is basically used to reduce the overhead of HTTP, since it has its own protocol defined by IETF and an API for the server communication. By using them, the client notifies the WebSocket server with the recipients ID of an event and the server immediately notifies all the active clients and the last clients processes the event when the given recipient ID matches the client ID.










