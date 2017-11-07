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
You should override the equals() and hashCode() methods from the Object class. The default implementation of the equals() and hashcode(), which are inherited from the `java.lang.Object` uses an object instance’s memory location (e.g. MyObject@6c60f2ea). This can cause problems when two instances of the car objects have the same color but the inherited equals() will return false because it uses the memory location, which is different for the two instances. Also the toString() method can be overridden to provide a proper string representation of your object.
![alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Java/images/hascodeEquals.png "class object")

#### Q. What are the primary considerations when implementing a user defined key?
* If a class overrides equals(), it must override hashCode().
* If 2 objects are equal, then their hashCode values must be equal as well.
* If a field is not used in equals(), then it must not be used in hashCode().
* If it is accessed often, hashCode() is a candidate for caching to enhance performance.
* It is a best practice to implement the user defined key class as an immutable object.

#### Q. Why it is a best practice to implement the user defined key class as an immutable object?
**Problem:**
As per the code snippet shown below if you use a mutable user defined class “UserKey” as a HashMap key and subsequently if you mutate (i.e. modify via setter method e.g. key.setName(“Sam”)) the key after the object has been added to the HashMap then you will not be able to access the object later on. The original key object will still be in the HashMap (i.e. you can iterate through your HashMap and print it – both prints as “Sam” as opposed to “John” & Sam) but you cannot access it with map.get(key) or querying it with map.containsKey(key) will return false because the key “John” becomes “Sam” in the “List of keys” at the key index “345678965” if you mutate the key after adding. These types of errors are very hard to trace and fix.

```java
Map myMap = new HashMap(10);
//add the key “John”
UserKey key = new UserKey(“John”); //Assume UserKey class is mutable
myMap.put(key, “Sydney”);
//now to add the key “Sam”
key.setName(“Sam”); // same key object is mutated instead of creating a new instance.
                    // This line modifies the key value “John” to “Sam” in the “List of keys”
                    // as shown in the diagram above. This means that the key “John” cannot be
                    // accessed. There will be two keys with “Sam” in positions with hash
                    // values 345678965 and 76854676.
myMap.put(key, “Melbourne”);
myMap.get(new UserKey(“John”)); // key cannot be accessed. The key hashes to the same position
// 345678965 in the “Key index array” but cannot be found in the “List of keys”
```

**Solution:**
Generally you use a `java.lang.Integer` or a `java.lang.String` class as the key, which are immutable Java objects. If you define your own key class then it is a best practice to make the key class an immutable object (i.e. do not provide any setXXX() methods in your key class. e.g. no setName(…) method in the UserKey class). If a programmer wants to insert a new key then he/she will always have to instantiate a new object (i.e. cannot mutate the existing key because immutable key object class has no setter methods).

```java
Map myMap = new HashMap(10);
//add the key “John”
UserKey key1 = new UserKey(“John”); //Assume UserKey is immutable
myMap.put(key1, “Sydney”);

//add the key “Sam”
UserKey key2 = new UserKey(“Sam”); //Since UserKey is immutable, new instance is created.
myMap.put(key2, “Melbourne”);
myMap.get(new UserKey(“John”)); //Now the key can be accessed
```

**Similar issues are possible with the Set** (e.g. HashSet) as well. If you add an object to a `Set` and subsequently modify the added object and later on try to query the original object it may not be present. `mySet.contains(originalObject)` may return `false`.

* `J2SE 5.0` introduces enumerated constants, which improves readability and maintainability of your code. Java programming language enums are more powerful than their counterparts in other languages. Example: As shown below a class like “Weather” can be built on top of simple enum type “Season” and the class “Weather” can be made immutable, and only one instance of each “Weather” can be created, so that your Weather class does not have to override equals() and hashCode() methods.

```java
public class Weather {
  public enum Season {WINTER, SPRING, SUMMER, FALL}
  private final Season season;
  private static final List<Weather> listWeather = new ArrayList<Weather> ();
  
  private Weather (Season season) { this.season = season;}
  public Season getSeason () { return season;}
    static {
      for (Season season : Season.values()) { //using J2SE 5.0 for each loop
        listWeather.add(new Weather(season));
      }
    }
  }
  public static ArrayList<Weather> getWeatherList () { return listWeather; }
  public String toString(){ return season;} //takes advantage of toString() method of Season.
}
```

