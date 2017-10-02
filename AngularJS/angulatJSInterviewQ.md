
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

```java<directive-name="title2"></directive-name>```

This can be achieved by specifying a name behind the above mentioned option in the scope definition:

```js
scope: {
    title: '@directiveName'
}
```

### 2. How do you share data between controllers?
Create an AngularJS service that will hold the data and inject it inside of the controllers.

Using a service is the cleanest, fastest and easiest way to test. However, there are couple of other ways to implement data sharing between controllers, like:

* Using _events_
* Using _$parent, nextSibling, controllerAs_, etc. to directly access the controllers
* Using the _$rootScope_ to add the data on (not a good practice)

The methods above are all correct, but are not the most efficient and easy to test.

### 3. What is a digest cycle in AngularJS?
In each digest cycle Angular compares the old and the new version of the scope model values. The digest cycle is triggered automatically. We can also use $apply() if we want to trigger the digest cycle manually.

### 4. Where should we implement the DOM manipulation in AngularJS?
In the directives. DOM Manipulations should not exist in controllers, services or anywhere else but in directives.

### 5. If you were to migrate from Angular 1.4 to Angular 1.5, what is the main thing that would need refactoring?
Changing .directive to .component to adapt to the new Angular 1.5 components

### 6. How would you specify that a scope variable should have one-time binding only?
By using “::” in front of it. This allows you to check if the candidate is aware of the available variable bindings in AngularJS.

### 7. What is the difference between one-way binding and two-way binding?
* One way binding implies that the scope variable in the html will be set to the first value its model is bound to (i.e. assigned to)
* Two way binding implies that the scope variable will change it’s value everytime its model is assigned to a different value

### 8. Explain how $scope.$apply() works
$scope.$apply re-evaluates all the declared ng-models and applies the change to any that have been altered (i.e. assigned to a new value) 
Explanation: **scope.scope.apply()** is one of the core angular functions that should never be used explicitly, it forces the angular engine to run on all the watched variables and all external variables and apply the changes on their values

### 9. What makes the angular.copy() method so powerful?
It creates a deep copy of the variable.

A deep copy of a variable means it doesn’t point to the same memory reference as that variable. Usually assigning one variable to another creates a “shallow copy”, which makes the two variables point to the same memory reference. Therefore if one is changed, the other changes as well.

### 10. How would you make an Angular service return a promise? Write a code snippet as an example?
To add promise functionality to a service, we inject the “$q” dependency in the service, and then use it like so:

```js
angular.factory('testService', function($q) {
  return {
    getName: function() {
      var deferred = $q.defer();

      //API call here that returns data
      testAPI.getName().then(function(name) {
        deferred.resolve(name);
      });

      return deferred.promise;
    }
  };
});
```

The $q library is a helper provider that implements promises and deferred objects to enable asynchronous functionality.

### 11. What is the role of services in AngularJS and name any services made available by default?
AngularJS Services are objects that provide separation of concerns to an AngularJS app. These can be created using a factory method or a service method. Services are singleton components and all components of the application (into which the service is injected) will work with single instance of the service. An AngularJS service allows developing of business logic without depending on the View logic which will work with it.

Few of the inbuilt services in AngularJS are:

* **the $http service:** The $http service is a core Angular service that facilitates communication with the remote HTTP servers via the browser’s XMLHttpRequest object or via JSONP
* **the $log service:** Simple service for logging. Default implementation safely writes the message into the browser’s console
* **the $anchorScroll:** it scrolls to the element related to the specified hash or (if omitted) to the current value of $location.hash() Why should one know about AngularJS Services, you may ask. Well, understanding the purpose of AngularJS Services helps bring modularity to AngularJS code
Services are the best may to evolve reusable API within and AngularJS app.

Overview:

* AngularJS Services help create reusable components.
* A Service can be created either using the service() method or the factory() method.
* A typical service can be injected into another service or into an AngularJS Controller.

