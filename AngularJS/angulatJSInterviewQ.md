
### 1. How can you can pass arguments to your custom directive as you do with the builtin Angular-directives - by specifying an attribute on the directive-element:

```js
angular.element(document.getElementById('wrapper')).append('<directive-name title="title2"></directive-name>');
```

What you need to do is define the scope (including the argument(s)/parameter(s)) in the factory function of your directive. In below example the directive takes a title-parameter. You can then use it, for example in the template, using the regular Angular-way: {{title}}

```js
app.directive('directiveName', function(){
   return {
      restrict:'E',
      scope: {
         title: '@'
      },
      template:'<div class="title"><h2>{{title}}</h2></div>'
   };
});
```

Depending on how/what you want to bind, you have different options:

* **=** is two-way binding
* **@** simply reads the value (one-way binding)
* **&** is used to bind functions

In some cases you may want use an "external" name which differs from the "internal" name. With external I mean the attribute name on the directive-element and with internal I mean the name of the variable which is used within the directive's scope.

For example if we look at above directive, you might not want to specify another, additional attribute for the title, even though you internally want to work with a title-property. Instead you want to use your directive as follows:

```java
<directive-name="title2"></directive-name>
```

This can be achieved by specifying a name behind the above mentioned option in the scope definition:

```js
scope: {
    title: '@directiveName'
}
```

### 2. How do you share data between controllers?

Create an AngularJS service that will hold the data and inject it inside of the controllers.

Using a service is the cleanest, fastest and easiest way to test. However, there are couple of other ways to implement data sharing between controllers, like:

* Using <p style="color:red;">events</p>
* [events](https://placehold.it/15/f03c15/000000?text=+) `#f03c15`
* Using <span style="color:red;">$parent, nextSibling, controllerAs</span>, etc. to directly access the controllers
* Using the <span style="color:red;">$rootScope</span> to add the data on (not a good practice)

The methods above are all correct, but are not the most efficient and easy to test.













