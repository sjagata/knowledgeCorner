### Q1. What are “static initializers” or “static blocks with no function names”?
When a class is loaded, all blocks that are declared static and don’t have function name (i.e. static initializers) are executed even before the constructors are executed. As the name suggests they are typically used to initialize static fields.

### Q2. What is the difference between constructors and other regular methods? What happens if you do not provide a constructor? Can you call one constructor from another? How do you call the superclass’s constructor?
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

### Q3. How do you express an ‘is a’ relationship and a ‘has a’ relationship or explain inheritance and composition? What is the difference between composition and aggregation?
The `is a` relationship is expressed with **inheritance** and `has a` relationship is expressed with **composition**. Both
inheritance and composition allow you to place sub-objects inside your new class. Two of the main techniques for code reuse are class inheritance and object composition.
* IS-A refers to inheritance or implementation.
* IS-A is expressed with the keyword extends.
* IS-A, "inherits from," and "is a subtype of " are all equivalent expressions.
* HAS-A means an instance of one class "has a" reference to an instance of another class or another instance of the same class.

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

### Q4. What do you mean by polymorphism, inheritance, encapsulation, and dynamic binding?
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



### Q5.What is the difference between an abstract class and an interface and when should you use them?
In design, you want the base class to present only an interface for its derived classes. This means, you don’t want anyone to actually instantiate an object of the base class. You only **want to upcast to it** (implicit upcasting, which gives you polymorphic behavior), so that its interface can be used. This is accomplished by making that class abstract using the abstract keyword. If anyone tries to make an object of an abstract class, the compiler prevents it.

The **interface** keyword takes this concept of an **abstract** class a step further by preventing any method or function implementation at all. You can only declare a method or function but not provide the implementation. The class, which is implementing the interface, should provide the actual implementation. The interface is a very useful and commonly used aspect in OO design, as it provides the **separation of interface and implementation** and enables you to:
* Capture similarities among unrelated classes without artificially forcing a class relationship.
* Declare methods that one or more classes are expected to implement.
* Reveal an object's programming interface without revealing its actual implementation.
* Model multiple interface inheritance in Java, which provides some of the benefits of full on multiple inheritances, a feature that some object-oriented languages support that allow a class to have more than one superclass.
* When you implement an interface, you are fulfilling its contract.
* You implement an interface by properly and concretely overriding all of the methods defined by the interface.
* A single class can implement many interfaces.

**Abstract class**
1. Have executable methods and abstract methods. 
2. Can only subclass one abstract class.

**Interface**
1. Have no implementation code. All methods are public, abstract.
2. A class can implement any number of interfaces.

#### Q. When to use an abstract class?: 
In case where you want to use implementation inheritance then it is usually provided by an abstract base class. Abstract classes are excellent candidates inside of application frameworks. Abstract classes let you define some default behavior and force subclasses to provide any specific behavior. Care should be taken not to overuse implementation inheritance as discussed in Q10 in Java section.
#### Q. When to use an interface?: 
For polymorphic interface inheritance, where the client wants to only deal with a type and does not care about the actual implementation use interfaces. If you need to change your design frequently, you should prefer using interface to abstract. CO Coding to an interface reduces coupling and interface inheritance can achieve code reuse with the help of object composition. 

For example: The Spring framework’s dependency injection promotes code to an interface principle. Another justification for using interfaces is that they solve the ‘diamond problem’ of traditional multiple inheritance as shown in the figure. Java does not support multiple inheritance. Java only supports multiple interface inheritance. Interface will solve all the ambiguities caused by this ‘diamond problem’.

### Q6. Why there are some interfaces with no defined methods (i.e. marker interfaces) in Java?
The interfaces with no defined methods act like markers. They just tell the compiler that the objects of the classes implementing the interfaces with no defined methods need to be treated differently. 
Example: `java.io.Serializable`, `java.lang.Cloneable`, `java.util.EventListener` etc. 
Marker interfaces are also known as `tag` interfaces since they tag all the derived classes into a category based on their purpose.