### 12. How do you reset a $timeout, $interval(), and disable a $watch()?
To reset a timeout and/or $interval, assign the result of the function to a variable and then call the .cancel() function:

```js
var customTimeout = $timeout(function() {
  // arbitrary code
}, 55);

$timeout.cancel(customTimeout);
```

To disable $watch(), we call its deregistration function. $watch() then returns a deregistration function that we store to a variable and that will be called for cleanup:

```js
var deregisterWatchFn = $scope.$on('$destroy', function() {
  // we invoke that deregistration function, to disable the watch
  deregisterWatchFn();
});
```

### 13. What is DDO Directive Definition Object?
“DDO is an object used while creating a custome directive. A standard DDO object has following parameters.

```js
var directiveDefinitionObject = {
  priority: 0,
  template: '<div></div>', // or // function(tElement, tAttrs) { ... },
  // or
  // templateUrl: 'directive.html', // or // function(tElement, tAttrs) { ... },
  transclude: false,
  restrict: 'A',
  templateNamespace: 'html',
  scope: false,
  controller: function(
    $scope,
    $element,
    $attrs,
    $transclude,
    otherInjectables
  ) { ... },
  controllerAs: 'stringIdentifier',
  bindToController: false,
  require: 'siblingDirectiveName', // or // ['^parentDirectiveName', '?optionalDirectiveName', '?^optionalParent'],
  compile: function compile(tElement, tAttrs, transclude) {
    return {
      pre: function preLink(scope, iElement, iAttrs, controller) { ... },
      post: function postLink(scope, iElement, iAttrs, controller) { ... }
    };
    // or
    // return function postLink( ... ) { ... }
  }
  // or
  // link: {
  //  pre: function preLink(scope, iElement, iAttrs, controller) { ... },
  //  post: function postLink(scope, iElement, iAttrs, controller) { ... }
  // }
  // or
  // link: function postLink( ... ) { ... }
};
```

### 14. What is a singleton pattern and where we can find it in Angularjs?
Is a great pattern that restricts the use of a class more than once. We can find singleton pattern in angular in dependency injection and in the services.

In a sense, if the candidate does 2 times ‘new Object()‘ without this pattern, the candidate will be alocating 2 pieces of memory for the same object. With singleton pattern, if the object exists, it'll be reused.

### 15. What is an interceptor? What are common uses of it?
An interceptor is a middleware code where all the _http_ requests go through.

The interceptor is a factory that are registered in _$httpProvider_. There are 2 types of requests that go through the interceptor, request and response (with _requestError_ and _responseError_ respectively). This piece of code is very useful for error handling, authentication or middleware in all the requests/responses.

### 16. How would you programatically change or adapt the template of a directive before it is executed and transformed?
The candidate should use the compile function. The compile function gives access to the directive’s template before transclusion occurs and templates are transformed, so changes can safely be made to DOM elements. This is very useful for cases where the DOM needs to be constructed based on runtime directive parameters.

### 17. How would you implement application-wide exception handling in your Angular app?
Angular has a built-in error handler service called **_$exceptionHandler_** which can easily be overriden as seen below:

```js
myApp.factory('$exceptionHandler', function($log, ErrorService) {
  return function(exception, cause) {
    if (console) {
      $log.error(exception);
      $log.error(cause);
    }

    ErrorService.send(exception, cause);
  };
});
```

This is very useful for sending errors to third party error logging services or helpdesk applications. Errors trapped inside of event callbacks are not propagated to this handler, but can manually be relayed to this handler by calling $exceptionHandler(e) from within a try catch block.

### 18. How would you react on model changes to trigger some further action? For instance, say you have an input text field called email and you want to trigger or execute some code as soon as a user starts to type in their email.
This can be achieved by using **_$watch_** function in the controller.

```js
function MyCtrl($scope) {
  $scope.email = '';

  $scope.$watch('email', function(newValue, oldValue) {
    if ($scope.email.length > 0) {
      console.log('User has started writing into email');
    }
  });
}
```



































