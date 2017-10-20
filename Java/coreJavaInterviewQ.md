### Q1) What are “static initializers” or “static blocks with no function names”?
When a class is loaded, all blocks that are declared static and don’t have function name (i.e. static initializers) are executed even before the constructors are executed. As the name suggests they are typically used to initialize static fields.

### Q2) What is the difference between constructors and other regular methods? What happens if you do not provide a constructor? Can you call one constructor from another? How do you call the superclass’s constructor?
* Constructors must have the same name as the class name and cannot return a value. The constructors
are called only once per creation of an object while regular methods can be called many times. E.g. for a Pet.class

```java
public Pet() {} // constructor
```

* Regular methods can have any name and can be called any number of times. E.g. for a Pet.class.

```java
public void Pet(){} // regular method has a void return type.
```

* Java does not actually require an explicit constructor in the class description. If you do not include a constructor, the Java compiler will create a default constructor in the byte code with an empty argument. This default constructor is equivalent to the explicit “Pet(){}”. If a class includes one or more explicit constructors like `public Pet(int id)` or `Pet(){}` etc, the java compiler does not create the default constructor `Pet(){}`.

#### Q. Can you call one constructor from another? 
Yes, by using this() syntax. E.g.

```java
public Pet(int id) {
  this.id = id; // “this” means this object
}
public Pet (int id, String type) {
  this(id); // calls constructor public Pet(int id) 
  this.type = type; // ”this” means this object
}
```

#### Q. How to call the superclass constructor? 
If a class called `SpecialPet` extends your `Pet` class then you can use the keyword `super` to invoke the superclass’s constructor. E.g.

```java
public SpecialPet(int id) {
  super(id); //must be the very first statement in the constructor.
}
```

* To call a regular method in the super class use: “super.myMethod( );”. This can be called at any line.

### Q3) How do you express an ‘is a’ relationship and a ‘has a’ relationship or explain inheritance and composition? What is the difference between composition and aggregation?
The `is a` relationship is expressed with **inheritance** and `has a` relationship is expressed with **composition**. Both
inheritance and composition allow you to place sub-objects inside your new class. Two of the main techniques for code reuse are class inheritance and object composition.

```java
// is-a
class Building{
.......
}
class House extends Building{
.........
}

// has-a
class House {
  Bathroom room = new Bathroom() ;
  ....
  public void getTotMirrors(){
    room.getNoMirrors();
    ....
  }
}
```

* Inheritance is uni-directional. For example House `is a` Building. But Building is not a House. Inheritance uses `extends` key word. Composition: is used when House has a Bathroom. It is incorrect to say House is a Bathroom. Composition simply means using instance variables that refer to other objects. The class House will have an instance variable, which refers to a Bathroom object.

#### Q. Which one to favor, composition or inheritance?
The guide is that inheritance should be only used when subclass `is a` superclass.
*  Don’t use inheritance just to get code reuse. If there is no `is a` relationship then use composition for code reuse. Overuse of implementation inheritance (uses the “extends” key word) can break all the subclasses, if the superclass is modified.
*  Do not use inheritance just to get polymorphism. If there is no `is a`  relationship and all you want is polymorphism then use interface inheritance with composition, which gives you code reuse

### Q4) What do you mean by polymorphism, inheritance, encapsulation, and dynamic binding?
**Polymorphism** – means the ability of a single variable of a given type to be used to reference objects of different types, and automatically call the method that is specific to the type of object the variable references. In a nutshell, polymorphism is a bottom-up method call. The benefit of polymorphism is that it is very easy to add new classes of derived objects without breaking the calling code (i.e. getTotArea() in the sample code shown below) that uses the polymorphic classes or interfaces. When you send a message to an object even though you don’t know what specific type it is, and the right thing happens, that’s called **polymorphism.** The process used by object-oriented programming languages to implement polymorphism is called **dynamic binding**.

* Polymorphism means "many forms."
* A reference variable is always of a single, unchangeable type, but it can refer to a subtype object.
* A single object can be referred to by reference variables of many different types —as long as they are the same type or a supertype of the object.
* The reference variable's type (not the object's type), determines which methods can be called!
* Polymorphic method invocations apply only to overridden instance methods.