* An enum specifies a list of constant values assigned to a type.
* An enum is NOT a String or an int; **an enum constant's type is the enum type.** For example, SUMMER and FALL are of the enum type Season.
* An enum can be declared outside or inside a class, **but NOT in a method**.
* An enum declared outside a class must NOT be marked static, final, abstract, protected, or private.
* Enums can contain constructors, methods, variables, and constant class bodies.
* enum constants can send arguments to the enum constructor, using the syntax BIG(8), where the int literal 8 is passed to the enum constructor.
* enum constructors can have arguments, and can be overloaded.
* enum constructors can NEVER be invoked directly in code. They are always called automatically when an enum is initialized.
* The semicolon at the end of an enum declaration is optional. These are legal:
    * enum Foo { ONE, TWO, THREE}
    * enum Foo { ONE, TWO, THREE};
* **MyEnum.values()** returns an array of MyEnum's values.

### Q10. What is the main difference between a String and a StringBuffer class?
* **String objects** are **immutable**, and **String reference variables are not.**
* If you create a new String without assigning it, it will be lost to your program.
* If you redirect a String reference to a new String, the old String can be lost.
* String methods use zero-based indexes, except for the second argument of substring().
* The String class is final—its methods can't be overridden.
* When the JVM finds a String literal, it is added to the String literal pool.
* Strings have a method: length(); arrays have an attribute named length.
* The **StringBuffer's** API is the same as the new **StringBuilder's API,** except that **StringBuilder's methods are not synchronized for thread safety.**
* **StringBuilder** methods should **run faster** than **StringBuffer** methods.
* All of the following bullets apply to both StringBuffer and StringBuilder:
    * They are mutable—they can change without creating a new object.
    * StringBuffer methods act on the invoking object, and objects can change without an explicit assignment in the statement.
    * StringBuffer equals() is not overridden; it doesn't compare values.
* Remember that chained methods are evaluated from left to right.
* **String methods** to remember: `charAt()`, `concat()`, `equalsIgnoreCase()`, `length()`, `replace()`, `substring()`, `toLowerCase()`, `toString()`, `toUpperCase()`, and `trim()`.
* **StringBuffer methods** to remember: `append()`, `delete()`, `insert()`, `reverse()`, and `toString()`.

### Q11. How would you defensively copy a Date field in your immutable class?

```java
public final class MyDiary {
  private Date myDate = null;
  
  public MyDiary(Date aDate){
    this.myDate = new Date(aDate.getTime()); // defensive copying by not exposing the “myDate” reference
  }
  
  public Date getDate() {
    return new Date(myDate.getTime); // defensive copying by not exposing the “myDate” reference
  }
}
```

### Q12. What is the main difference between pass-by-reference and pass-by-value? 
Other languages use pass-by-reference or pass-by-pointer. But in **Java no matter what type of argument you pass the corresponding parameter (primitive variable or object reference) will get a copy of that data, which is exactly how pass-by-value (i.e. copy-by-value) works.**

In Java, if a calling method passes a reference of an object as an argument to the called method then the **passedin reference gets copied first** and then passed to the called method. **Both the original reference that was passed-in and the copied reference will be pointing to the same object. So no matter which reference you use, you will be always modifying the same original object, which is how the pass-by-reference works as well.**

### Q12. What is the difference between an instance variable and a static variable? How does a local variable compare to an instance or a static variable? Give an example where you might use a static variable?

* The lifetime of a **local variable** is determined by execution path and local variables are also known as stack variables because they live on the **stack.**
* For a local variable, it is illegal for code to fail to assign it a value. It is the best practice to declare local variables only where required as opposed to declaring them upfront and cluttering up your code with some local variables that never get used.

* **Instance and static variables** are associated with objects and therefore live in the **heap.**
* Both the static and instance variables always have a value. If your code does not assign them a value then the run-time system will implicitly assign a default value (e.g.null/0/0.0/false).

