
[mvvm explained](https://msdn.microsoft.com/en-us/library/hh848246.aspx)
	
![alt text][mvc]

[mvc]: https://github.com/SandeepJagatha/knowledgeCorner/blob/master/AngularJS/images/digestprocess.png "digestprocess"

<br>
<br>

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

```js
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

### 19. What is a Factory method in AngularJS?
AngularJS Factory: the purpose of Factory is also the same as Service, however in this case we create a new object and add functions as properties of this object and at the end we return this object.

```js
  app.service('myService', function() {

  // service is just a constructor function
  // that will be called with 'new'

  this.sayHello = function(name) {
     return "Hi " + name + "!";
  };
});

app.factory('myFactory', function() {

  // factory returns an object
  // you can run some code before

  return {
    sayHello : function(name) {
      return "Hi " + name + "!";
    }
  }
});
```

When to use Factory: It is just a collection of functions like a class. Hence, it can be instantiated in different controllers when you are using it with a constructor function.



### 20. What are the services in AngularJS?
Services are one of the most important concepts in AngularJS. In general services are functions that are responsible for specific tasks in an application. AngularJS services are designed based on two principles.

**1. instantiated**
Angular only instantiates a service when an application component depends on it using dependency injection for making the Angular codes robust and less error prone.

**2. Singletons**
Each component is dependent on a service that gets a reference to the single instance generated by the service factory.

AngularJS provides many built in services, for example, $http, $route, $window, $location and so on. Each service is responsible for a specific task, for example, $http is used to make an Ajax call to get the server data. $route defines the routing information and so on. Builtin services are always prefixed with the $ symbol.

#### AngularJS internal services

AngularJS internally provides many services that we can use in our application. $http is one example. There are other useful services, such as $route, $window, $location and so on. Some of the commonly used services in any AngularJS applications are listed below.

* $window Provide a reference to a DOM object.
* $Location Provides reference to the browser location.
* $timeout Provides a reference to window.settimeout function.
* $Log Used for logging.
* $sanitize Used to avoid script injections and display raw HTML in page.
* $Rootscope Used for scope hierarchy manipulation.
* $Route Used to display browser based path in browser URL.
* $Filter Used for providing filter access.
* $resource Used to work with Restful API.
* $document Used to access the window. Document object.
* $exceptionHandler Used for handling exceptions.
* $q: Provides a promise object.

### 21 Explain what is Dependency Injection in AngularJS?
Dependency Injection is one of the best features of AngularJS. It is a software design pattern in which objects are passed as dependencies. It helps us to remove hard coded dependencies and makes dependencies configurable. Using Dependency Injection, we can make components maintainable, reusable and testable.

#### Dependency Injection is required for the following

* Separating the process of creation and consumption of dependencies.
* It allows us to create independent development of the dependencies.
* We can change the dependencies when required.
* It allows injecting mock objects as dependencies for testing.

#### AngularJS uses dependency with several types

* Value
* Factory
* Service
* Provider
* Constant

### 22. What are the filters in AngularJS?
Filters are used to modify the data and can be clubbed in expression or directives using a pipe character. A filter formats the value of an expression for display to the user. They can be used in view templates, controllers, or services, and we can easily create our own filter. Filter is a module provided by AngularJS. There are nine components of filter which are provided by AngularJS. We can write custom as well.

* currency
* date
* filter
* json
* limitTo
* lowercase
* number
* orderBy
* uppercase

### 23. Explain Provider Method in AngularJS.
The Module.provider method allows you to take more control over the way that a service object is created or configured. The arguments to the provider method are the name of the service that is being defined and a factory function. The factory function is required to return a provider object that defines a method called $get, which in turn is required to return the service object. When the service is required, AngularJS calls the factory method to get the provider object and then calls the $get method to get the service object. Using the provider method doesn’t change the way that services are consumed, which means that I don’t need to make any changes to the controller or directive in the example.

The advantage of using the provider method is that you can add functionality to the provider method that can be used to configure the service object.

To demonstrate this process, I again change the serviceapp.js file as below,

```js
var serviceApp = angular.module('ServiceApp', []);  
  
serviceApp.provider("logService", function()  
{  
    var counter = true;  
    var debug = true;  
    return  
    {  
        messageCounterEnabled: function(setting)  
      {  
            if (angular.isDefined(setting))  
            {  
                counter = setting;  
                return this;  
            } else  
            {  
                return counter;  
            }  
        },  
        debugEnabled: function(setting)  
      {  
            if (angular.isDefined(setting))  
            {  
                debug = setting;  
                return this;  
            } else  
            {  
                return debug;  
            }  
        },  
        $get: function()   
      {  
            return  
            {  
                messageCount: 0,  
                log: function(msg)  
              {  
                    if (debug)   
                    {  
                        console.log("(LOG" + (counter ? " + " + this.messageCount++ + ") " : ") ") + msg);  
                    }  
                }  
            };  
        }  
    }  
});  
```

### Services
Syntax: `module.service( 'serviceName', function );`

When declaring serviceName as an injectable argument **you will be provided with an instance of the function. In other words** `new FunctionYouPassedToService()`.

### Factories
Syntax: `module.factory( 'factoryName', function );` 

When declaring factoryName as an injectable argument you will be provided with the value that is returned by invoking the function reference passed to module.factory.

### Providers
Syntax: `module.provider( 'providerName', function );`

Result: When declaring providerName as an injectable argument **you will be provided with `(new ProviderFunction()).$get()`.** The constructor function is instantiated before the $get method is called - `ProviderFunction` is the function reference passed to module.provider.

* Providers have the advantage that they can be configured during the module configuration phase.

```html
<!DOCTYPE html>
<html ng-app="app">
<head>
	<script src="http://cdnjs.cloudflare.com/ajax/libs/angular.js/1.0.1/angular.min.js"></script>
	<meta charset=utf-8 />
	<title>JS Bin</title>
</head>
<body ng-controller="MyCtrl">
	{{serviceOutput}}
	<br/><br/>
	{{factoryOutput}}
	<br/><br/>
	{{providerOutput}}

	<script>
		var app = angular.module( 'app', [] );

		var MyFunc = function() {

			this.name = "default name";

			this.$get = function() {
				this.name = "new name"
				return "Hello from MyFunc.$get(). this.name = " + this.name;
			};

			return "Hello from MyFunc(). this.name = " + this.name;
		};

		// returns the actual function
		app.service( 'myService', MyFunc );

		// returns the function's return value
		app.factory( 'myFactory', MyFunc );

		// returns the output of the function's $get function
		app.provider( 'myProv', MyFunc );

		function MyCtrl( $scope, myService, myFactory, myProv ) {

			$scope.serviceOutput = "myService = " + myService;
			$scope.factoryOutput = "myFactory = " + myFactory;
			$scope.providerOutput = "myProvider = " + myProv;

		}
	</script>

</body>
</html>

//Output

myService = [object Object] 
myFactory = Hello from MyFunc(). this.name = default name 
myProvider = Hello from MyFunc.$get(). this.name = new name
```

[@article](https://stackoverflow.com/a/15666049)



### 24. Explain $routeProvider in AngularJS?
The $routeProvider is used to set the configuration of urls and map them with the corresponding html page or ng-template and also attach a controller. Routing in AngularJS is taken care of by a service provide that is called $routeProvider. Routes for templates and urls in Angular are declared via the$routeProvider, that is the provider of the $route service. This service makes it easy to wire together controllers, view templates, and the current URL location in the browser.

We can use config() method of “myApp” module to configure $routeProvider. The when method of$routeProvideris used to bind the url with a template. This method takes a url(i.e. “/viewDelhi”) that will map with a template (i.e. delhi.htm) using the templateUrl parameter. The when method also binds a controller for templates using the controller parameter (i.e. controller: 'AddDelhi'), otherwise the method is used to set the default view.

Example

```js
mainApp.config(['$routeProvider', function($routeProvider)  
{  
    $routeProvider.  
    when('/viewDelhi',   
    {  
        templateUrl: 'delhi',  
        controller: 'AddDelhi'  
    }).  
    when('/viewMumbai',   
    {  
        templateUrl: 'mumbai',  
        controller: 'AddMumbai'  
    }).  
    when('/viewJaipur',   
    {  
        templateUrl: 'jaipur',  
        controller: 'AddJaipur'  
    }).  
    otherwise  
    ({  
        redirectTo: '/viewDelhi'  
    });  
}]);  
```

### 25. What Are Angular Prefixes $ And $$?
To prevent accidental name collisions within the code, AngularJS prefixes the names of public objects with $ and the names of private objects with $$.

Use of these literals ($ or $$) for any other reason is not recommended.

### 26. 































