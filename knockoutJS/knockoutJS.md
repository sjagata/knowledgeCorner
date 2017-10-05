
[reference](https://github.com/oreillymedia/knockout_js)

<br>

### Knockout offers several useful variables that allow you to navigate between the context you are in to a parent or even the root context:

* **$root** - This accesses the root context (the ViewModel bound to Knockout) in any child context. This is handy when you are unsure of how many parent/child contexts are above
the one you are currently in.
* **$parent** - When you are in a child context, this will access the current context’s direct parent.
* **$parents** - This is similar to the $parent variable except that it contains an array of parent contexts to the context you are currently in. $parents[0] is the same as $parent. Similarly,
using $parents[$parents.length - 1] is the same as using $root.
* **$data** - This provides access to the current object your context is in. This is quite useful when you are in a context that is a variable and contains no properties.
* **$index** - This is only available within the foreach binding and contains an integer that represents the current position of the loop starting at 0 and going to length –1.

### foreach Binding:

```html
<!DOCTYPE html>
<html>

<head>
	<title>Data Binding with KnockoutJS</title>
</head>

<body>

	<ul>
		<!-- ko foreach: books -->
		<li data-bind="text: $data"></li>
		<!-- /ko -->
	</ul>

	<script type='text/javascript' src='js/knockout-3.2.0.js'></script>
	<script>
		var viewModel = function () {
			var self = this;

			self.books = [
				'Rapid Application Development With CakePHP',
				'20 Recipes for Programming MVC 3: Faster, Smarter Web Development',
				'20 Recipes for Programming PhoneGap: Cross-Platform Mobile Development for Android and iPhone'
			];
		};

		ko.applyBindings(viewModel);
	</script>
</body>

</html>
```

> The **foreach binding was not bound to an HTML tag; instead, it is placed inside HTML comments.** I find this quite convenient when using a foreach binding because it avoids an unnecessary element to wrap the HTML that I want repeated for each element in the array.

### foreach Callbacks (Events)
The foreach binding contains several callback methods that can be executed by Knockout after certain events happen:
* **afterRender**
This is called when the foreach first finishes initializing and every time an element is added to the array.
* **afterAdd**
This is called every time an element is added to the array. Unlike afterRender, this is not called when the array is first initialized.
* **beforeRemove** 
This is called when an item is removed from the array. This is often used to animate a removal of an item.
* **beforeMove**
This is called when an item is moved within the array. It’s another great opportunity to begin an animation or add an effect to the element being interacted with.
* **afterMove**
This is called after the item is moved within the array. Much like the beforeMove, this would be the opportunity to finish any effects on the moved element.

```html
<!DOCTYPE html>
<html>
<head>
	<title>Data Binding with KnockoutJS</title>
</head>
<body>
	
	<table>
	<thead>
		<tr>
			<th>Thumbnail</th>
			<th>Title</th>
			<th>ISBN</th>
			<th>Published</th>
		</tr>
	</thead>
	<tbody data-bind="foreach: { data: books, afterRender: loadImage }">
		<tr>
			<td><img src="images/loading.gif" data-bind="attr { id: 'image_' + isbn }" /></td>
			<td data-bind="text: title"></td>
			<td data-bind="text: isbn"></td>
			<td data-bind="text: $parent.formatDate(publishedDate)"></td>
		</tr>
	</tbody>
	</table>
	
	<script type='text/javascript' src='js/jquery.js'></script>
	<script type='text/javascript' src='js/knockout-3.2.0.js'></script>
	<script>
		function ViewModel() {
			var self = this;
			
			self.books = [
				{
					title: 'Rapid Application Development With CakePHP',
					isbn: '1460954394',
					publishedDate: '2011-02-17',
					image: 'http://ecx.images-amazon.com/images/I/41JC54HEroL._AA160_.jpg'
				},
				{
					title: '20 Recipes for Programming MVC 3: Faster, Smarter Web Development', 
					isbn: '1449309860',
					publishedDate: '2011-10-14',
					image: 'http://ecx.images-amazon.com/images/I/51LpqnDq8-L._AA160_.jpg'
				},
				{
					title: '20 Recipes for Programming PhoneGap: Cross-Platform Mobile Development for Android and iPhone', 
					isbn: '1449319548',
					publishedDate: '2012-04-06',
					image: 'http://ecx.images-amazon.com/images/I/51AkFkNeUxL._AA160_.jpg'
				}
			];
			
			self.loadImage = function(element, index, data) {
				$('#image_' + index.isbn).attr('src', index.image);
			};
			
			self.formatDate = function(dateToFormat) {
				var months = new Array("January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December");

				var d = new Date(dateToFormat);
				
				return months[d.getMonth()] + ' ' + d.getDate() + ', ' + d.getFullYear();
			};
		};
		
		var viewModel = new ViewModel();
		ko.applyBindings(viewModel);
	</script>
</body>
</html>
```

> `foreach` data binding has been changed to include the `afterRender` callback. It will call the function `loadImage`.

### with Binding
The with binding is similar to the foreach binding in that it creates a new child context. Everything within the binding is now relative to the variable to which it is bound. The major difference between the two is that with is a single object with multiple properties, whereas the foreach repeats the HTML in the binding.

```html
<!DOCTYPE html>
<html>
<head>
	<title>Data Binding with KnockoutJS</title>
</head>
<body>
	
	<div id="book" data-bind="with: book">
		<h1 data-bind="text: title"></h1>
		<h2>Published on <span data-bind="text: $parent.formatDate(publishedDate)"></span></h2>
		<p data-bind="text: synposis"></p>
	</div>
	
	<div id="book">
		<h1 data-bind="text: book.title"></h1>
		<h2>Published on <span data-bind="text: formatDate(book.publishedDate)">
		</span></h2>
		<p data-bind="text: book.synposis"></p>
	</div>
	
	<script type='text/javascript' src='js/knockout-3.2.0.js'></script>
	<script>
		function ViewModel(book) {
			var self = this;
			
			self.book = book;
			
			self.formatDate = function(dateToFormat) {
				var months = new Array("January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December");

				var d = new Date(dateToFormat);
				
				return months[d.getMonth()] + ' ' + d.getDate() + ', ' + d.getFullYear();
			};
		};
		
		var book = {
			title: 'Rapid Application Development With CakePHP',
			synposis: '...',
			isbn: '1460954394',
			publishedDate: '2011-02-17'
		};
		
		var viewModel = new ViewModel(book);
		ko.applyBindings(viewModel);
	</script>
</body>
</html>
```

> When the with binding is not used, notice how the HTML elements are data-bound
using the full variable path (e.g., book.title). The other difference is that the format
Date function no longer needs to be prefixed with $parent because a child context
was not created, and it is still in the root context.

### Defining an Observable
There are three different types of observables that are most commonly used.

#### first type

```js
var myObservable = ko.observable();
myObservable('Hello');
alert(myObservable());
```

> To create an observable, assign the `ko.observable` function to the variable. A default
value can be specified in the constructor of the call. Knockout then converts your
variable into a function and tracks when the value changes, in order to notify the UI
elements associated with the variable.

**Accessing an Observable**
After an observable is defined, it needs to be called like a function
in order to get or set its value. If you try setting it directly as if it
were a variable, the observable would be destroyed.

#### second type
Just like observable variables, when elements are added or removed from the array, Knockout notifies elements that are subscribed to the notifications.

An observable array is great for use with tables where elements are being dynamically added and removed.

```js
var myObservableArray = ko.observableArray([]);
myObservableArray.push('Hello');
// the array is instantiated as an empty array by passing two square brackets in the constructor.
```

#### third type
The final type of observable, as shown in Example below, is a **_computed observable._** This is slightly different than the previous two types in that a computed observable is commonly used to combine one or more observables into a single object.

```js
self.firstName = ko.observable('Steve');
self.lastName = ko.observable('Kennedy');

self.fullName = ko.computed(function() {
	return 'Hello ' + self.firstName() + ' ' + self.lastName();
});
```

Once the ViewModel is bound to Knockout, the computed function is executed. For
each observable that is used within that function, it subscribes to any change events to
that variable. When it changes, Knockout knows that the computed variable should
be updated.


### pureComputed Observables
As of Knockout version 3.2, a new type of observable called **_pureComputed observable_** was introduced.
It is quite similar to the computed observable with several performance and memory improvements. The name is borrowed from the **Pure function** programming term.

```js
self.firstName = ko.observable('Steve');
self.lastName = ko.observable('Kennedy');

self.fullName = ko.pureComputed(function() {
	return 'Hello ' + self.firstName() + ' ' + self.lastName();
});
```

> The observables are treated differently because when there are no elements listening
for changes to the computed variable, they are placed in `sleeping mode` versus `listening
mode`. While in `sleeping mode`, Knockout disposes all dependencies and reevaluates
the content when it is read—unlike `listening mode`, which manages
references to all subscribers and ensures the value is up-to-date prior to first access.

The previous example follows both rules for being a pure function:
* Given the same input, it will output the same result.
* No side effects occur because of the function executed.

The second rule is probably the most important when deciding whether to use a computed or a pureComputed observable with Knockout. **Within your observable, if you need to execute other code, then you should use a `computed observable` to ensure it is in listening mode instead of sleeping mode.**

### Showing and Hiding Elements

```js
<!DOCTYPE html>
<html>
<head>
	<title>Data Binding with KnockoutJS</title>
</head>
<body>
	
	<button type="button" data-bind="click: updateObservable">Click me</button>
	
	<div data-bind="visible: showExtraData" style="display: none">
		Now you see me!
	</div>
	
	<script type='text/javascript' src='js/knockout-3.2.0.js'></script>
	<script>
		function ViewModel() {
			var self = this;
			
			self.showExtraData = ko.observable(false);
			
			self.updateObservable = function() {
				self.showExtraData(!self.showExtraData());
			};
		};
		
		var viewModel = new ViewModel();
		ko.applyBindings(viewModel);
	</script>
</body>
</html>
```

Pervious example combines the use of an observable variable with a new data binding called `visible`. The `visible` data binding sets the CSS property display to either block or none depending on the results of the condition used in the binding.

### Adding and Removing Elements
The `if` and `ifnot` data bindings are quite similar to the previous `visible` data binding.
The difference between the two is that, unlike the `visible` binding setting a CSS
style to show or hide the element, `if` and `ifnot` physically add or remove the elements
from the Document Object Model (DOM).

```html
<!DOCTYPE html>
<html>
<head>
	<title>Data Binding with KnockoutJS</title>
</head>
<body>
	
	<button type="button" data-bind="click: updateObservable">Click me</button>
	
	<!-- ko if: showExtraData -->
	<div>
		Now you see me!
	</div>
	<!-- /ko -->
	
	<script type='text/javascript' src='js/knockout-3.2.0.js'></script>
	<script>
		function ViewModel() {
			var self = this;
			
			self.showExtraData = ko.observable(false);
			
			self.updateObservable = function() {
				self.showExtraData(!self.showExtraData());
			};
		};
		
		var viewModel = new ViewModel();
		ko.applyBindings(viewModel);
	</script>
</body>
</html>
```

> HTML to be dynamically inserted into the DOM.

**Adding and Removing from the DOM**
If an element is being added to the DOM because of a user interaction
that had one or more JavaScript side effects performed on it
during the original page load, these would need to be executed
after adding them back to the DOM.
For example, if you have a field that is linked to a jQuery date
picker, JavaScript is required to initialize it. This needs to be executed
after the element is added to the DOM.
In a scenario like this, it might be more prudent to use the visible
data binding because the elements will remain in the DOM and can
be initialized upon the document load.





