Static Variables and Methods
* They are not tied to any particular instance of a class.
* No classes instances are needed in order to use static members of the class.
* There is only one copy of a static variable / class and all instances share it.
* static methods do not have direct access to non-static members.

Local Variables 
* Local (method, automatic, or stack) variable declarations cannot have access modifiers.
* final is the only modifier available to local variables.
* Local variables don't get default values, so they must be initialized before use.

Variable Declarations 
* Instance variables can
    * Have any access control
    * Be marked final or transient
* Instance variables can't be abstract, synchronized, native, or strictfp.
* It is legal to declare a local variable with the same name as an instance variable; this is called "shadowing."
* **final variables** have the following properties:
    * final variables cannot be reinitialized once assigned a value.
    * final reference variables cannot refer to a different object once the object has been assigned to the final variable.
    * final reference variables must be initialized before the constructor completes.
* There is no such thing as a `final` object. An object reference marked final does not mean the object itself is immutable.
* The `transient` modifier applies only to instance variables.
* The `volatile` modifier applies only to instance variables.
* `volatile` means : The value of this variable will never be cached thread-locally: all reads and writes will go straight to "main memory"; Access to the variable acts as though it is enclosed in a synchronized block, synchronized on itself.
* the volatile modifier guarantees that any thread that reads a field will see the most recently written value.

### Q13. Give an example where you might use a static method?
Static methods prove useful for creating utility classes, singleton classes and factory methods

### Q14. What are access modifiers?
![alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Java/images/access.png "class object")

Default and protected members differ only when subclasses are involved:
  * `Default members` can be accessed only by classes in the same package.
  * `protected members` can be accessed by other classes in the same package, plus subclasses regardless of package.
  * `protected` = **package plus kids (kids meaning subclasses).**
  * For subclasses outside the package, the protected member can be accessed only through inheritance; a subclass outside the package cannot access a protected member by using a reference to a superclass instance (in other words, inheritance is the only mechanism for a subclass outside the package to access a protected member of its superclass).
  * A protected member inherited by a subclass from another package is not accessible to any other class in the subclass package, except for the subclass' own subclasses.

### Q15.What is a final modifier? Explain other Java modifiers?
![alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Java/images/modifiers.png "class object")

The **volatile modifier** is used on instance variables that may be modified simultaneously by other threads. The modifier volatile only synchronizes the variable marked as volatile whereas `synchronized` modifier synchronizes all variables. Since other threads cannot see local variables, there is no need to mark local variables as volatile.

### Q16. What is the difference between final, finally and finalize() in Java?
* **final -** constant declaration. 
* **finally -** handles exception. The finally block is optional and provides a mechanism to clean up regardless of what happens within the try block (except System.exit(0) call). Use the finally block to close files or to release other system resources like database connections, statements etc.
* **finalize() -** method helps in garbage collection. A method that is invoked before an object is discarded by the garbage collector, allowing it to clean up its state. Should not be used to release non-memory resources like file handles, sockets, database connections etc because Java has only a finite number of these resources and you do not know when the garbage collection is going to kick in to release these non-memory resources through the finalize() method. 

### Q17. What is type casting? Explain up casting vs. down casting? When do you get ClassCastException?
Type casting means treating a variable of one type as though it is another type.

When up casting primitives as shown below from left to right, automatic conversion occurs. But if you go from right to left, down casting or explicit casting is required. Casting in Java is safer than in C or other languages that allow arbitrary casting. Java only lets casts occur when they make sense, such as a cast between a float and an int. However you can't cast between an int and a String (is an object in Java).

byte -> short -> int -> long -> float -> double
* int i = 5;
* long j = i; //Right. Up casting or implicit casting
* byte b1 = i; //Wrong. Compile time error “Type Mismatch”.
* byte b2 = (byte) i ; //Right. Down casting or explicit casting is required.

When it comes to object references **you can always cast from a subclass to a superclass because a subclass object is also a superclass object.** You can cast an object implicitly to a super class type (i.e. upcasting). If this were not the case polymorphism wouldn’t be possible.

