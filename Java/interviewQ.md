### 1. What are immutable objects? What are the advantages of these objects?
Immutability is often presented as a key concept of functional programming. In order to get the benefits of immutability in Java we can use the following guidelines while programming -

* Mark the class final
* Mark all the fields private and final
* Force all the callers to construct an object of the class directly, i.e. do not use any setter methods
* Do not change the state of the objects in any methods of the class

**Advantages:**
* Immutable objects are thread-safe so you will not have any synchronization issues.
* Immutable objects are good Map keys and Set elements, since these typically do not change once created.
* Immutability makes it easier to write, use and reason about the code (class invariant is established once and then unchanged)
* Immutability makes it easier to parallelize your program as there are no conflicts among objects.
* The internal state of your program will be consistent even if you have exceptions.
* References to immutable objects can be cached as they are not going to change.

As a good programming practice in Java one should try to use immutable objects as far as possible. Immutability can have a performance cost, since when an object cannot be mutated we need to copy it if we want to write to it. When you care a lot about performance (e.g. programming a game) it may be necessary to use a mutable object. Even then it is often better to try to limit the mutability of objects.

<br>
<br>

### 2. How would you write a constructor for an immutable class person with fields name and DOB?
```java
public final class Contacts {

    private final String name;
    private final Date dob;

    public Contacts(String name, Date dob) {
        this.name = name;
        this.dob = dob;
    }
  
    public String getName(){
        return name;
    }
  
    public String getDob(){
        return dob;
    }
}
```

<br>
<br>

### 3. What are daemon threads?
Daemon thread in java can be useful to run some tasks in background. An example for a daemon thread is the garbage collection.

When a thread is marked as daemon thread, JVM doesn’t wait it to finish to terminate the program. As soon as all the user threads are finished, JVM terminates the program as well as all the associated daemon threads.

`Thread.setDaemon(true)` is used to create a daemon thread in java. This method should be invoked before the thread is started otherwise it will throw `IllegalThreadStateException`.

We can check if a thread is daemon thread or not by calling `isDaemon()` method on it.

Another point is that when a thread is started, it inherits the daemon status of it’s parent thread.
```java
package com.journaldev.threads;

public class JavaDaemonThread {

    public static void main(String[] args) throws InterruptedException {
        Thread dt = new Thread(new DaemonThread(), "dt");
        dt.setDaemon(true);
        dt.start();
        //continue program
        Thread.sleep(30000);
        System.out.println("Finishing program");
    }

}

class DaemonThread implements Runnable{

    @Override
    public void run() {
        while(true){
            processSomething();
        }
    }
    
    private void processSomething() {
        try {
            System.out.println("Processing daemon thread");
            Thread.sleep(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
    
}
```
When we execute above daemon thread program, JVM creates first user thread with main() method and then a daemon thread.

When main method is finished, the program terminates and daemon thread is also shut down by JVM.

**Daemon Thread Usage**
Usually we create a daemon thread for functionalities that are not critical to system. For example logging thread or monitoring thread to capture the system resource details and their state. If you are not okay will a thread being terminated, don’t create it as a daemon thread.

<br>
<br>

### 4. Explain the use of executor framework in multithreading?
* Executors service is created using one of the factory methods.
* Runnable argument is passed to the execute method of executor service.
* Executor service will execute it in parallel.
* Finally it will shutdown using 'shutdown()'.

Two implementations:
1. ThreadPoolExecutors
2. ScheduledThreadPoolExecutors

```java
Executors.newSingleThreadExecutor()
```
All threads passed with this will execute with single thread. One task ata atime sequentially

```java
Executors.newFixedThreadPool(10)
```
Fixed number of threads. All thaks will be executed with one of these threads.

```java
Executors.newScheduledThreadPool(10);
```
Schedule the execution of the task passed to it.

1. execute(Runnable)
2. submit(Runnable)
3. submit(Callable)
4. invokeAny()
5. invokeAll()

* submit will return future object 
* `future.get()` return null if the task has finished correctly.
* callable will be capable of returning object.


<br>
<br>

### 5. What is the difference between callable and runnable interface?
The Callable interface is similar to Runnable, in that both are designed for classes whose instances are potentially executed by another thread. A Runnable, however, does not return a result and cannot throw a checked exception.


<br>
<br>

### 6. What are the major differences between ArrayList and LinkedList?
Main difference between ArrayList and LinkedList is that ArrayList is implemented using re sizable array while LinkedList is implemented using doubly LinkedList. ArrayList is more popular among Java programmer than LinkedList as there are few scenarios on which LinkedList is a suitable collection than ArrayList. In this article we will see some differences between LinkedList and ArrayList and try to find out when and where to use LinkedList over ArrayList.