### Q7. When is a method said to be overloaded and when is a method said to be overridden?
**Method Overloading**
* Overloading deals with multiple methods in the same class with the same name but different method signatures.

```java
class MyClass {
  public void getInvestAmount(int rate) {…}
  public void getInvestAmount(int rate, long principal) { … }
}
```

Both the above methods have the same method names but different method signatures, which mean the methods are overloaded.
* Overloading lets you define the **same operation in different ways for different data.**

**Method Overriding**
* Overriding deals with two methods, one in the parent class and the other one in the child class and has the same name and signatures.

```java
class BaseClass{
  public void getInvestAmount(int rate) {…}
}
class MyClass extends BaseClass {
  public void getInvestAmount(int rate) { …}
}
```

Both the above methods have the same method names and the signatures but the method in the subclass MyClass overrides the method in the superclass BaseClass.
* Overriding lets you define the **same operation in different ways for different object types.**

* Methods can be overridden or overloaded; **constructors can be overloaded but not overridden.**
* Abstract methods must be overridden by the first concrete (non-abstract)subclass.
* With respect to the method it overrides, the overriding method
    * Must have the same argument list.
    * Must have the same return type, except that as of Java 5, the return type can be a subclass—this is known as a covariant return.
    * Must not have a more restrictive access modifier.
    * May have a less restrictive access modifier.
    * Must not throw new or broader checked exceptions.
    * May throw fewer or narrower checked exceptions, or any unchecked exception.
* `final` methods cannot be overridden.
* Only inherited methods may be overridden, and remember that private methods are not inherited.
* A subclass uses super.overriddenMethodName() to call the superclass version of an overridden method.
* Overloading means reusing a method name, but with different arguments.
* Overloaded methods
    * Must have different argument lists
    * May have different return types, if argument lists are also different
    * May have different access modifiers
    * May throw different exceptions