```java
Vehicle v1 = new Car(); //Right.upcasting or implicit casting
Vehicle v2 = new Vehicle();
Car c0 = v1; //Wrong. compile time error "Type Mismatch".
//Explicit or down casting is required
Car c1 = (Car)v1; // Right. down casting or explicit casting.
// v1 has knowledge of Car due to line1
Car c2 = (Car)v2; //Wrong. Runtime exception ClassCastException
//v2 has no knowledge of Car.
Bus b1 = new BMW(); //Wrong. compile time error "Type Mismatch"
Car c3 = new BMW(); //Right.upcasting or implicit casting
Car c4 = (BMW)v1; //Wrong. Runtime exception ClassCastException
Object o = v1; //v1 can only be upcast to its parent or
Car c5 = (Car)v1; //v1 can be down cast to Car due to line 1.
```

You can cast down the hierarchy as well but you must explicitly write the cast and the object must be a legitimate instance of the class you are casting to. The `ClassCastException` is thrown to indicate that code has attempted to cast an object to a subclass of which it is not an instance. If you are using J2SE 5.0 then `generics` will eliminate the need for casting and otherwise you can deal with the problem of incorrect casting in two ways:
* Use the exception handling mechanism to catch ClassCastException.

```java
try{
  Object o = new Integer(1);
  System.out.println((String) o);
}
catch(ClassCastException cce) {
  logger.log(“Invalid casting, String is expected…Not an Integer”);
  System.out.println(((Integer) o).toString());
}
```

* Use the instanceof statement to guard against incorrect casting.

```java
if(v2 instanceof Car) {
  Car c2 = (Car) v2;
}
```

### Q18. What do you know about the Java garbage collector? When does the garbage collection occur? Explain different types of references in Java?
Each time an object is created in Java, it goes into the area of memory known as heap. The Java heap is called the garbage collectable heap. The garbage collection cannot be forced. **The garbage collector runs in low memory situations.** When it runs, it releases the memory allocated by an unreachable object. **The garbage collector runs on a low priority daemon** (i.e. background) thread. 
You can nicely ask the garbage collector to collect garbage by calling **System.gc()** but you can’t force it.

Explain types of references in Java? java.lang.ref package can be used to declare soft, weak and phantom references.
* Garbage Collector won’t remove a strong reference.
* A **soft reference** will only get removed if memory is low. So it is useful for implementing caches while avoiding memory leaks.
* A **weak reference** will get removed on the next garbage collection cycle. Can be used for implementing canonical maps. The `java.util.WeakHashMap` implements a `HashMap` with keys held by weak references.
* A **phantom reference** will be finalized but the memory will not be reclaimed. Can be useful when you want to be notified that an object is about to be collected.




<br>
<br>

## Serialization

* The classes you need to understand are all in the `java.io` package; they include: `ObjectOutputStream` and `ObjectInputStream` primarily, and `FileOutputStream` and `FileInputStream` because you will use them to create the low-level streams that the ObjectXxxStream classes will use.
* A class must implement Serializable before its objects can be serialized.
* The `ObjectOutputStream.writeObject()` method serializes objects, and the `ObjectInputStream.readObject()` method deserializes objects.
* If you mark an instance variable `transient`, it will not be serialized even thought the rest of the object's state will be.
* You can supplement a class's automatic serialization process by implementing the `writeObject()` and `readObject()` methods. If you do this, embedding calls to `defaultWriteObject()` and `defaultReadObject()`, respectively, will handle the part of serialization that happens normally.
* If a superclass implements Serializable, then its subclasses do automatically.
* If a superclass doesn't implement Serializable, then when a subclass object is deserialized, the superclass constructor will be invoked, along with its superconstructor(s).
* `DataInputStream` and `DataOutputStream`.

### Q1. What is serialization? How would you exclude a field of a class from serialization or what is a transient variable? What is the common use? What is a serial version id?

`Serialization` is a process of reading or writing an object. It is a process of saving an object’s state to a sequence of bytes, as well as a process of rebuilding those bytes back into a live object at some future time. An object is marked serializable by implementing the `java.io.Serializable` interface, which is only a marker interface -- it simply allows the serialization mechanism to verify that the class can be persisted, typically to a file.

