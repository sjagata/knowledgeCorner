### 1. What are immutable objects? What are the advantages of these objects?
Immutability is often presented as a key concept of functional programming. Most functional programming languages like Haskell, OCaml and Scala follow a immutable-by-default approach for variables in their programs. In fact to write code which uses mutation programmers have to go out of the way and do something special - like using monads in Haskell and mutable references in OCaml and Scala. It is of course also possible to create and use immutable objects in other programming languages. In order to get the benefits of immutability in Java we can use the following guidelines while programming -

Mark the class final
Mark all the fields private and final
Force all the callers to construct an object of the class directly, i.e. do not use any setter methods
Do not change the state of the objects in any methods of the class


* Immutable objects are thread-safe so you will not have any synchronization issues.
* Immutable objects are good Map keys and Set elements, since these typically do not change once created.
* Immutability makes it easier to write, use and reason about the code (class invariant is established once and then unchanged)
* Immutability makes it easier to parallelize your program as there are no conflicts among objects.
* The internal state of your program will be consistent even if you have exceptions.
* References to immutable objects can be cached as they are not going to change.





2. How would you write a constructor for an immutable class person with fields name and DOB?
3. What are daemon threads?
4. Explain the use of executor framework in multithreading?
5. What is the difference between callable and runnable interface?
6. What are the major differences between ArrayList and LinkedList?
7. What is the difference between LinkedList and doublyLinkedList?
8. How do the keys operate in a HashMap?
 
9. How will you implement sorting logic in ArrayList? Array List contains custom type objects.
10. HashMap example, where he adds null key to the map. Question was if it will get compiled?
11. How will you implement AbstractFactory Design Pattern?
12. Will a singleton pattern work in a multi clustered environment?
13. What are the concurrent in the collection classes?
14. How will you handle unchecked exception in multi-threaded environment?
 
15. If the DBA's goofed up and forgot to mark the PK field as Primary Key and duplicate data gets loaded. How will you manage it?
 
16. Difference between collection and collections?
17. Different classes in collection?
18. How to save a directory structure in java?
19. Spring different types of scope?
20. What is the lifecycle of a bean?
21. How to count different salary in database?
 
22. Advantages and disadvantages of using SOAP WebServices?
23. About Restful WebServices?
24. Spring bean scopes – repeated?
25. Explain about executor framework and future object?
26. Differences between Array List and Linked List –repeated?
27. Creating Immutable class?
28. Is it possible to add new member variables in immutable class once created?
29. What is singleton class?
30. Can you access static variable from non-static methods?
31. Static vs singleton?
32. When there are two elements having the same value 5 how will you remove from an ArrayList? Will it thrown an exception and what is it.?
33. Pseudocode to remove element in Linked List?
 
34. What is closure in JavaScript?
35. What is prototype in JavaScript?
36. What is the difference between == and === in JavaScript?
 
37. Thread?
38. Cyclicbarrier vs Countdown latch (some deep question on them)?
 
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