* Methods from a superclass can be overloaded in a subclass.
* Polymorphism applies to overriding, not to overloading.
* Object type (not the reference variable's type), determines which overridden method is used at runtime.
* Reference type determines which overloaded method will be used at compile time.


### Q8. What is the difference between “==” and equals(…) method? What is the difference between shallow comparison and deep comparison of objects?
**== [ shallow comparison ]**
* The `==` returns true, **if the variable reference points to the same object in memory.** This is a `shallow comparison`.

**equals( ) [deep comparison ]**
* **The equals()** - returns the results of running the equals() method of a user supplied class, **which compares the attribute values.** The equals() method provides `deep comparison` by checking if two objects are logically equal as opposed to the shallow comparison provided by the operator ==. 
* If equals() method does not exist in a user supplied class then the inherited Object class's equals() method is run which evaluates if the references point to the same object in memory. The object.equals() works just like the "==" operator (i.e shallow comparison).
* Overriding the Object class may seem simple but there are many ways to get it wrong, and consequence can be unpredictable behavior.


* String assignment with the “new” operator follow the same rule as == and equals( ) as mentioned above.

```java
String str = new String(“ABC”); //Wrong. Avoid this because a new String instance is created each time it is executed.
```

* The `literal` String assignment is shown below, where if the assignment value is identical to another String assignment value created then a new String object is not created. A reference to the existing String object is returned.

```java
String str = “ABC”; //Right because uses a single instance rather than creating a new instance each time it is executed.
```

```java
public class StringBasics {
  public static void main(String[] args) {
    String s1 = new String("A"); //not recommended, use String s1 = "A"
    String s2 = new String("A"); //not recommended, use String s2 = "A"
    
    //standard: follows the == and equals() rule like plain java objects.
    
    if (s1 == s2) { //shallow comparison
      System.out.println("references/identities are equal"); //never reaches here
    }
    if (s1.equals(s2)) { //deep comparison
      System.out.println("values are equal"); // this line is printed
    }
    
    //variation: does not follow the == and equals rule
    
    String s3 = "A"; //goes into a String pool.
    String s4 = "A"; //refers to String already in the pool.
    if (s3 == s4) { //shallow comparison
      System.out.println("references/identities are equal"); //this line is printed
    }
    if (s3.equals(s4)) { //deep comparison
      System.out.println("values are equal"); //this line is also printed
    }
  }
}
```

* String class is designed with **Flyweight design pattern.** When you create a String constant as shown above in the variation, (i.e. String s3 = “A”, s4= “A”), it will be checked to see if it is already in the String pool. If it is in the pool, it will be picked up from the pool instead of creating a new one. **Flyweights are shared objects and using them can result in substantial performance gains.**

#### Q. What is an intern() method in the String class?
A pool of Strings is maintained by the String class. When the intern() method is invoked equals(…) method is invoked to determine if the String already exist in the pool. If it does then the String from the pool is returned. Otherwise, this String object is added to the pool and a reference to this object is returned. **For any two Strings s1 & s2, s1.intern() == s2.intern() only if s1.equals(s2) is true.**

### Q8. What are the non-final methods in Java Object class, which are meant primarily for extension?

* equals(), hashCode(), and toString() are public.
* Override toString() so that System.out.println() or other methods can see something useful, like your object's state.
* Use **==** to determine if two reference variables refer to the same object.
* Use **equals()** to determine if two objects are meaningfully equivalent.
* If you don't override equals(), your objects won't be useful hashing keys.
* If you don't override equals(), different objects can't be considered equal.
* **Strings** and **wrappers override equals()** and make **good hashing keys**.
* When overriding equals(), use the instanceof operator to be sure you're evaluating an appropriate class.
* When overriding equals(), compare the objects' significant attributes.
* Highlights of the **equals() contract**:
    * **Reflexive**: x.equals(x) is true.
    * **Symmetric**: If x.equals(y) is true, then y.equals(x) must be true.
    * **Transitive**: If x.equals(y) is true, and y.equals(z) is true, then z.equals(x) is true.
    * **Consistent**: Multiple calls to x.equals(y) will return the same result.
    * **Null**: If x is not null, then x.equals(null) is false.
* If **x.equals(y)** is **true**, then **x.hashCode() == y.hashCode()** is **true**.
* If you override equals(), override hashCode().
* HashMap, HashSet, Hashtable, LinkedHashMap, & LinkedHashSet use hashing.
* An appropriate hashCode() override sticks to the hashCode() contract.
* An efficient hashCode() override distributes keys evenly across its buckets.
* An overridden equals() must be at least as precise as its hashCode() mate.
* To reiterate: if two objects are equal, their hashcodes must be equal.
* It's legal for a hashCode() method to return the same value for all instances (although in practice it's very inefficient).
* Highlights of the **hashCode() contract**:
    * **Consistent**: multiple calls to x.hashCode() return the same integer.
    * If x.equals(y) is true, x.hashCode() == y.hashCode() is true.
    * If x.equals(y) is false, then x.hashCode() == y.hashCode() can be either true or false, but false will tend to create better efficiency.
* **transient variables** aren't appropriate for equals() and hashCode().

The **non-final methods** are **equals(), hashCode(), toString(), clone(), and finalize().** The other methods like **wait(), notify(), notifyAll(), getClass()** etc are **final methods** and therefore cannot be overridden. Let us look at these non-final methods, which are meant primarily for extension (i.e. inheritance).

![alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Java/images/classObjct.png "class object")

**The equals() and hashCode() methods prove to be very important, when objects implementing these two methods are added to collections. If implemented incorrectly or not implemented at all then your objects stored in a collection like a Set, List or Map may behave strangely and also is hard to debug.**