`Transient` variables cannot be serialized. The fields marked transient in a serializable object will not be transmitted in the byte stream. An example would be a file handle, a database connection, a system thread etc. Such objects are only meaningful locally. So they should be marked as transient in a serializable class.

![alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Java/images/serialization.png "class object")

#### Q. When to use serialization? 
Do not use serialization if you do not have to. **A common use of serialization is to use it to send an object over the network or if the state of an object needs to be persisted to a flat file or a database.** Deep cloning or copy can be achieved through serialization. This may be fast to code but will have performance implications.

To serialize the above “Car” object to a file (sample for illustration purpose only, should use try {} catch {} block):

```java
Car car = new Car(); // The “Car” class implements a java.io.Serializable interface
FileOutputStream fos = new FileOutputStream(filename);
ObjectOutputStream out = new ObjectOutputStream(fos);
out.writeObject(car); // serialization mechanism happens here
out.close();
```

The objects stored in an HTTP session should be serializable to support in-memory replication of sessions to achieve scalability (Refer Q20 in Enterprise section). Objects are passed in RMI (Remote Method Invocation) across network using serialization (Refer Q57 in Enterprise section).

#### Q. What is Java Serial Version ID? 
Say you create a “Car” class, instantiate it, and write it out to an object stream. The flattened car object sits in the file system for some time. Meanwhile, if the “Car” class is modified by adding a new field. Later on, when you try to read (i.e. deserialize) the flattened “Car” object, you get the `java.io.InvalidClassException` – because all serializable classes are automatically given a unique identifier. This exception is thrown when the identifier of the class is not equal to the identifier of the flattened object. If you really think about it, the exception is thrown because of the addition of the new field. You can avoid this exception being thrown by controlling the versioning yourself by declaring an explicit `serialVersionUID`. There is also a small performance benefit in explicitly declaring your serialVersionUID (because does not have to be calculated). So, it is best practice to add your own serialVersionUID to your Serializable classes as soon as you create them as shown below:

```java
public class Car {
  static final long serialVersionUID = 1L; //assign a long value
}
```

### Q2 Explain the Java I/O streaming concept and the use of the decorator design pattern in Java I/O?
Java input and output is defined in terms of an abstract concept called a `stream`, which is a sequence of data.
There are 2 kinds of streams.
* **Byte streams (8 bit bytes)** - Abstract classes are: InputStream and OutputStream
* **Character streams (16 bit UNICODE)** - Abstract classes are: Reader and Writer

**Design pattern:** `java.io.*` classes use the decorator design pattern. **The decorator design pattern attaches responsibilities to objects at runtime.** Decorators are more flexible than inheritance because the inheritance attaches responsibility to classes at compile time. The `java.io.*` classes use the decorator pattern to construct different combinations of behavior at runtime based on some basic classes.

#### Attaching responsibilities to classes at compile time using subclassing.
`Inheritance` (aka subclassing) attaches responsibilities to classes at compile time. When you extend a class, each individual changes you make to child class will affect all instances of the child classes. Defining many classes using inheritance to have all possible combinations is problematic and inflexible.

#### Attaching responsibilities to objects at runtime using a decorator design pattern.
By attaching responsibilities to objects at runtime, you can apply changes to each individual object you want to change.

```java
File file = new File(“c:/temp”);
FileInputStream fis = new FileInputStream(file);
BufferedInputStream bis = new BufferedInputStream(fis);
```

Decorators decorate an object by enhancing or restricting functionality of an object it decorates. The decorators add or restrict functionality to decorated objects either before or after forwarding the request. At runtime the `BufferedInputStream (bis)`, which is a decorator (aka a wrapper around decorated object), forwards the method call to its decorated object `FileInputStream (fis)`. The `bis` will apply the additional functionality of buffering around the lower level file (i.e. fis) I/O.


![alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Java/images/javaIO.png "class object")