1) Since Array is an index based data-structure searching or getting element from Array with index is pretty fast. Array provides O(1) performance for get(index) method but remove is costly in ArrayList as you need to rearrange all elements. On the Other hand LinkedList doesn't provide Random or index based access and you need to iterate over linked list to retrieve any element which is of order O(n).

2) Insertions  are easy and fast in LinkedList as compared to ArrayList because there is no risk of resizing array
and copying content to new array if array gets full which makes adding into ArrayList of O(n) in worst case, while adding is O(1) operation in LinkedList in Java. ArrayList also needs to update its index if you insert something anywhere except at the end of array.

3) Removal is like insertions better in LinkedList than ArrayList.

4) LinkedList has more memory overhead than ArrayList because in ArrayList each index only holds actual object (data) but in case of LinkedList each node holds both data and address of next  and previous node.

**When to use LinkedList and ArrayList in Java**

As I said LinkedList is not as popular as ArrayList but still there are situation where a LinkedList is better choice than ArrayList in Java. Use LinkedList in Java if:

1) Your application can live without Random access. Because if you need nth element in LinkedList you need to first traverse up to nth element O(n) and than you get data from that node.

2) Your application is more insertion and deletion driver and you insert or remove more than retrieval. Since insertion or
removal doesn't involve resizing its much faster than ArrayList.

That’s all on difference between ArrayList and LinkedList in Java. Use ArrayList in Java for all there situation where you need a non-synchronized index based access. ArrayList is fast and easy to use, just try to minimize array resizing by constructing arraylist with proper initial size


<br>
<br>

### 7. What is the difference between LinkedList and doublyLinkedList?
`java.util.LinkedList` is a doubly-linked list.

All of the operations perform as could be expected for a doubly-linked list.
You can create it by passing the array list as constructor argument:
```java
List linkedList = new LinkedList(arrayList);
```
Update: The `java.util.LinkedList` has `add(index, element)` which, combined with `indexOf(..)` should cover the `addBefore` and `addAfter` methods. You can extend LinkedList to add these convenient methods if you like.

<br>
<br>

### 8. How do the keys operate in a HashMap?
 
<br>
<br>

### 9. How will you implement sorting logic in ArrayList? Array List contains custom type objects.
```java
package collections.framework;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class C7_SortingListsComparator {

	public static void main(String[] args) {
		////////////////////// Sorting Strings ////////////////////////////////
		List<String> animals = new ArrayList<String>();

		animals.add("tiger");
		animals.add("lion");
		animals.add("cat");
		animals.add("snake");
		animals.add("mongoose");
		animals.add("elephant");

		// Collections.sort(animals, new StringLengthComparator());
		Collections.sort(animals, new ReverseAlphabeticalComparator());

		for (String animal : animals) {
			System.out.println(animal);
		}

		////////////////////// Sorting Numbers ////////////////////////////////
		List<Integer> numbers = new ArrayList<Integer>();

		numbers.add(3);
		numbers.add(36);
		numbers.add(73);
		numbers.add(40);
		numbers.add(1);

		Collections.sort(numbers, new Comparator<Integer>() {
			public int compare(Integer num1, Integer num2) {
				return -num1.compareTo(num2);
			}
		});

		for (Integer number : numbers) {
			System.out.println(number);
		}

		////////////////////// Sorting arbitary objects  ////////////////////////////////

		List<Human> human = new ArrayList<Human>();

		human.add(new Human(1, "Joe"));
		human.add(new Human(3, "Bob"));
		human.add(new Human(4, "Clare"));
		human.add(new Human(2, "Sue"));

		// Sort in order of ID
		Collections.sort(human, new Comparator<Human>() {
			public int compare(Human p1, Human p2) {

				if (p1.getId() > p2.getId()) {
					return 1;
				} else if (p1.getId() < p2.getId()) {
					return -1;
				}

				return 0;
			}
		});

		for (Human person : human) {
			System.out.println(person);
		}

		System.out.println("/n");
		// Sort in order of name
		Collections.sort(human, new Comparator<Human>() {
			public int compare(Human p1, Human p2) {
				return p1.getName().compareTo(p2.getName());
			}
		});

		for (Human person : human) {
			System.out.println(person);
		}

	}

}

class Human {
	private int id;
	private String name;

	public Human(int id, String name) {
		this.id = id;
		this.name = name;
	}

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String toString() {
		return id + ": " + name;
	}
}

class StringLengthComparator implements Comparator<String> {

	@Override
	public int compare(String s1, String s2) {

		int len1 = s1.length();
		int len2 = s2.length();

		if (len1 > len2) {
			return 1;
		} else if (len1 < len2) {
			return -1;
		}

		return 0;
	}
}

class ReverseAlphabeticalComparator implements Comparator<String> {

	@Override
	public int compare(String s1, String s2) {
		return -s1.compareTo(s2);
	}
}



/*
tiger
snake
mongoose
lion
elephant
cat
73
40
36
3
1
1: Joe
2: Sue
3: Bob
4: Clare
/n
3: Bob
4: Clare
1: Joe
2: Sue

 */
```