* Class Object has a finalize() method.
* The `finalize()` method is guaranteed to run once and only once before the garbage collector deletes an object.
* The garbage collector makes no guarantees, `finalize()` may never run.
* You can uneligibilize an object for GC from within `finalize()`.

### Q9. When providing a user defined key class for storing objects in the HashMaps or Hashtables, what methods do you have to provide or override (i.e. method overriding)?



<br>
<br>

## Collections 

### Q1. What is the main difference between an ArrayList and a Vector? What is the main difference between HashMap and Hashtable? What is the difference between a stack and a queue?
* Original classes before the introduction of Collections API. `Vector & Hashtable` are synchronized. Any method that touches their contents is thread-safe.
* So if you don’t need a thread safe collection, use the `ArrayList or HashMap`. Why pay the price of synchronization unnecessarily at the expense of performance degradation.

#### Q. So which is better? As a general rule, prefer ArrayList/HashMap to Vector/Hashtable. 
If your application is a multithreaded application and at least one of the threads either adds or deletes an entry into the collection then use new Java collections API‘s **external synchronization facility** as shown below to temporarily synchronize
your collections as needed:

```java
Map myMap = Collections.synchronizedMap (myMap); // single lock for the entire map
List myList = Collections.synchronizedList (myList); // single lock for the entire list
```

* If you are using J2SE5, you should use the new `java.util.concurrent` package for improved performance because the concurrent package collections are not governed by a single synchronized lock as shown above. The `java.util.concurrent` package collections like `ConcurrentHashMap` is **threadsafe and at the same time safely permits any number of concurrent reads as well as tunable number of concurrent writes.** The `java.util.concurrent` package also provides an efficient scalable thread-safe non-blocking FIFO queue like `ConcurrentLinkedQueue`.

* The `java.util.concurrent` package also has classes like `CopyOnWriteArrayList`, `CopyOnWrite- ArraySet`, which gives you thread safety with the added benefit of immutability to deal with data that changes infrequently. The `CopyOnWriteArrayList` behaves much like the ArrayList class, except that when the list is modified, instead of modifying the underlying array, a new array is created and the old array is discarded. This means that when a caller gets an iterator (i.e. `copyOnWriteArrayListRef.iterator()` ), which internally holds a reference to the underlying CopyOnWriteArrayList object’s array, which is immutable and therefore can be used for traversal without requiring either synchronization on the list `copyOnWriteArrayListRef` or need to clone() the `copyOnWriteArrayListRef` list before traversal (i.e. there is no risk of concurrent modification) and also offers better performance.

#### Q. What is Read-Write Lock? Does ConcurrentHashMap in Java Uses The ReadWrite Lock?
ReadWrite Lock is an implementation of `lock stripping technique`, where two separate locks are used for read and write operation. Since read operation doesn't modify the state of the object, it's safe to allow multiple thread access to a shared object for reading without locking, and by splitting one lock into read and write lock, you can easily do that. 

Java provides an implementation of read-write lock in the form of `ReentrantReadWritLock` class in the `java.util.concurrent.lock` package. This is worth looking before you decide to write your own read-write locking implementation. 

Also, the current implementation of `java.util.ConcurrentHashMap` doesn't use the ReadWriteLock, instead, it divides the Map into several segments and locks them separately using different locks. This means any given time, **only a portion of the ConcurrentHashMap is locked, instead of the whole Map.** See [how ConcurrentHashMap internally works in Java](http://javarevisited.blogspot.com/2013/02/concurrenthashmap-in-java-example-tutorial-working.html) for more detail. 

**Arrays**
* Java arrays are even faster than using an `ArrayList/Vector` and perhaps therefore may be preferable if you know the size of your array upfront (because arrays cannot grow as Lists do).
* In an array, any item can be accessed.