### Q3. How does the new I/O (NIO) offer better scalability and better performance?
Java has long been not suited for developing programs that perform a lot of I/O operations. Furthermore, **commonly needed tasks such as file locking, non-blocking and asynchronous I/O operations and ability to map file to memory were not available.** 
**Non-blocking I/O operations were achieved through work around such as multithreading or using JNI.** The New I/O API (aka NIO) in J2SE 1.4 has changed this situation. 

A server’s ability to handle several client requests effectively depends on how it uses I/O streams. When a server has to handle hundreds of clients simultaneously, it must be able to use I/O services concurrently. One way to cater for this scenario in Java is to use threads but having almost one-to-one ratio of threads (100 clients will have 100 threads) is prone to enormous thread overhead and can result in performance and scalability problems due to consumption of memory stacks (i.e. each thread has its own stack.) and CPU context switching (i.e. switching between threads as opposed to doing real computation.). 

To overcome this problem, a new set of non-blocking I/O classes have been introduced to the Java platform in `java.nio package`. **The non-blocking I/O mechanism is built around Selectors and Channels.** 
**Channels, Buffers and Selectors are the core of the NIO.**

![alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Java/images/nio.png "class object")

A **Channel** class represents a bi-directional communication channel (similar to InputStream and OutputStream) between datasources such as a socket, a file, or an application component, which is capable of performing one or more I/O operations such as reading or writing. Channels can be non-blocking, which means, no I/O operation will wait for data to be read or written to the network. The good thing about NIO channels is that they can be asynchronously interrupted and closed. So if a thread is blocked in an I/O operation on a channel, another thread can interrupt that blocked thread.

A **Selector** class enables multiplexing (combining multiple streams into a single stream) and demultiplexing (separating a single stream into multiple streams) I/O events and makes it possible for a single thread to efficiently manage many I/O channels. A Selector monitors selectable channels, which are registered with it for I/O events like connect, accept, read and write. The keys (i.e. Key1, Key2 etc represented by the SelectionKey class) encapsulate the relationship between a specific selectable channel and a specific selector.

**Buffers** hold data. Channels can fill and drain Buffers. Buffers replace the need for you to do your own buffer management using byte arrays. There are different types of Buffers like ByteBuffer, CharBuffer, DoubleBuffer, etc.

`Design pattern`: NIO uses a **reactor design pattern**, which demultiplexes events (separating single stream into multiple streams) and dispatches them to registered object handlers. The **reactor pattern is similar to** an **observer pattern (aka publisher and subscriber design pattern),** but an **observer pattern handles only a single source of events** (i.e. a single publisher with multiple subscribers) where a reactor pattern handles multiple event sources (i.e. multiple publishers with multiple subscribers). The intent of an observer pattern is to define a one-to-many dependency so that when one object (i.e. the publisher) changes its state, all its dependents (i.e. all its subscribers) are notified and updated correspondingly.

Another feature of NIO is its ability to lock and unlock files. Locks can be exclusive or shared and can be held on a contiguous portion of a file. But file locks are subject to the control of the underlying operating system.

### Q4. How can you improve Java I/O performance?
Java applications that utilize Input/Output are excellent candidates for performance tuning. Profiling of Java applications that handle significant volumes of data will show significant time spent in I/O operations. This means substantial gains can be had from I/O performance tuning. Therefore, I/O efficiency should be a high priority for developers looking to optimally increase performance.

The basic rules for speeding up I/O performance are
* Minimize accessing the hard disk.
* Minimize accessing the underlying operating system.
* Minimize processing bytes and characters individually.

1. Use **buffering** to minimize disk access and underlying operating system. As shown below, with buffering large chunks of a file are read from a disk and then accessed a byte or character at a time.