<br>
<br>

### 10. HashMap example, where he adds null key to the map. Question was if it will get compiled?
HashMap supports both null keys and values

<br>
<br>

### 11. How will you implement AbstractFactory Design Pattern?
<br>
<br>

### 12. Will a singleton pattern work in a multi clustered environment?
Distributed Singleton Caches

<br>
<br>

### 13. What are the concurrent in the collection classes?
Java Concurrent Collection Classes

* **BlockingQueue** – an interface that is at the base of all Queue based concurrent collections. While adding an element to a BlockingQueue, if there is no space it can wait till it becomes available and when retrieving, it will wait till an element is available if it is empty.
* **ArrayBlockingQueue** – a blocking queue class based on bounded Java Array. Once instantiated, cannot be resized.
* **SynchronousQueue** – a blocking queue class with capacity of zero always.
* **PriorityBlockingQueue** – a priority queue based blocking queue. It is an unbounded concurrent collection.
* **LinkedBlockingQueue** – an optionally bounded Java concurrent collection. Orders elements based on FIFO order.
* **DelayQueue** – a queue where only delay expired elements can be taken out. Its an unbounded concurrent collection.
* **BlockingDeque** – an interface that extends BlockingQueue and adds the operations of Deque.
* **LinkedBlockingDeque** – an implementation class of BlockingDequeue.
* **TransferQueue** – a Java concurrent collection interface that extends BlockingQueue and adds method where the producer will wait for the consumer to receive elements.
* **LinkedTransferQueue** – an implementation class of TransferQueue.
* **ConcurrentMap** – a Java concurrent collection interface and a type of Map which provides thread safety and atomicity guarantees.
* **ConcurrentHashMap** – an implementation class of ConcurrentMap.
* **ConcurrentNavigableMap** – a Java concurrent collection interface that extends ConcurrentMap and adds operations of NavigableMap.
* **ConcurrentSkipListMap** – an implementation class of ConcurrentNavigableMap.
<br>
<br>

### 14. How will you handle unchecked exception in multi-threaded environment?
 We are talking about unchecked exceptions thrown from Thread.run method. By default, you will get sth like this in system error:
```java
Exception in thread "Thread-0" java.lang.RuntimeException
    at Main$1.run(Main.java:11)
    at java.lang.Thread.run(Thread.java:619)
```

This is the result of printStackTrace for unhandled exceptions. To handle it, you can add your own UncaughtExceptionHandler:
```java

Thread t = new Thread(new Runnable(){
        public void run() {
            throw new RuntimeException();
        }       
    });
   t.setUncaughtExceptionHandler(new Thread.UncaughtExceptionHandler() {

        public void uncaughtException(Thread t, Throwable e) {
            System.out.println("exception " + e + " from thread " + t);
        }
    });
    t.start();
```
To set handler for all threads use a static method `Thread.setDefaultUncaughtExceptionHandler`.
 
 
<br>
<br>

### 15. If the DBA's goofed up and forgot to mark the PK field as Primary Key and duplicate data gets loaded. How will you manage it?
 
<br>
<br>

### 16. Difference between collection and collections?
[Collection](java.sun.com/javase/6/docs/api/java/util/Collection.html) is a base interface for most collection classes, whereas [Collections](java.sun.com/javase/6/docs/api/java/util/Collections.html) is a utility class. I recommend you read the documentation.

<br>
<br>

### 17. Different classes in collection?
The entire collection framework is divided into four interfaces.

1) List  —> It handles sequential list of objects. ArrayList, Vector and LinkedList classes implement this interface.

2) Queue  —> It handles special list of objects in which elements are removed only from the head. LinkedList and PriorityQueue classes implement this interface.

3) Set  —> It handles list of objects which must contain unique element. This interface is implemented by HashSet and LinkedHashSet classes and extended by SortedSet interface which in turn, is implemented by TreeSet.

4) Map  —> This is the one interface in Collection Framework which is not inherited from Collection interface. It handles group of objects as Key/Value pairs. It is implemented by HashMap and HashTable classes and extended by SortedMap interface which in turn is implemented by TreeMap.