**List / Stack etc**
* `ArrayList/Vector` are specialized data structures that internally uses an array with some convenient methods like `add(..)`, `remove(…)` etc so that they can grow and shrink from their initial size. ArrayList also supports index based searches with `indexOf(Object obj)` and `lastIndexOf(Object obj)` methods. 
* These are more abstract than arrays and access is restricted. For example, a stack allows access to only last item inserted.

**Queue<E> (added in J2SE 5.0)**
* First item to be inserted is the first one to be removed.
* This mechanism is called First In First Out (FIFO).
* Placing an item in the queue is called `enqueue or insertion` and removing an item from a queue is called `dequeue or deletion`. Pre J2SE 5.0, you should write your own Queue class with enqueue() and dequeue() methods using an ArrayList or a LinkedList class.
J2SE 5.0 has a java.util.Queue<E> interface.

**Stack**
* Allows access to only last item inserted.
* An item is inserted or removed from one end called the “top” of the stack. This is called Last In First Out (LIFO) mechanism.
* Placing the data at the top is called “pushing” and removing an item from the top is called “popping”. If you want to reverse “XYZ” -> ZYX, then you can use a `java.util.Stack`

### Q2. Explain the Java Collections Framework?
The key interfaces used by the collections framework are **List, Set and Map**. The List and Set extends the **Collection interface**. Should not confuse the Collection interface with the **Collections class** which is a utility class.

* Common collection activities include adding objects, removing objects, verifying object inclusion, retrieving objects, and iterating.
* Three meanings for "collection":
    * **collection** Represents the data structure in which objects are stored
    * **Collection** java.util **interface** from which Set and List extend
    * **Collections** A **class** that holds static collection utility methods
* Four basic flavors of collections include Lists, Sets, Maps, Queues:
    * **Lists** of things **Ordered, duplicates allowed, with an index.**
    * **Sets** of things **May or may not be ordered and/or sorted; duplicates not allowed.**
    * **Maps** of things with keys **May or may not be ordered and/or sorted; duplicate keys are not allowed.**
    * **Queues** of things to process Ordered by FIFO or by priority.
* Four basic sub-flavors of collections Sorted, Unsorted, Ordered, Unordered.
    * **Ordered** Iterating through a collection in a specific, non-random order.
    * **Sorted** Iterating through a collection in a sorted order.
* Sorting can be alphabetic, numeric, or programmer-defined.

Key Attributes of Common Collection Classes
* **ArrayList:** Fast iteration and fast random access.
* **Vector:** It's like a slower ArrayList, but it has synchronized methods.
* **LinkedList:** Good for adding elements to the ends, i.e., stacks and queues.
* **HashSet:** Fast access, assures no duplicates, provides no ordering.
* **LinkedHashSet:** No duplicates; iterates by insertion order.
* **TreeSet:** No duplicates; iterates in sorted order. 
   * A TreeSet is an **ordered HashSet**, which implements the **SortedSet** interface.
* **HashMap:** Fastest updates (key/values); allows one null key, many null values.
* **Hashtable:** Like a slower HashMap (as with Vector, due to its synchronized methods). No null values or null keys allowed.
* **LinkedHashMap:** Faster iterations; iterates by insertion order or last accessed; allows one null key, many null values.
* **TreeMap:** A sorted map.
* **PriorityQueue:** A to-do list ordered by the elements' priority.

Using Collection Classes
* Collections hold only Objects, but primitives can be autoboxed.
* Iterate with the enhanced for, or with an Iterator via hasNext() & next().
    * **hasNext()** determines if more elements exist; the Iterator does NOT move.
    * **next()** returns the next element AND moves the Iterator forward.
* To work correctly, a Map's keys must override **equals()** and **hashCode()**.
* Queues use **offer() to add an element**, **poll() to remove the head of the queue**, and **peek() to look at the head of a queue.**
* As of Java 6 TreeSets and TreeMaps have new navigation methods like floor() and higher().
* You can create/extend "backed" sub-copies of TreeSets and TreeMaps.

