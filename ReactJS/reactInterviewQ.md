### What is React?
React is a front end JavaScript library developed by Facebook in 2011. It follows the component based approach which helps in building reusable UI components. It is used for developing complex and interactive web and mobile UI. Even though, it was open-sourced only in 2015, it has one of the largest communities supporting it.

<br>
<br>

### What are the features of React? 
Major features of React are listed below:

1. It uses the **virtual DOM** instead of the real DOM.
2. It uses **server-side rendering.**
3. It follows **uni-directional data flow** or data binding.

### List some of the major advantages of React.
Some of the major advantages of React are:

1. It **increases** the application’s **performance**
2. It can be conveniently used on the client as well as server side
3. Because of JSX, code’s readability increases
4. React is easy to integrate with other frameworks like Meteor, Angular, etc
5. Using React, writing UI test cases become extremely easy

<br>
<br>

### What are the limitations of React?
Limitations of React are listed below:

1. React is just a library, not a full-blown framework
2. Its library is very large and takes time to understand
3. It can be little difficult for the novice programmers to understand
4. Coding gets complex as it uses inline templating and JSX


<br>
<br>

### What is JSX?
JSX is a shorthand for JavaScript XML. This is a type of file used by React which utilizes the expressiveness of JavaScript along with HTML like template syntax. This makes the HTML file really easy to understand. This file makes applications robust and boosts its performance. Below is an example of JSX:
```js
render(){
    return(        
         <div>
            <h1> Hello World from Edureka!!</h1>
         </div>
    );
}
```

<br>
<br>

### What do you understand by Virtual DOM? Explain its working.
A virtual DOM is a lightweight JavaScript object which originally is just the copy of the real DOM. It is a node tree that lists the elements, their attributes and content as Objects and their properties. React’s render function creates a node tree out of the React components. It then updates this tree in response to the mutations in the data model which is caused by various actions done by the user or by the system.

This Virtual DOM works in three simple steps.
1. Whenever any underlying data changes, the entire UI is re-rendered in Virtual DOM representation.
2. Then the difference between the previous DOM representation and the new one is calculated.
3. Once the calculations are done, the real DOM will be updated with only the things that have actually changed. 

<br>
<br>

### Differentiate between Real DOM and Virtual DOM.

#### Real DOM	
1. It updates slow.	
2. Can directly update HTML.	
3. Creates a new DOM if element updates.	
4. DOM manipulation is very expensive.	
5. Too much of memory wastage.	

#### Virtual  DOM
1. It updates faster.
2. Can’t directly update HTML.
3. Updates the JSX if element updates.
4. DOM manipulation is very easy.
5. No memory wastage.


<br>
<br>

### Why can’t browsers read JSX?
Browsers can only read JavaScript objects but JSX in not a regular JavaScript object. Thus to enable a browser to read JSX, first, we need to transform JSX file into a JavaScript object using JSX transformers like Babel and then pass it to the browser.

<br>
<br>

### How different is React’s ES6 syntax when compared to ES5?
Syntax has changed from ES5 to ES6 in following aspects:

1. require vs import
```js
// ES5
var React = require('react');
 
// ES6
import React from 'react';
```
2. export vs exports
```js
// ES5
module.exports = Component;
 
// ES6
export default Component;
```
3. component and function
```js
// ES5
var MyComponent = React.createClass({
    render: function() {
        return <h3>Hello Edureka!</h3>;
    }
});
 
// ES6
class MyComponent extends React.Component {
    render() {
        return <h3>Hello Edureka!</h3>;
    }
}
```
4. props
```js
// ES5
var App = React.createClass({
    propTypes: { name: React.PropTypes.string },
    render: function() {
        return <h3>Hello, {this.props.name}!</h3>;
    }
});
 
// ES6
class App extends React.Component {
    render() {
        return <h3>Hello, {this.props.name}!</h3>;
    }
}
```
5. state
```js
// ES5
var App = React.createClass({
    getInitialState: function() {
        return { name: 'world' };
    },
    render: function() {
        return <h3>Hello, {this.state.name}!</h3>;
    }
});
 
// ES6
class App extends React.Component {
    constructor() {
        super();
        this.state = { name: 'world' };
    }
    render() {
        return <h3>Hello, {this.state.name}!</h3>;
    }
}
```

<br>
<br>

### 

<br>
<br>

### 

<br>
<br>

### 