<br>
<br>

### 18. How to save a directory structure in java?
<br>
<br>

### 19. Spring different types of scope?
1. singleton(default*)
Scopes a single bean definition to a single object instance per Spring IoC container.

2. prototype
Scopes a single bean definition to any number of object instances.

3. request
Scopes a single bean definition to the lifecycle of a single HTTP request; that is each and every HTTP request will have its own instance of a bean created off the back of a single bean definition. Only valid in the context of a web-aware Spring ApplicationContext.

4. session
Scopes a single bean definition to the lifecycle of a HTTP Session. Only valid in the context of a web-aware Spring ApplicationContext.

5. global session
Scopes a single bean definition to the lifecycle of a global HTTP Session. Typically only valid when used in a portlet context. Only valid in the context of a web-aware Spring ApplicationContext.

<br>
<br>

### 20. What is the lifecycle of a bean?

1. Instantiation
2. Properties population
3. Call of `setBeanName()` method of `BeanNameAware`
4. Call of `setBeanFactory()` method of `BeanFactoryAware`
5. Call of `setApplicationContext()` of `ApplicationContextAware`
6. Pre-initialization with `BeanPostProcessor`
7. Call of `afterPropertiesSet()` method of InitializingBean
8. Custom `init` method
9. `Post-initialization` with `BeanPostProcessor`
10. Bean is ready to use
11. Call of `destroy()` method of `DisposableBean`
12. Custom destroy method
<br>
<br>

### 21. How to count different salary in database?
 
<br>
<br>

### 22. Advantages and disadvantages of using SOAP WebServices?
<br>
<br>

### 23. About Restful WebServices?
<br>
<br>

### 25. Explain about executor framework and future object?
<br>
<br>

### 27. Creating Immutable class?
To create immutable class in java, you have to do following steps.

1. Declare the class as final so it can’t be extended.
2. Make all fields private so that direct access is not allowed.
3. Don’t provide setter methods for variables
4. Make all mutable fields final so that it’s value can be assigned only once.
5. Initialize all the fields via a constructor performing deep copy.
6. Perform cloning of objects in the getter methods to return a copy rather than returning the actual object reference.

<br>
<br>

### 28. Is it possible to add new member variables in immutable class once created?
<br>
<br>

### 29. What is singleton class?
In object-oriented programming, a singleton class is a class that can have only one object (an instance of the class) at a time.
After first time, if we try to instantiate the Singleton class, the new variable also points to the first instance created. So whatever modifications we do to any variable inside the class through any instance, it affects the variable of the single instance created and is visible if we access that variable through any variable of that class type defined.
To design a singleton class:

* Make constructor as private.
* Write a static method that has return type object of this singleton class. Here, the concept of Lazy initialization in used to write this static method.

<br>
<br>

### 30. Can you access static variable from non-static methods?
* Instance methods can access instance variables and instance methods directly.
* Instance methods can access class variables and class methods directly.
* Class methods can access class variables and class methods directly.
* Class methods cannot access instance variables or instance methods directly—they must use an object reference. Also, class methods cannot use the this keyword as there is no instance for this to refer to.

So the answer is yes, non-static methods CAN modify static variables
<br>
<br>

### 31. Static vs singleton?
A singleton allows access to a single created instance - that instance (or rather, a reference to that instance) can be passed as a parameter to other methods, and treated as a normal object.

A static class allows only static methods.

<br>
<br>

### 32. When there are two elements having the same value 5 how will you remove from an ArrayList? Will it thrown an exception and what is it.?

```java
ArrayList<Integer> numbers = new ArrayList<Integer>();

// Adding
numbers.add(10);
numbers.add(100);
numbers.add(40);
numbers.add(5);
numbers.add(5);

// Retrieving
System.out.println(numbers.get(0)); // 10

numbers.remove(numbers.size() - 1); // 5 will be removed

// This is VERY slow
numbers.remove(0);
numbers.remove(new Integer(5)); // removes the first Integer object that is equal to the 5

for (Integer value : numbers) {
	System.out.println(value);
}
```		

If you don't want duplicates in a Collection, you should consider why you're using a Collection that allows duplicates. The easiest way to remove repeated elements is to add the contents to a Set (which will not allow duplicates) and then add the Set back to the ArrayList:
```java
List<String> al = new ArrayList<>();
// add elements to al, including duplicates
Set<String> hs = new HashSet<>();
hs.addAll(al);
al.clear();
al.addAll(hs);
```

Of course, this destroys the ordering of the elements in the ArrayList.

