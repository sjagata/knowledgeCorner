# Demystifying Custom Directives

## The Four Functions of the AngularJS Directive Life Cycle

There are many options that can be configured and how those options are related to each other is important. Each directive undergoes something similar to a life cycle as AngularJS compiles and links the DOM. The directive lifecycle begins and ends within the AngularJS bootstrapping process, before the page is rendered. In a directive’s life cycle, there are four distinct functions that can execute if they are defined. Each enables the developer to control and customize the directive at different points of the life cycle.

**The four functions are: compile, controller, pre-link and post-Link.**

The **_compile_** function allows the directive to manipulate the DOM before it is compiled and linked thereby allowing it to add/remove/change directives, as well as, add/remove/change other DOM elements.

The **_controller_** function facilitates directive communication. Sibling and child directives can request the controller of their siblings and parents to communicate information.

The **_pre-link_** function allows for private $scope manipulation before the post-link process begins.

The **_post-link_** method is the primary workhorse method of the directive.

In the directive, post-compilation DOM manipulation takes place, event handlers are configured, and so are watches and other things. In the declaration of the directive, the four functions are defined like this.

```js
  .directive("directiveName",function () {

    return {
      controller: function() {
        // controller code here...
      },
      compile: {
  
        // compile code here...

        return {

          pre: function() {
            // pre-link code here...
          },
      
          post: function() {
            // post-link code here...
          }
        };
      }
    }
  })
  ```
  
Commonly, not all of the functions are needed. In most circumstances, developers will simply create a controller and post-link function following the pattern below.

```js
  .directive("directiveName",function () {

    return {

      controller: function() {
        // controller code here...
      },
  
      link: function() {
        // post-link code here...
      }
    }
  })
  ```
  
In this configuration, link refers to the post-link function.

Whether all or some of the functions are defined, their execution order is important, especially their execution relative to the rest of the AngularJS application.

## AngularJS Directive Function Execution Relative to other Directives

Consider the following HTML snippet with the directives parentDir, childDir and grandChildDir applied to the HTML fragment.

```html
<div parentDir>
  <div childDir>
    <div grandChildDir>
    </div>
  </div>
</div>
```
The execution order of the functions within a directive, and relative to other directives, is as follows:

* Compile Phase

..* Compile Function: parentDir
..* Compile Function: childDir
..* Compile Function: grandChildDir

* Controller & Pre-Link Phase

..* Controller Function: parentDir
..* Pre-Link Function: parentDir
..* Controller Function: childDir
..* Pre-Link Function: childDir
..* Controller Function: grandChildDir
..* Pre-Link Function: grandChildDir

*Post-Link Phase

..* Post-Link Function: grandChildDir
..* Post-Link Function: childDir
..* Post-Link Function: parentDir