Utility Classes: Collections and Arrays 
* Both of these java.util classes provide
    * A sort() method. Sort using a Comparator or sort using natural order.
    * A binarySearch() method. Search a pre-sorted array or List.
* `Arrays.asList()` creates a List from an array and links them together.
* `Collections.reverse()` reverses the order of elements in a List.
* `Collections.reverseOrder()` returns a Comparator that sorts in reverse.
* `Lists and Sets` have a `toArray()` method to create arrays.


#### Q. How to implement collection ordering?
**SortedSet** and **SortedMap interfaces** maintain sorted order. The classes, which implement the Comparable interface, impose natural order. By implementing Comparable, sorting an array of objects or a collection (List etc) is as simple as:

```java
Arrays.sort(myArray);
Collections.sort(myCollection); // do not confuse “Collections” utility class with the 
                                // “Collection” interface without an “s”.
```

For classes that don’t implement Comparable interface, or when one needs even more control over ordering based on multiple attributes, a Comparator interface should be used.

* Sorting can be in natural order, or via a Comparable or many Comparators.
* Implement **Comparable** using **compareTo()**; provides only one sort order.
* Create many **Comparators** to sort a class many ways; implement **compare()**.
* To be sorted and searched, a List's elements must be comparable.
* To be searched, an array or List must first be sorted.

```java
if compare(o1,o2) == 0 then o1.equals(o2) should be true.
if compare(o1,o2) != 0 then o1.equals(o2) should be false.
```

#### Q. What is an Iterator?
An Iterator is a use once object to access the objects stored in a collection. **Iterator design pattern** (aka Cursor) is used, which is a behavioral design pattern that provides a way to access elements of a collection sequentially without exposing its internal representation.

#### Q. Why do you get a ConcurrentModificationException when using an iterator?
**Problem:**
The `java.util Collection` classes are fail-fast, which means that if one thread changes a collection while another thread is traversing it through with an `iterator` the `iterator.hasNext()` or `iterator.next()` call will throw `ConcurrentModificationException`. Even the synchronized collection wrapper classes `SynchronizedMap` and `SynchronizedList` are only conditionally thread-safe, which means all individual operations are thread-safe but compound operations where flow of control depends on the results of previous operations may be subject to threading issues.

```java
Collection<String> myCollection = new ArrayList<String>(10);

myCollection.add("123");
myCollection.add("456");
myCollection.add("789");

for (Iterator it = myCollection.iterator(); it.hasNext();) {
  String myObject = (String)it.next();
  System.out.println(myObject);
  if (someConditionIsTrue) {
    myCollection.remove(myObject); //can throw ConcurrentModificationException in single as well as multi-thread access situations.
  }
}
```

**Solutions 1-3: for multi-thread access situation:**
* **Solution 1:** You can convert your list to an array with `list.toArray()` and iterate on the array. This approach is not recommended if the list is large.
* **Solution 2:** You can lock the entire list while iterating by wrapping your code within a `synchronized block`. This approach adversely affects scalability of your application if it is highly concurrent.
* **Solution 3:** If you are using JDK 1.5 then you can use the `ConcurrentHashMap` and `CopyOnWriteArrayList` classes, which provide much better scalability and the iterator returned by `ConcurrentHashMap.iterator()` will not throw `ConcurrentModificationException` while preserving thread-safety.

**Solution 4: for single-thread access situation:**

```java
//Use:
it.remove(); // removes the current object via the Iterator “it” which has a reference to
// your underlying collection “myCollection”. Also can use solutions 1-3.

//Avoid:
myCollection.remove(myObject); // avoid by-passing the Iterator. When it.next() is called, can throw the exception
// ConcurrentModificationException
```

#### Q. What is a list iterator?
The `java.util.ListIterator` is an iterator for lists that allows the programmer to traverse the list in either direction (i.e. forward and or backward) and modify the list during iteration.