LinkedHashSet, if you wish to retain the order.

<br>
<br>

### 33. Pseudocode to remove element in Linked List?
 ```java
 public static void main(String[] args) {
	/*
	 * ArrayLists manage arrays internally. [0][1][2][3][4][5] ....
	 */
	List<Integer> arrayList = new ArrayList<Integer>();

	/*
	 * LinkedLists consists of elements where each element has a reference
	 * to the previous and next element [0]->[1]->[2] .... <- <-
	 */
	List<Integer> linkedList = new LinkedList<Integer>();

	//doTimings adds 200000 items
	doTimings("ArrayList", arrayList); // Time taken: 2858 ms for ArrayList
	doTimings("LinkedList", linkedList); // Time taken: 6 ms for LinkedList

	System.out.println(linkedList.size()); //200000
	System.out.println(arrayList.size()); //200000

	for(Iterator<Integer> iter = linkedList.iterator(); iter.hasNext();) {
	    int data = iter.next();
	    if (data == 25815) {
		    System.out.println(data);
		iter.remove();
		break;
	    }
	}
}
```
<br>
<br>

### 34. What is closure in JavaScript?
A closure is an inner function that has access to the outer (enclosing) function’s variables—scope chain. The closure has three scope chains: it has access to its own scope (variables defined between its curly brackets), it has access to the outer function’s variables, and it has access to the global variables.

The inner function has access not only to the outer function’s variables, but also to the outer function’s parameters. Note that the inner function cannot call the outer function’s arguments object, however, even though it can call the outer function’s parameters directly.
```js
function showName (firstName, lastName) {
var nameIntro = "Your name is ";
    // this inner function has access to the outer function's variables, including the parameter​
function makeFullName () {
	return nameIntro + firstName + " " + lastName;
}

return makeFullName ();
}
showName ("Michael", "Jackson"); // Your name is Michael Jackson 
```

<br>
<br>

### 35. What is prototype in JavaScript?
Every JavaScript object has a prototype. The prototype is also an object.

All JavaScript objects inherit their properties and methods from their prototype.

Objects created using an object literal, or with new Object(), inherit from a prototype called Object.prototype.

Objects created with new Date() inherit the Date.prototype.

The Object.prototype is on the top of the prototype chain.

All JavaScript objects (Date, Array, RegExp, Function, ....) inherit from the Object.prototype.

<br>
<br>

### 36. What is the difference between == and === in JavaScript?
 JavaScript has both strict and type-converting equality comparison. For strict equality the objects being compared must have the same type and:

* Two strings are strictly equal when they have the same sequence of characters, same length, and same characters in corresponding positions.
* Two numbers are strictly equal when they are numerically equal (have the same number value). NaN is not equal to anything, including NaN. Positive and negative zeros are equal to one another.
* Two Boolean operands are strictly equal if both are true or both are false.
* Two objects are strictly equal if they refer to the same Object.
* Null and Undefined types are == (but not ===). [I.e. (Null==Undefined) is true but (Null===Undefined) is false]

<br>
<br>

### 37. Thread?
Thread class provide constructors and methods to create and perform operations on a thread.Thread class extends Object class and implements Runnable interface.


<br>
<br>

### 38. Cyclicbarrier vs Countdown latch (some deep question on them)?
 CountDownLatch works in latch principle, main thread will wait until gate is open. One thread waits for n number of threads specified while creating CountDownLatch in Java.
 
 Any thread, usually main thread of application, which calls CountDownLatch.await() will wait until count reaches zero or its interrupted by another thread. All other thread are required to do count down by calling CountDownLatch.countDown() once they are completed or ready.
 
 As soon as count reaches zero, Thread awaiting starts running. One of the disadvantages/advantages of CountDownLatch is that it's not reusable once count reaches to zero you can not use CountDownLatch any more.
 
 Use CountDownLatch when one thread like main thread, requires to wait for one or more thread to complete, before it can start processing.
 
 Classical example of using CountDownLatch in Java is any server side core Java application which uses services architecture, where multiple services are provided by multiple threads and application can not start processing until all services have started successfully.
 
Features and some question on that
1. Collection
2. Collection that you have used other than ArrayList/HashMap/HashSet
3. Blocking queue
4. Comparable Vs Comparator
   
Few more question on comparator when to use what
1. Serialization 
2. What happens to final variables?
3. Class access levels, package private
4. Exceptions, custom exceptions, checked and runtime exception

