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
<br>
<br>

### 11. How will you implement AbstractFactory Design Pattern?
<br>
<br>

### 12. Will a singleton pattern work in a multi clustered environment?
<br>
<br>

### 13. What are the concurrent in the collection classes?
<br>
<br>

### 14. How will you handle unchecked exception in multi-threaded environment?
 
<br>
<br>

### 15. If the DBA's goofed up and forgot to mark the PK field as Primary Key and duplicate data gets loaded. How will you manage it?
 
<br>
<br>

### 16. Difference between collection and collections?
<br>
<br>

### 17. Different classes in collection?
<br>
<br>

### 18. How to save a directory structure in java?
<br>
<br>

### 19. Spring different types of scope?
<br>
<br>

### 20. What is the lifecycle of a bean?
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

### 24. Spring bean scopes – repeated?
<br>
<br>

### 25. Explain about executor framework and future object?
<br>
<br>

### 26. Differences between Array List and Linked List –repeated?
<br>
<br>

### 27. Creating Immutable class?
<br>
<br>

### 28. Is it possible to add new member variables in immutable class once created?
<br>
<br>

### 29. What is singleton class?
<br>
<br>

### 30. Can you access static variable from non-static methods?
<br>
<br>

### 31. Static vs singleton?
<br>
<br>

### 32. When there are two elements having the same value 5 how will you remove from an ArrayList? Will it thrown an exception and what is it.?
<br>
<br>

### 33. Pseudocode to remove element in Linked List?
 
<br>
<br>

### 34. What is closure in JavaScript?
<br>
<br>

### 35. What is prototype in JavaScript?
<br>
<br>

### 36. What is the difference between == and === in JavaScript?
 
<br>
<br>

### 37. Thread?
<br>
<br>

### 38. Cyclicbarrier vs Countdown latch (some deep question on them)?
 
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
12. When dealing with sensitive data, is it good to use string or array of char's. Why?
13. Which is better String s ="hello" or String s= new String ("hello")
14. What are fast fail and fail safe iterators?
15. Explain spring bean lifecycle?
16. Autowired vs inject?
17. Why do you override equals and hash code?
18. Set vs tree set?
19. Write a program that prints numbers 1 to 100. For every multiple of 3 print F, for every multiple of 5 print B for every multiple of 15 print FB.
20. Write a program to reverse a string using recursion
21. Write a program to create an immutable object, implement a builder, code and unit test to this
22. Implement a simple rules processor with flexibility to add/delete rules
 
23. What are synchronized methods and synchronized statements?
24. How do you manage concurrent access to a variable (int)
25. What are the states of a Thread?
26. How do you stop a Thread?
27. When a thread blocks on I/O, what state does it enter?
28. What is the difference between preemptive scheduling and time slicing?
29. How do you stop a Java program?
30. Difference b/w Collection and Map interfaces?
31. What are all the Collection implementation techniques?
32. What is the difference between set and list?
 
33. To implement TreeSet, what interface must implement?
34. Difference b/w Stack and Heap?
35. What is Marker Interface?
36. What are Transient and Volatile Modifiers?
37. Difference between String s = "java" and String s = new String ("java");
38. What is the difference between error and an exception?
39. What value does readLine () return when it has reached the end of a file?
40. Why to use EJB in the project?
41. Why to use springs in the application?
42. How to handle the transactions in the project?
43. How to find the duplicate element in the array with less complexity?
44. Puzzle: if there are 8 balls in which 7 of them are of same weight one is different.?
45. How to find the odd one in 2 iteration?
46. Some questions on struts flow?
 
http://java.sun.com/j2se/1.5.0/docs/guide/lang/resources.html
http://www.javabeat.net/qna/junit/1/
http://sqa.fyicenter.com/FAQ/JUnit/
http://flapdoor.blogspot.com/2009/05/java-interview-questions-collections-ii.html