#### Q. What are static factory methods?
Some of the above mentioned features like searching, sorting, shuffling, immutability etc are achieved with `java.util.Collections` class and `java.util.Arrays` utility classes. The great majority of these implementations are provided via **static factory methods in a single, non-instantiable (i.e. private constrctor) class.** 
**Speaking of static factory methods, they are an alternative to creating objects through constructors.** 
Unlike constructors, **static factory methods are not required to create a new object (i.e. a duplicate object) each time they are invoked (e.g. immutable instances can be cached)** and also they have a more meaningful names like valueOf, instanceOf, asList etc. 

For example:

```java
// Instead of:
String[] myArray = {"Java", "J2EE", "XML", "JNDI"};
for (int i = 0; i < myArray.length; i++) {
  System.out.println(myArray[i]);
}

// You can use:
String[] myArray = {"Java", "J2EE", "XML", "JNDI"};
System.out.println(Arrays.asList(myArray)); //factory method Arrays.asList(…)
```
* The following static factory method (an alternative to a constructor) example **converts a boolean primitive value to a Boolean wrapper object.**

```java
public static Boolean valueOf(boolean b) {
  return (b ? Boolean.TRUE : Boolean.FALSE)
}
```

### Q3. What are some of the best practices relating to Java collection?
1. **Use ArrayList, HashMap etc as opposed to Vector, Hashtable etc, where possible to avoid any synchronization overhead.** Even better is to use just arrays where possible. If multiple threads concurrently access a collection and at least one of the threads either adds or deletes an entry into the collection, then the collection must be externally synchronized. This is achieved by:

```java
Map myMap = Collections.synchronizedMap (myMap); //conditional thread-safety
List myList = Collections.synchronizedList (myList); //conditional thread-safety
// use java.util.concurrent package for J2SE 5.0 Refer Q16 in Java section under ConcurrentModificationException
```

2. Set the initial capacity of a collection appropriately (e.g. ArrayList, HashMap etc). This is because Collection classes like ArrayList, HashMap etc must grow periodically to accommodate new elements. But if you have a very large array, and you know the size in advance then you can speed things up by setting the initial size appropriately.
For example: HashMaps/Hashtables need to be created with sufficiently large capacity to minimize rehashing (which happens every time the table grows). HashMap has two parameters initial capacity and load factor that affect its performance and space requirements. Higher load factor values (default load factor of 0.75 provides a good trade off between performance and space) will reduce the space cost but will increase the lookup cost of myMap.get(…) and myMap.put(…) methods. When the number of entries in the HashMap exceeds the current capacity * loadfactor then the capacity of the HasMap is roughly doubled by calling the rehash function. It is also very important not to set the initial capacity too high or load factor too low if iteration performance or reduction in space is important.

3. **Program in terms of interface not implementation:** For example you might decide a LinkedList is the best choice for some application, but then later decide ArrayList might be a better choice for performance reason. 

```java
//Use:
List list = new ArrayList(100); // program in terms of interface & set the initial capacity.
//Instead of:
ArrayList list = new ArrayList();
```

4. **Return zero length collections or arrays as opposed to returning null:** Returning null instead of zero length collection (use `Collections.EMPTY_SET`, `Collections.EMPTY_LIST`, `Collections.EMPTY_MAP`) is more error prone, since the programmer writing the calling method might forget to handle a return value of null.

5. **Immutable objects should be used as keys for the HashMap:** Generally you use a `java.lang.Integer` or a `java.lang.String` class as the key, which are immutable Java objects. If you define your own key class then it is a best practice to make the key class an immutable object (i.e. do not provide any setXXX() methods etc). If a programmer wants to insert a new key then he/she will always have to instantiate a new object (i.e. cannot mutate the existing key because immutable key object class has no setter methods).

6. **Encapsulate collections:** In general collections are not immutable objects. So care should be taken not to unintentionally expose the collection fields to the caller.

7. Avoid storing unrelated or different types of objects into same collection