**Inheritance** – is the inclusion of behavior (i.e. methods) and state (i.e. variables) of a base class in a derived class so that they are accessible in that derived class. The key benefit of Inheritance is that it provides the formal mechanism for
code reuse. Any shared piece of business logic can be moved from the derived class into the base class as part of
refactoring process to improve maintainability of your code by avoiding code duplication. The existing class is called the
superclass and the derived class is called the subclass. Inheritance can also be defined as the process whereby one
object acquires characteristics from one or more other objects the same way children acquire characteristics from their
parents. 
* Inheritance allows a class to be a subclass of a superclass, and thereby inherit public and protected variables and methods of the superclass.
* Inheritance is a key concept that underlies IS-A, polymorphism, overriding, overloading, and casting.
* All classes (except class Object), are subclasses of type Object, and therefore they inherit Object's methods.


There are two types of inheritances:

1. **Implementation inheritance (aka class inheritance):** You can extend an application’s functionality by reusing functionality in the parent class by inheriting all or some of the operations already implemented. In Java, you can only inherit from one superclass. Implementation inheritance promotes reusability but improper use of class inheritance can cause programming nightmares by breaking encapsulation and making future changes a problem. With implementation inheritance, the subclass becomes tightly coupled with the superclass. This will make the design fragile because if you want to change the superclass, you must know all the details of the subclasses to avoid breaking them. So when using implementation inheritance, **make sure that the subclasses depend only on the behavior of the superclass, not on the actual implementation.**
For example, the subclasses should only be concerned about the behavior but not how it is implemented.

2. **Interface inheritance (aka type inheritance):** This is also known as subtyping. Interfaces provide a mechanism for specifying a relationship between otherwise unrelated classes, typically by specifying a set of common methods each implementing class must contain. Interface inheritance promotes the design concept of **program to interfaces not to implementations.** This also reduces the coupling or implementation dependencies between systems. In Java, you can implement any number of interfaces. This is more flexible than implementation inheritance because it won’t lock you into specific implementations which make subclasses difficult to maintain. So care should be taken not to break the implementing classes by modifying the interfaces.

**Which one to use?** - Prefer interface inheritance to implementation inheritance because it promotes the design concept of coding to an interface and reduces coupling. Interface inheritance can achieve code reuse with the help of object composition. If you look at Gang of Four (GoF) design patterns, you can see that it favors interface inheritance to implementation inheritance.

#### Q. Why would you prefer code reuse via composition over inheritance? 
Both the approaches make use of polymorphism and gives code reuse (in different ways) to achieve the same results but:
* The advantage of class inheritance is that it is done **statically at compile-time and is easy to use.** The disadvantage of
class inheritance is that because it is **static,** implementation inherited from a parent class **cannot be changed at run-time**.
* In object composition, functionality is acquired dynamically at run-time by objects collecting references to other objects. The advantage of this approach is that **implementations can be replaced at run-time.** This is possible because objects are accessed only through their interfaces, so one object can be replaced with another just as long as they have the same type. For example: the composed class AccountHelperImpl can be replaced by another more efficient implementation as shown below if required:

```java
public class EfficientAccountHelperImpl implements AccountHelper {
  public void deposit(double amount) {
    System.out.println("efficient depositing " + amount);
  }
  public void withdraw(double amount) {
    System.out.println("efficient withdrawing " + amount);
  }
}
```

* Another problem with class inheritance is that the subclass becomes dependent on the parent class implementation. This makes it harder to reuse the subclass, especially if part of the inherited implementation is no longer desirable and hence can break encapsulation. Also a change to a superclass can not only ripple down the inheritance hierarchy to subclasses, but can also ripple out to code that uses just the subclasses making the design fragile by tightly coupling the subclasses with the super class. But it is easier to change the interface/implementation of the composed class. 
* Due to the flexibility and power of object composition, most design patterns emphasize object composition over inheritance whenever it is possible. Many times, a design pattern shows a clever way of solving a common problem through the use of object composition rather then a standard, less flexible, inheritance based solution.

**Encapsulation –** refers to keeping all the related members (variables and methods) together in an object. Specifying member variables as private can hide the variables and methods. Objects should hide their inner workings from the outside view. Good **encapsulation improves code modularity by preventing objects interacting with each other in an unexpected way,** which in turn makes future development and refactoring efforts easy.
* Encapsulation helps hide implementation behind an interface (or API).
* Encapsulated code has two features:
    * Instance variables are kept protected (usually with the private modifier).
    * Getter and setter methods provide access to instance variables.
* IS-A refers to inheritance or implementation.
* IS-A is expressed with the keyword extends.
* IS-A, "inherits from," and "is a subtype of " are all equivalent expressions.
* HAS-A means an instance of one class "has a" reference to an instance of another class or another instance of the same class.


### Q5) 
































