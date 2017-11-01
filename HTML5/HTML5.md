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
* <header>: Represents header data of HTML.
* <footer>: Footer section of the page.
* <nav>: Navigation elements in the page.
* <article>: Self-contained content.
* <section>: Used inside article to define sections or group content in to sections.
* <aside>: Represent side bar contents of a page.

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



