Very generic question like have you worked on “Rest WebService”, “JQuery”, “Hibernate”, “EXT JS” and so on…
1. Various JavaScript frameworks that u have used, what is the difference between few of JavaScript frameworks
2. In Project, what level I have used these JavaScriptlibraries especially EXTJS
3. Since I have Bootstrap in my resume, few question on that
4. Declare global variable and override it in function? Is it possible?
5. What is Prototype?
6. Difference between JavaScript and Other frameworks (especially looking for function based approach in JS)
7. What is closure?
 
8. In Java, how do generate query without using the any of JDBC framework
9. Spring bean scope
10. Hibernate criteria
11. Caching Mechanism
<br>
<br>

### 12. When dealing with sensitive data, is it good to use string or array of char's. Why?
The biggest difference between the two is the way Garbage Collector(GC) handles each of the object. Since Strings are handled by Java Garbage Collector in a different way than the other traditional objects, it makes String less usable to store sensitive information.

So the main reasons to prefer char[] are:
1. IMMUTABILITY OF STRINGS.
Strings in Java are immutable(i.e. once created we can not change its value) and it also uses the String Pool concept for reusability  purpose, hence we are left with no option to clear it from the memory until GC clears it from the memory. Because of this there are great chances that the object created will remain in the memory for a long duration and we can’t even change its value. So anyone having access to the memory dump can easily retrieve the exact password from the memory. For this we can also use the encryption techniques so that if someone access then he will get the encrypted copy of the password.

But with character array you can yourself wipe out the data from the array and there would be no traces of password into the memory.
```java
public class PasswordSecurityExample {
 
    public static void main(String[] args) {
 
        char[] password = { 'p', 'a', 's', 's', 'w', 'o', 'r', 'd' };
 
        // Changing value of all characters in password
        for (int i = 0; i < password.length; i++) {
            password[i] = 'x';
        }
 
        System.out.print("New Password - ");
        // Priniting new Password
        for (int i = 0; i < password.length; i++) {
            System.out.print(password[i]);
        }
    }
// Output :
// New Password - xxxxxxxx
```
2. ACCIDENTAL PRINTING TO LOGS
```java
public class PasswordSecurityExample {
 
    public static void main(String[] args) {
 
        String password = "password";
        char[] password2;
 
        System.out.println("Printing String -> " + password);
 
        password2 = password.toCharArray();
        System.out.println("Printing Char Array -> " + password2);
    }
}
// Output:
// Printing String -> password
// Printing Char Array -> [C@21882d18
```
3. RECOMMENDATION BY JAVA ITSELF 

<br>
<br>
### 13. Which is better String s ="hello" or String s= new String ("hello")
Explain Strin pool concept

<br>
<br>

### 14. What are fast fail and fail safe iterators?
**Fail safe means**: it won't fail. Strictly speaking, there is no such thing in Java as a fail-safe iterator. The correct term is "weakly consistent".

Typically, weak consistency means that if a collection is modified concurrently with an iteration, the guarantees of what the iteration sees are weaker. (The details will be specified in each conncurrent collection classes javadocs.)

**Fail fast means**: it may fail ... and the failure condition is checked aggressively so that the failure condition is (where possible1) detected before damage can be done. In Java, a fail-fast iterator fails by throwing a ConcurrentModificationException.

The alternative to **fail-fast** and **weakly consistent** is a semantic where the iteration fails unpredictably; e.g. to sometimes give the wrong answer or throw a totally unexpected exception. (This was the behavior of some standard implementations of the Enumeration API in early versions of Java.)

The fail-fast iterators are typically implemented using a volatile counter on the collection object.

* When the collection is updated, the counter is incremented.
* When an Iterator is created, the current value of the counter is embedded in the Iterator object.
* When an Iterator operation is performed, the method compares the two counter values and throws a CME if they are different.

The implementation of fail-safe iterators is typically light-weight. They typically rely on properties of the specific list implementation's data structures. There is no general pattern. (Read the source code for the specific collection classes you are interested in.)

<br>
<br>

### 16. Autowired vs inject?
`@Autowired` is Spring's own (legacy) annotation. `@Inject` is part of a new Java technology called CDI that defines a standard for dependency injection similar to Spring. In a Spring application, the two annotations works the same way as Spring has decided to support some JSR-299 annotations in addition to their own.

`@Autowired` and `@Inject` annotation behave identically. Both of these annotations use the `AutowiredAnnotationBeanPostProcessor` to inject dependencies. `@Autowired` and `@Inject` can be used interchangeable to inject Spring beans. However the `@Resource` annotation uses the `CommonAnnotationBeanPostProcessor` to inject dependencies. Even though they use different post processor classes they all behave nearly identically. Below is a summary of their execution paths.

**@Autowired and @Inject**
* Matches by Type
* Restricts by Qualifiers
* Matches by Name

