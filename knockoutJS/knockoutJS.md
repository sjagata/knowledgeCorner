


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

> The foreach binding was not bound to an HTML tag; instead, it is placed inside HTML comments. I find this quite convenient when using a foreach binding because it avoids an unnecessary element to wrap the HTML that I want repeated for each element in the array.