```java
// With Buffering: yields better performance
try{
  File f = new File("myFile.txt");
  FileInputStream fis = new FileInputStream(f);
  BufferedInputStream bis = new BufferedInputStream(fis);
  int count = 0;
  int b = 0 ;
  while((b = bis.read()) != -1){
    if(b== '\n') {
      count++;
    }
  }
  //bis should be closed in a finally block.
  bis.close() ;
}
catch(IOException io){}

// Note: bis.read() takes the next byte from the input buffer and only rarely access the underlying operating system.
```
2. Use the **NIO package**, if you are using JDK 1.4 or later, which uses performance-enhancing features like buffers to hold data, memory mapping of files, non-blocking I/O operations etc.
3.  I/O performance can be improved by minimizing the calls to the underlying operating systems. The Java runtime itself cannot know the length of a file, querying the file system for isDirectory(), isFile(), exists() etc must query the underlying operating system.
4.  Where applicable caching can be used to improve performance by reading in all the lines of a file into a Java Collection class like an ArrayList or a HashMap and subsequently access the data from an in-memory collection instead of the disk.









<br>
<br>

## Collections 

![alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Java/images/Collection-Classes.png "class object")

![alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Java/images/Collection-Classes_Map.png "class object")

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

* Underlying Data structure is Hashtable.
* ConcurrentHashmap allows Concurrent Read and Thread Safe Update Operations.
* To Perform Read Operations thread won't require any lock. But to perform update operration thread requires lock but it is lock of only a particular part of Map (Bucket level lock)
* Instead of whole map concurrent update achieved by internally dividing Mao into smaller portion which is defined by Concurrency level.
* The default concurrency level is 16.
* That is concurrenthashmap allows simultaneous read operations and simultaneously 16 write(update) operations.
* Null is not allowed for both Keys and Values.
* While one thread iterating the other thread can perform update operation and concurrentHashMap Never throw **ConcurrentModificationException**


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

<br>
<br>

### 4. How HashSet and LinkedHashSet works?

![alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Java/images/HowHashSetWorks.png "class object")

![alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Java/images/HowLinkedHashSetWorks.png "class object")



<br>
<br>

## Exception Hadling

### Q1. Discuss the Java error handling mechanism? What is the difference between Runtime (unchecked) exceptionsand checked exceptions? What is the implication of catching all the exceptions with the type “Exception”?
**Errors:**
When a dynamic linking failure or some other “hard” failure in the virtual machine occurs, the virtual machine throws an Error. Typical Java programs should not catch Errors. In addition, it’s unlikely that typical Java programs will ever throw Errors either.

**Exceptions:**
Most programs throw and catch objects that derive from the Exception class. Exceptions indicate that a problem occurred but that the problem is not a serious JVM problem. An Exception class has many subclasses. These descendants indicate various types of exceptions that can occur. 

For example, **NegativeArraySizeException** indicates that a program attempted to create an array with a negative size. One exception subclass has special meaning in the Java language: RuntimeException. **All the exceptions except RuntimeException are compiler checked exceptions. If a method is capable of throwing a checked exception it must declare it in its method header or handle it in a try/catch block. Failure to do so raises a compiler error.** So checked exceptions can, at compile time, greatly reduce the occurrence of unhandled exceptions surfacing at runtime in a given application at the expense of requiring large throws declarations and encouraging use of poorlyconstructed try/catch blocks. Checked exceptions are present in other languages like C++, C#, and Python.

![alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Java/images/exception.png "class object")

#### Runtime Exceptions (unchecked exception)
A RuntimeException class represents exceptions that occur within the Java virtual machine (during runtime). An example of a runtime exception is **NullPointerException**. The cost of checking for the runtime exception often outweighs the benefit of catching it. Attempting to catch or specify all of them all the time would make your code unreadable and unmaintainable. The compiler allows runtime exceptions to go uncaught and unspecified. If you like, you can catch these exceptions just like other exceptions. However, you do not have to declare it in your `throws` clause or catch it in your catch clause. In addition, you can create your own RuntimeException subclasses and this approach is probably preferred at times because checked exceptions can complicate method signatures and can be difficult to follow.

#### Q. Why should you throw an exception early?
The exception stack trace helps you pinpoint where an exception occurred by showing you the exact sequence of method calls that lead to the exception. By throwing your exception early, the exception becomes more accurate and more specific. Avoid suppressing or ignoring exceptions. Also avoid using exceptions just to get a flow control.

```java
// Instead of
// assume this line throws an exception because filename == null.
InputStream in = new FileInputStream(fileName);
…

//Use the following code because you get a more accurate stack trace:
if(filename == null) {
  throw new IllegalArgumentException(“file name is null”);
}
InputStream in = new FileInputStream(fileName);
```