**@Resource**
* Matches by Name
* Matches by Type
* Restricts by Qualifiers (ignored if match is found by name)

[@Article](https://blogs.sourceallies.com/2011/08/spring-injection-with-resource-and-autowired/#more-2350)

17. Why do you override equals and hash code?
18. Set vs tree set?
19. Write a program that prints numbers 1 to 100. For every multiple of 3 print F, for every multiple of 5 print B for every multiple of 15 print FB.
20. Write a program to reverse a string using recursion
21. Write a program to create an immutable object, implement a builder, code and unit test to this
22. Implement a simple rules processor with flexibility to add/delete rules
 
23. What are synchronized methods and synchronized statements?

<br>
<br>

### 24.How do you manage concurrent access to a variable (int)?

If there is one and only one thread that writes to variable you can get away with making it `volatile`. Otherwise see the answer with [AtomicInteger](https://docs.oracle.com/javase/1.5.0/docs/api/java/util/concurrent/atomic/AtomicInteger.html).

AtomicInteger - An int value that may be updated atomically

Only `volatile` will work in case of only one writing thread because there is only one writing thread so it always has the right value of variable

```java
package com.journaldev.concurrency;

import java.util.concurrent.atomic.AtomicInteger;

public class JavaAtomic {

    public static void main(String[] args) throws InterruptedException {

        ProcessingThread pt = new ProcessingThread();
        Thread t1 = new Thread(pt, "t1");
        t1.start();
        Thread t2 = new Thread(pt, "t2");
        t2.start();
        t1.join();
        t2.join();
        System.out.println("Processing count=" + pt.getCount());
    }
}

class ProcessingThread implements Runnable {
    private AtomicInteger count = new AtomicInteger();

    @Override
    public void run() {
        for (int i = 1; i < 5; i++) {
            processSomething(i);
            count.incrementAndGet();
        }
    }

    public int getCount() {
        return this.count.get();
    }

    private void processSomething(int i) {
        // processing some job
        try {
            Thread.sleep(i * 1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

}
```

Benefits of using Concurrency classes for atomic operation is that we don't need to worry about synchronization. This improves code readability and chance of errors are reduced. Also atomic operation concurrency classes are assumed to be more efficient that synchronization which involves locking resources.

<br>
<br>

### 25. What are the states of a Thread?

26. How do you stop a Thread?
27. When a thread blocks on I/O, what state does it enter?

<br>
<br>

### 28. What is the difference between preemptive scheduling and time slicing?

* **Preemptive scheduling:** The highest priority task executes until it enters the waiting or dead states or a higher priority task comes into existence.

* **Time slicing:** A task executes for a predefined slice of time and then reenters the pool of ready tasks. The scheduler then determines which task should execute next, based on priority and other factors.

<br>
<br>

### 29.How do you stop a Java program?

`return` to come out of the method execution, `break` to come out of a loop execution and `continue` to skip the rest of the current loop. 

<br>
<br>

### 30. Difference b/w Collection and Map interfaces?

31. What are all the Collection implementation techniques?
32. What is the difference between set and list?
 
<br>
<br>

### 33. To implement TreeSet, what interface must implement?

```java
import java.util.TreeSet;
 
class Dog {
    int size;
    Dog(int s) {
        size = s;
    }
}
 
public class ImpComparableWrong {
 
    public static void main(String[] args) {
        TreeSet<Integer> i = new TreeSet<Integer>();
        TreeSet<Dog> d = new TreeSet<Dog>();
        d.add(new Dog(1));
        d.add(new Dog(2));
        d.add(new Dog(1));
 
        i.add(1);
        i.add(2);
        i.add(3);
 
        System.out.println(d.size() + &quot; &quot; + i.size());
    }
}
```
```java
// Output : 
Exception in thread "main" java.lang.ClassCastException: Dog cannot be cast to java.lang.Comparable
        at java.util.TreeMap.put(TreeMap.java:542)
        at java.util.TreeSet.add(TreeSet.java:238)
        at ImpComparableWrong.main(ImpComparableWrong.java:17)
Java Result: 1
BUILD SUCCESSFUL (total time: 2 seconds)
```
The reason is that Class Dog needs to implement Comparable in order for a TreeSet (which keeps its elements sorted) to be able to contain Dog objects. The added object cannot be compared with the elements currently in the set, the add(Object) call throws a ClassCastException. To make an object comparable, user-defined class must implement the Comparable interface.
```java
import java.util.TreeSet;
 
class Dog implements Comparable<Dog> {
 
    int size;
 
    Dog(int s) {
        size = s;
    }
 
    public int compareTo(Dog o) {
        return size - o.size;
    }
}
 
public class ImpComparable {
 
    public static void main(String[] args) {
 
        TreeSet<Dog> d = new TreeSet<Dog>();
        d.add(new Dog(1));
        d.add(new Dog(2));
        d.add(new Dog(1));
 
        TreeSet<Integer> i = new TreeSet<Integer>();
        i.add(1);
        i.add(2);
        i.add(3);
 
        System.out.println(d.size() + &quot; &quot; + i.size());
    }
}
```

34. Difference b/w Stack and Heap?
35. What is Marker Interface?
36. What are Transient and Volatile Modifiers?
37. Difference between String s = "java" and String s = new String ("java");
38. What is the difference between error and an exception?

<br>
<br>

### 39. What value does readLine () return when it has reached the end of a file?
With text files, maybe the EOF is -1 when using BufferReader.read(), char by char. I made a test with BufferReader.readLine()!=null and it worked properly.

40. Why to use EJB in the project?
41. Why to use springs in the application?

<br>
<br>

### 42. How to handle the transactions in the project?
#### Types of the transaction management Spring support
Spring supports two types of transaction management:

* **Programmatic transaction management:** This means that you have managed the transaction with the help of programming. That gives you extreme flexibility, but it is difficult to maintain.
* **Declarative transaction management:** This means you separate transaction management from the business code. You only use annotations or XML based configuration to manage the transactions.

[article](https://www.journaldev.com/2603/spring-transaction-management-jdbc-example#spring-declarative-transaction-management-8211-service)

#### Which Transaction management type is more preferable?
Most users of the Spring Framework choose declarative transaction management because it is the option with the least impact on application code, and hence is most consistent with the ideals of a non-invasive lightweight container. Declarative transaction management is preferable over programmatic transaction management though it is less flexible than programmatic transaction management, which allows you to control transactions through your code.

[article-youtube](https://www.youtube.com/watch?v=hBO44wKy2zQ)

<br>
<br>

### 43. How to find the duplicate element in the array with less complexity?
```java
/*
*
* Java Program to find duplicate elements in an array. There are two straight 
* forward solution of this problem first, brute force way and second by using 
* HashSet data structure. A third solution, similar to second one is by using 
* hash table data structure e.g. HashMap to store count of each element and 
* print element with count 1. 
*/
public class DuplicatesInArray {
	public static void main(String args[]) {
		String[] names = { "Java", "JavaScript", "Python", "C", "Ruby", "Java" };
		// First solution : finding duplicates using brute force method
		System.out.println("Finding duplicate elements in array using brute force method");
		for (int i = 0; i < names.length; i++) {
			for (int j = i + 1; j < names.length; j++) {
				if (names[i].equals(names[j])) {
					// got the duplicate element
				}
			}
		}

		// Second solution : use HashSet data structure to find duplicates
		System.out.println("Duplicate elements from array using HashSet data structure");
		Set<String> store = new HashSet<>();
		for (String name : names) {
			if (store.add(name) == false) {
				System.out.println("found a duplicate element in array : " + name);
			}
		}

		// Third solution : using Hash table data structure to find duplicates
		System.out.println("Duplicate elements from array using hash table");
		Map<String, Integer> nameAndCount = new HashMap<>();

		// build hash table with count
		for (String name : names) {
			Integer count = nameAndCount.get(name);
			if (count == null) {
				nameAndCount.put(name, 1);
			} else {
				nameAndCount.put(name, ++count);
			}
		}
		// Print duplicate elements from array in Java
		Set<Entry<String, Integer>> entrySet = nameAndCount.entrySet();
		for (Entry<String, Integer> entry : entrySet) {
			if (entry.getValue() > 1) {
				System.out.println("Duplicate element from array : " + entry.getKey());
			}
		}
	}
}

// Output : 
// Finding duplicate elements in array using brute force method 
// Duplicate elements from array using HashSet data structure found a duplicate element in array : Java 
// Duplicate elements from array using hash table 
// Duplicate element from array : Java
```
[article](http://javarevisited.blogspot.com/2015/06/3-ways-to-find-duplicate-elements-in-array-java.html)


44. Puzzle: if there are 8 balls in which 7 of them are of same weight one is different.?
45. How to find the odd one in 2 iteration?
46. Some questions on struts flow?
 
http://java.sun.com/j2se/1.5.0/docs/guide/lang/resources.html
http://www.javabeat.net/qna/junit/1/
http://sqa.fyicenter.com/FAQ/JUnit/
http://flapdoor.blogspot.com/2009/05/java-interview-questions-collections-ii.html
