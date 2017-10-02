### 1. What is Inversion of Control (IoC) and Dependency Injection?
In software engineering, inversion of control (IoC) is a programming technique in which object coupling is bound at run time by an assembler object and is typically not known at compile time using static analysis. In traditional programming, the flow of the business logic is determined by objects that are statically assigned to one another. With inversion of control, the flow depends on the object graph that is instantiated by the assembler and is made possible by object interactions being defined through abstractions. The binding process is achieved through “dependency injection”.

Inversion of control is a design paradigm with the goal of giving more control to the targeted components of your application, the ones that are actually doing the work.

Dependency injection is a pattern used to create instances of objects that other objects rely on without knowing at compile time which class will be used to provide that functionality. Inversion of control relies on dependency injection because a mechanism is needed in order to activate the components providing the specific functionality. Otherwise how will the framework know which components to create if it is no longer in control?

In Java, dependency injection may happen through 3 ways:

A constructor injection
A setter injection
An interface injection