#### Q. Why should you catch a checked exception late in a catch {} block?
You should not try to catch the exception before your program can handle it in an appropriate manner. The natural tendency when a compiler complains about a checked exception is to catch it so that the compiler stops reporting errors. **It is a bad practice to sweep the exceptions under the carpet by catching it and not doing anything with it.** The best practice is to catch the exception at the appropriate layer (e.g. an exception thrown at an integration layer can be caught at a presentation layer in a catch {} block), where your program can either meaningfully recover from the exception and continue to execute or log the exception only once in detail, so that user can identify the cause of the exception.

#### Q. When should you use a checked exception and when should you use an unchecked exception?
Due to heavy use of checked exceptions and minimal use of unchecked exceptions, there has been a hot debate in the Java community regarding true value of checked exceptions. **Use checked exceptions when the client code can take some useful recovery action based on information in exception. Use unchecked exception when client code cannot do anything.**

`For example` Convert your `SQLException` into another checked exception if the client code can recover from it. Convert your `SQLException` into an unchecked (i.e. `RuntimeException`) exception, if the client code can not recover from it. (Note: Hibernate 3 & Spring uses RuntimeExceptions prevalently).

**A note on key words for error handling:**
* **throw / throws** – used to pass an exception to the method that called it.
* **try –** block of code will be tried but may cause an exception.
* **catch –** declares the block of code, which handles the exception.
* **finally –** block of code, which is always executed (except System.exit(0) call) no matter what program flow, occurs when dealing with an exception.
* **assert –**  Evaluates a conditional expression to verify the programmer’s assumption.

### Q2. What is a user defined exception?
User defined exceptions may be implemented by defining a new exception class by extending the `Exception` class.

```java
public class MyException extends Exception {
  /* class definition of constructors goes here */
  public MyException() {
    super();
  }
  public MyException (String errorMessage) {
    super (errorMessage);
  }
}
```

* Throw and/or throws statement is used to signal the occurrence of an exception. To throw an exception:

```java
throw new MyException(“I threw my own exception.”)
```

* To declare an exception: 

```java
public myMethod() throws MyException {…}
```


![alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Java/images/exception1.png "class object")

#### Handling Exceptions 

* Exceptions come in two flavors: **checked** and **unchecked**.
* **Checked exceptions** include all **subtypes of Exception, excluding classes that extend RuntimeException.**
* **Checked exceptions** are subject to the handle or declare rule; any method that might throw a checked exception (including methods that invoke methods that can throw a checked exception) must either declare the exception using throws, or handle the exception with an appropriate try/catch.
* **Subtypes of Error or RuntimeException** are **unchecked**, so the compiler doesn't enforce the handle or declare rule. You're free to handle them, or to declare them, but the compiler doesn't care one way or the other.
* If you use an optional finally block, it will always be invoked, regardless of whether an exception in the corresponding try is thrown or not, and regardless of whether a thrown exception is caught or not.
* The only exception to the finally-will-always-be-called rule is that a finally will not be invoked if the JVM shuts down. That could happen if code from the try or catch blocks calls System.exit().
* Just because finally is invoked does not mean it will complete. Code in the finally block could itself raise an exception or issue a **System.exit()**.
* Uncaught exceptions propagate back through the call stack, starting from the method where the exception is thrown and ending with either the first method that has a corresponding catch for that exception type or a JVM shutdown (which happens if the exception gets to main(), and main() is `ducking` the exception by declaring it).
* You can create your **own exceptions**, normally by extending Exception or one of its subtypes. Your exception will then be considered a **checked exception**, and the **compiler will enforce the handle or declare rule for that exception.**
* All catch blocks must be ordered from most specific to most general. If you have a catch clause for both IOException and Exception, you must put the catch for IOException first in your code. Otherwise, the IOException would be caught by catch(Exception e), because a catch argument can catch the specified exception or any of its subtypes! The compiler will stop you from defining catch clauses that can never be reached.
* Some exceptions are created by programmers, some by the JVM.













