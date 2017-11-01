### Higher Order Components 
HOC is a react component that adds some additional functionality or behaviour to an existing component that you have already written or planned to write in the furture
* HOC and prctice end up being a fantastic way to extract functionality that is common to multiple coponents or may be multiple features within our application.
* It is also grat for providing duplicate logic or maybe we are duplicating logic all over the place inside our app and if we see a location where we can kind of centralize that logic that would be the purpose of a **higher order component**
* HOC are also very commanly used with third party libraries including **react-redux**

`Component`  +  `HOC` = `Component + Additional functionality or Data` (**Enhanced** or **Composed** Component)

Example: `connect` function from `react-redux` is a HOC.

* `Provider` wraps the reducx store which is you know redux the actual library, Its the object that holds our global application state that is formed by all of our different reducers.
* The provider holds the redux store and it watches the redux store very directly says hey redux store whenever you changes i want you to tell me just tell me whenever you change thats the job of the provider.
* Then Whenever the redux store changes the provider takes notice of it and it says OK new state something new just happened I need to ga and update any child components that I have.
* So provider broadcast down to any connected component - hey there is just some change to the redux state - take it read render yourself do whatever you want with it, here's the new state.

![Alt text](./images/reactjs4.png?raw=true "Optional Title")

<br>
<br>


