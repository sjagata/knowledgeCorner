# Spring framework  

#### [(reference)](http://tutorialspointexamples.com/spring-tutorial-beginners-eclipse/)

Spring Framework is one of the most popular Java EE frameworks. It is an open source and light weight framework created by Rod Johnson in June 2003.

### Core principles of Spring Framework:
1. Dependency Injection (DI).
2. Aspect Oriented Programming (AOP).

**Advantages of Spring Framework:**

1. **Light weight:**
Spring framework is light weight framework because of its POJO model implementation.
2. **Non-invasive approach:**
As we know that struts forces programmer to extend Action Class but spring framework doesn’t force a programmer to extend class or implement interface given by Spring API.
3. **Loose Coupling:**
Because of dependency injection concept, spring objects are loosely coupled.
4. **Modular fashion:**
Spring framework is designed in modular fashion. A programmer can use only needed modules and ignore the rest.
5. **Easy Testing:**
Dependency injection and POJO model makes easy to test an application.
6. **Transaction management interface:**
Spring framework provides transaction management interface for transaction management.
7. **No need of application server:**
Struts or EJB application require application server to run but spring application doesn’t need an application server.
8. **MVC framework:**
Spring framework is a great alternative to web MVC frameworks like Struts.

<br>
<br>

** **

## Spring framework architecture modules

Spring framework is designed in modular fashion from which a programmer can choose the applicable modules and ignore the rest. Spring framework modules are divided into categories given below.

**Spring framework architecture Diagram:**

![alt text][logo]

[logo]: http://tutorialspointexamples.com/wp-content/uploads/2015/09/spring-overview.png "Spring framework architecture"


### 1. Test:

Spring test module provides the supports for testing of spring components with JUnit or TestNG frameworks.

### 2. Core Container:

Spring core container contains the following:

* **Core:** Core module provides the fundamental features of spring framework like IoC and DI.
*	**Bean:** Bean module provides the BeanFactory.
* **Context:** Context module provides a way to access any object. ApplicationContext interface is the main part of Context module.
*	**Expression language:** Expression language module provides a way to manipulate objects at runtime.

### 3.	Data Access/Integration contains the following:

* **JDBC:** JDBC modules provides a JDBC-abstraction layer.
* **ORM:** ORM provides integration layers for object-relational mapping APIs like JPA, and Hibernate etc.
* **OXM:** OXM module provides an abstraction layer for Object/XML mapping APIs like JAXB, Castor and XMLBeans etc.
* **JMS:** JMS module provides feature of message processing.
* **Transaction:** Transaction module provides the facility of transaction management for classes like POJOs etc.

### 4.	Web:

Web module consist of Web, Web-Servlet, Web-Struts, Web-Socket and Web-Portlet which provides the facility of creating web applications.

### 5. AOP:

AOP module provides aspect-oriented programming implementation which provides the facility to define method-interceptors.

### 6.	Instrumentation:

Instrumentation module provides class instrumentation support and class loader implementations

<br>
<br>

** **

## spring IoC container types

Spring IoC container is responsible for create, wire, configure and manage objects during their complete life cycle. It uses configuration metadata for create, configure and manage objects. Configuration metadata can be represented by spring configuration xml file or annotations.

#### Types of Spring IoC container:

1.	BeanFactory
2.	ApplicationContext

#### BeanFactory:

BeanFactory **_org.springframework.beans.factory.BeanFactory_** is the interface and **_XmlBeanFactory_** is an implementation class of it. It is a simple container which provides the basic support for dependency injection.

```java
Resource resource = new ClassPathResource(“spring configuration file”);
BeanFactory beanFactory = new XmlBeanFactory(resource);
```

#### ApplicationContext:

ApplicationContext **_org.springframework.context.ApplicationContext_** is the interface and **_ClassPathXmlApplicationContext_** is an implementation class of it. ApplicationContext container includes all functionality of the BeanFactory container with some extra functionality like internationalization, event listeners etc.

```java
ApplicationContext applicationContext = new ClassPathXmlApplicationContext("spring configuration file");
```

_Note: As ApplicationContext provides extra functionality including all given by BeanFactory it is better to use ApplicationContext container._

<br>
<br>

** **

## spring bean

A spring bean represents an object that is created, configured and managed by spring container. A spring bean is created by configuration metadata passed to the spring container which tells the container about bean creation, bean lifecycle and bean dependencies.

**Spring bean properties:**

<table class="table">
    <thead>
      <tr>
        <th>Bean Properties</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>1. class</td>
        <td>It is mandatory and specify the bean class which is used to create the bean.</td>
      </tr>
      <tr>
        <td>2. name</td>
        <td>It specifies the bean unique identifier.</td>
      </tr>
      <tr>
        <td>3. scope</td>
        <td>It specifies the scope of the objects created from a particular bean definition.</td>
      </tr>
      <tr>
        <td>4. constructor-arg</td>
        <td>It is used to inject the dependencies.</td>
      </tr>
      <tr>
        <td>5. properties</td>
        <td>It is used to inject the dependencies.</td>
      </tr>
      <tr>
        <td>6. autowiring mode</td>
        <td>It is used to inject the dependencies.</td>
      </tr>
      <tr>
        <td>7. lazy-initialization mode</td>
        <td>It tells the IoC container to create a bean instance when it is first requested, rather than at startup.</td>
      </tr>
      <tr>
        <td>8. initialization method</td>
        <td>It is a callback method to be called just after all necessary properties on the bean have been set by the container.</td>
      </tr>
      <tr>
        <td>9. destruction method</td>
        <td>It is a callback to be called when the container containing the bean is destroyed.
 </td>
      </tr>
    </tbody>
  </table>


```java
<bean id="..." class="..." lazy-init="true">
       //bean configuration
</bean>
```

<br>
<br>

** **

## Spring bean scopes:

As we discussed that spring container is responsible for creating and managing bean object. Spring provides the facility to return the same instance or a new instance each time when one is needed. It depends upon the bean scope.

### Spring framework bean scopes:

<table class="table">
    <thead>
      <tr>
        <th>Bean Scope</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>1. singleton</td>
        <td>It scopes the bean definition to a single instance per spring container. It is the default scope. Spring container keeps it into cache and returns the same instance each time a request for that particular bean is made.</td>
      </tr>
     <tr>
          <td>2. prototype	</td>
          <td>It scopes a single bean definition to have new bean instance each time a request for that particular bean is made.</td>
      </tr>
      <tr>
          <td>3. request</td>
          <td>It scopes a bean definition to an HTTP request.</td>
      </tr>
      <tr>
          <td>4. session</td>
          <td>It scopes a bean definition to an HTTP session.</td>
      </tr>
        <tr>
          <td>5. global-session</td>
          <td>It scopes a bean definition to a global HTTP session./td>
      </tr>
    </tbody>
</table>

_Note: The request, session and global-session are only available in the context of a web-aware ApplicationContext._

<br>
<br>

** **

## Spring bean life cycle:

As we discussed earlier spring IoC container is responsible to create, configure and manage objects during their complete life cycle using configuration metadata. See the below points to understand the spring bean life cycle.

**Bean lifecycle in spring framework:**

1.	Spring container finds the bean definition from configuration file.
2.	Spring container instantiates the bean using Java Reflection API.
3.	Spring container applies the all specified properties using DI.
4.	If the bean class implements the BeanNameAware interface, then spring container calls the setBeanName() method by passing bean’s id.
5.	If the bean class implements the BeanClassLoaderAware interface, then spring container calls the setBeanClassLoader() method by passing an instance of the ClassLoader object that loaded this bean.
6.	If the bean class implements the BeanFactoryAware interface, then spring container calls setBeanFactory() method by passing an instance of BeanFactory object.
7.	If there are any BeanPostProcessors object associated with the BeanFactory than spring container calls their postProcessBeforeInitialization() method even before setting the properties for the bean.
8.	If the bean class implements the InitializingBean interface, then spring container calls the afterPropertiesSet() method after setting bean properties.
9.	If init-method is specified in configuration file for the bean then spring container calls the corresponding method in the bean class.
10.	If there are any BeanPostProcessors associated with the bean then spring container calls the postProcessAfterInitialization() method.
11.	If the bean class implements the DisposableBean interface, then spring container calls the destroy() method when the application no longer needs the bean reference.
12.	If destroy-method is specified in the Configuration file for the bean, then spring container calls the corresponding method in the bean class.
 
<br>
<br>

** **

## Callback method:

A callback method in java is a method which is called when an event occurs. Normally we can implement that by passing an implementation of a certain interface to the system which is responsible for triggering the event.

### Post-initialization callback methods:

#### Using InitializingBean interface:

The InitializingBean interface provides afterPropertiesSet() method which can be used for any post-initialization task.

```java
public class TestBean implements InitializingBean {
   public void afterPropertiesSet() {
      // post-initialization task.
   }
}
```

#### Using init-method attribute:

In XML configuration metadata we can specify the name of the method which has a void no-argument signature in init-method attribute for any post-initialization task.

```java
<bean id="testBean" class="Test" init-method="init"/>
In class definition:
public class Test {
   public void init() {
      // post-initialization task.
   }
}
```

### Pre-destroy callback methods:

#### Using DisposableBean interface:

The DisposableBean interface provides destroy() method which can be used for any pre-destroy task.

```java
public class TestBean implements DisposableBean {
   public void destroy() {
      // pre-destroy task.
   }
}
```

#### Using destroy-method attribute:

In XML configuration metadata we can specify the name of the method which has a void no-argument signature in destroy-method attribute for any pre-destroy task.

```java
<bean id="testBean" class="Test" destroy-method=" destroy"/>
In class definition:
public class Test {
   public void destroy() {
      // pre-destroy task.
   }
}
```

#### Example :

```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import springframework.HelloWorld;

@SpringBootApplication
public class SpringFrameworkApplication {

	private static ApplicationContext context;

	public static void main(String[] args) {
		SpringApplication.run(SpringFrameworkApplication.class, args);

		context = new ClassPathXmlApplicationContext("applicationContext.xml");

		// Get HelloWorld bean object from ApplicationContext instance.
		HelloWorld helloWorld = (HelloWorld) context.getBean("helloWorld");

		// Call sayHello method of HelloWorld bean.
		helloWorld.sayHello();
	}
}
```


```java

// applicationContext.xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="helloWorld" class="springframework.HelloWorld">
		<property name="userName" value="John Doe" />
	</bean>

</beans>

```

<br>
<br>

** **

## Spring bean definition inheritance

As we discussed earlier a bean definition in configuration metadata can contain constructor arguments, property values etc. Spring framework provides the facility that a child bean definition can inherits configuration data from a parent definition. A child definition can override some values of parent definition or add some others, as required.

**_Use parent attribute in child definition and pass parent bean into it._**

Syntax:

```java
<bean id="parentBeanId" class="TestParentBean">
      <property name="name1" value="value1"/>
      <property name="name2" value="value2"/>
</bean>
 
<bean id="childBeanId" class="ChildBeanId" parent="parentBeanId">
      <property name="name1" value="value"/>
      <property name="name3" value="value3"/>
</bean>
```

#### Example:

```java
// Get BeanInheritance bean object from ApplicationContext instance.
BeanInheritance beanInheritance = (BeanInheritance) context.getBean("beanInheritance");

// Process HelloWorld Object.
System.out.println("BeanInheritance bean properties: ");
System.out.println(beanInheritance.getMsg1());
System.out.println(beanInheritance.getMsg2());

// Get BeanInheritance2 bean object from ApplicationContext instance.
BeanInheritance2 beanInheritance2 = (BeanInheritance2) context.getBean("beanInheritance2");

// Process HelloJava Object.
System.out.println("BeanInheritance2 bean properties: ");
System.out.println(beanInheritance2.getMsg1());
System.out.println(beanInheritance2.getMsg2());
System.out.println(beanInheritance2.getMsg3());
```

```java
// applicationContext.xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="helloWorld" class="springframework.HelloWorld">
		<property name="userName" value="John Doe" />
	</bean>

	<bean id="beanInheritance" class="springframework.BeanInheritance">
		<property name="msg1" value="beanInheritance - Msg1" />
		<property name="msg2" value="beanInheritance - Msg2" />
	</bean>

	<bean id="beanInheritance2" class="springframework.BeanInheritance2" parent="beanInheritance">
		<property name="msg2" value="beanInheritance2 - Msg2" />
		<property name="msg3" value="beanInheritance2 - Med3" />
	</bean>

</beans>

```

<br>
<br>

** **

## Spring bean definition template

As we discussed earlier a bean definition in configuration metadata can contain constructor arguments, property values etc. Spring framework provides the facility to define a bean definition template which can be used by child bean definitions. To define a template remove class attribute and use abstract attribute to true in bean definition.

**_Use parent attribute in child definition and pass template bean into it._**

Syntax:

```java
<bean id="templateId" abstract=”true”>
      <property name="name1" value="value1"/>
      <property name="name2" value="value2"/>
</bean>
 
<bean id="childBeanId" class="ChildBeanId" parent="templateId">
      <property name="name1" value="value"/>
      <property name="name3" value="value3"/>
</bean>
```

**_Note: We can create template with or without using the class attribute. If we create template using class attribute then corresponding class can’t be instantiated._**

```java
//applicationContext.xml
 <bean id="abstractTemplate" abstract="true">
       <property name="msg1" value="Common World."/>
   </bean>
 
   <bean id="helloWorld" 
       class="springframework.HelloWorld" parent="abstractTemplate">
     <property name="msg2" value="World."/>
   </bean>
 
    <bean id="helloJava" 
        class="springframework.HelloJava" parent="abstractTemplate">
     <property name="msg2" value="Java"/>
    </bean>
```

<br>
<br>

** **

## Spring dependency injection

Injection is a process of passing the dependency to a dependent object.

### Dependency Injection (DI):

Dependency Injection (DI) is a design pattern that implements inversion of control principle for resolving dependencies. It allows a programmer to remove hard coded dependencies so that the application becomes loosely coupled and extendable.

### Let us discuss object dependency with below example:

```java
public class Student {
   private Address address;
 
   public Student() {
      address = new Address();
   }
}
```

In above example Student class requires an Address object and it is responsible for initializing and using the Address object. If Address class is changed in future then we have to make changes in Student class also. This approach makes tight coupling between Student and Address objects. We can resolve this problem using dependency injection design pattern. i.e. Address object will be implemented independently and will be provided to Student when Student is instantiated by using constructor-based or setter-based dependency injection.

### Types of dependency Injection:

1. Constructor-based Dependency Injection.
2. Setter-based Dependency Injection.

<br>

## Spring constructor based injection

Constructor based dependency injection is a process of passing the dependency to a dependent object via a constructor.

**_Note:_**

1. For primitive data types use element and for dependent objects use

```java
<ref bean="beanId"/>
```

2. Index attribute is used to specify the index of constructor arguments.

#### Example :

We have created two beans “Student” and “Address”. Student class requires an Address class object. In struts configuration file we define Address bean and pass this as an argument in Student class using constructor-arg element.

```java
//applicationContext.xml

<bean id="student" class="springframework.Student">
	<property name="name" value="John Doe"/>
	<property name="id" value="java"/>
	<property name="role" value="Developer"/>
	<constructor-arg ref="address"/>
</bean>

<bean id="address" class="springframework.Address">
	<property name="addLine" value="Test address"/>
	<property name="city" value="charlotte"/>
	<property name="state" value="NC"/>
	<property name="country" value="USA"/>
</bean>
```
    
```java
// java code

//Get ApplicationContext using spring configuration file.
  ApplicationContext context =  new ClassPathXmlApplicationContext("applicationContext.xml");
 
  //Get Student bean object from ApplicationContext instance. 
  Student student = (Student) context.getBean("student");
 
  //Process Student Object.
  System.out.println("Student info: "); 
  System.out.println("Name: " + student.getName());
  System.out.println("RollNo: " + student.getId());
  System.out.println("Class: " + student.getRole());
 
  //Get Address from Student Object.
  Address studentAddress = student.getAddress();
 
  //Process Address Object.
  System.out.println("Student Address: ");
  System.out.println("Address Line: " + studentAddress.getAddLine());
  System.out.println("City: " + studentAddress.getCity());
  System.out.println("State: " + studentAddress.getState());
  System.out.println("Country: " + studentAddress.getCountry());
```
<br>

### Constructor injection type ambiguities in spring tutorial

In constructor based dependency injection if our class contains multiple constructors with different types and same number of arguments then spring framework cause the constructor injection argument type ambiguities issue. Let us discuss it with below example.

#### Problem1 :

We have created one bean class “Student” which have two constructors with same number of arguments but with different data types. 
First constructor have String name, int id and second constructor have String name, String role arguments. In spring configuration file we pass arguments ‘John Doe’ and 27. 
It should call first constructor but if it calls the second constructor and the result is not as expected.

```java
 <bean id="student" class="springFramework.Student">
	<constructor-arg  value="John Doe"/>
	<constructor-arg value="27"/>
</bean>
```

#### Solution:

We have to specify the constructor argument’s data types using type attribute. Now it will call the first constructor and the result is as expected.

```java
 <bean id="student" class="springFramework.Student">
	<constructor-arg  value="John Doe"/>
	<constructor-arg value="27" type="int"/>
</bean>
```

#### Problem2 :

In case when we have one constructor with more than one parameter and do not defined the argument type then the spring framework may through org.springframework.beans.factory.UnsatisfiedDependencyException exception.

```java
   <bean id="student" class="springFramework.Student">
       <constructor-arg value="27"/> // no constructor with index 1 of type int 
       <constructor-arg value="John Doe"/>
   </bean>
   
   //output
   Exception in thread "main" 
org.springframework.beans.factory.UnsatisfiedDependencyException: 
Error creating bean with name 'student' defined in class path resource 
[applicationContext.xml]: Unsatisfied dependency expressed through 
constructor argument with index 1 of type [int]: Could not convert 
constructor argument value of type [java.lang.String] to required 
type [int]: Failed to convert value of type 'java.lang.String' to 
required type 'int'; nested exception is java.lang.NumberFormatException:
For input string: "John Doe"
```

#### Solution:

We have to use index attribute to specify the index of constructor arguments.

```java
   <bean id="student" class="springFramework.Student">
       <constructor-arg index="1" value="27"/>
       <constructor-arg index="0" value="John Doe"/>
   </bean>
```
<br>

## Spring Setter based injection

Setter based dependency injection is a process of passing the dependency to a dependent object via a setter method.

**_Note:_**

1. For primitive data types use element and for dependent objects use

```java
<ref bean="beanId"/>
```

2. Index attribute is used to specify the index of constructor arguments.

### Example :

We have created two beans “Student” and “Address”. Student class requires an Address class object. In spring configuration file we define Address bean and pass this as an argument in Student class using parameter element.

```java
   <bean id="student" class="springFramework.Student">
       <property name="name" value="John Doe"/>
       <property name="id" value="06"/>
       <property name="role" value="developer"/>
       <property name="address" ref="address"/>
   </bean>
 
    <bean id="address" class="springFramework.Address">
       <property name="addLine" value="Test address"/>
       <property name="city" value="Charlotte"/>
       <property name="state" value="NC"/>
       <property name="country" value="USA"/>
    </bean>
 ```

<br>
<br>

** **

## Spring dependency injection collections

Spring framework provides the facility to inject collection values via constructor or setter method. We can use the following inside the constructor or property element.

1. List.
2. Set.
3. Map.

Syntax (constructor based dependency injection):

```java
<bean id="testBeanId" class="Test">  
   <constructor-arg>  
    <list>  
     <value>value1</value>  
     <value>value2</value>  
     <value>value3</value>  
   </list>  
  </constructor-arg>  
</bean>
```

Syntax (setter based dependency injection):

```java
<bean id="testBeanId" class="Test">  
   <property name="testProperty">  
    <list>  
     <value>value1</value>  
     <value>value2</value>  
     <value>value3</value>  
   </list>  
  </property>  
</bean>
```

#### Example :

```java
// applicationContext.xml 

   <bean id="student" class="springFramework.Student">
       <property name="name" value="Jai"/>
       <property name="rollNo" value="MCA/07/06"/>
       <property name="className" value="MCA"/>
       <constructor-arg>
        <list>
      	 <ref bean="address1"/>
         <ref bean="address2"/>
        </list>
       </constructor-arg>
   </bean>
 
    <bean id="address1" class="springFramework.Address">
       <property name="addLine" value="Test address1"/>
       <property name="city" value="Matthews"/>
       <property name="state" value="SC"/>
       <property name="country" value="USA"/>
    </bean>
 
    <bean id="address2" class="springFramework.Address">
       <property name="addLine" value="Test address2"/>
       <property name="city" value="Charlotte"/>
       <property name="state" value="NC"/>
       <property name="country" value="USA"/>
    </bean>
    
    
 // java code
 
 //Get Address from Student Object.
List<Address> studentAddressList = student.getAddress()
 ```
<br>
<br>

** **

## Spring AOP tutorial

AOP refers to Aspect Oriented Programming which behaves like OOPs as both provides the concept of modularity. But the difference is it uses aspect rather than class for the unit of modularity.
Aspect Oriented Programming breaks down program logic into distinct parts called concerns. A cross-cutting concerns are aspects of a program that affect other concerns like transaction management, authentication, logging etc.

Spring AOP module provides the facility to add extra functionality before or after the method execution.
Note: Aspect Oriented Programming AOP is like triggers in programming languages like java, Perl, .NET etc.

**AOP Terminologies:**

### Aspect:
An aspect represents a class that contains advices, join points etc like transaction management. An aspect can be configured through Spring XML configuration or spring AspectJ integration.
 
### Join point:
Joint point represents a point in our application where we can plug-in AOP aspect. It can be method execution, exception handling, field access etc. Spring AOP only supports method execution joint type.
 
### Advice:
It represents the actual action to be taken by an aspect at a particular join point. In programming point view it represents the methods to be executed at a particular join point.
 
### Pointcut:
It represents the expression which is matched with join points to determine whether advice to be executed or not.
 
### Introduction:
It provides the facility to add new methods or attributes to existing classes.
 
### Target object:
It is an object on which advices are applied. It always be proxied object in spring because Spring AOP is implemented using runtime proxies.
 
### Weaving:
Weaving is the process of linking aspects with other application types or objects to create the advised proxy objects. This can be done at compile time, load time or at runtime. Spring AOP performs weaving at the runtime.

**AOP Advice Types:**

### Before:
It executes before the method execution.
 
### After:
It executes after the method execution. It not depends upon the method outcome.
 
### after-returning:
It executes after the method execution when method completes successfully.
 
### after-throwing:
It executes after the method execution when method exits by throwing an exception.
 
### Around:
It executes before and after the advised method is called.

<br>

## Spring AOP AspectJ Xml Configuration Example
AspectJ libraries provides the facility to declare aspect, pointcut etc using xml file. Let us discuss the syntax first.

### Declaring an aspect:

The element is used to declare an aspect. The ref attribute is used for bean reference.

### Declaring a pointcut:

The element is used to declare an pointcut. The expression element represents the expression used for matching the join point.

### Declaring advices:

The element is used to declare an advice.

**Advice types:**

#### Before:
It executes before the method execution.

#### After:
It executes after the method execution. It not depends upon the method outcome.

#### after-returning:
It executes after the method execution when method completes successfully.

#### after-throwing:
It executes after the method execution when method exits by throwing an exception.

#### Around:
It executes before and after the advised method is called.


### Spring AOP AspectJ Xml Configuration Before Advice Example:

BusinessLogic.java

```java
package springframework.aop;

public class BusinessLogic {
	public void implementBusinessLogic() {
		System.out.println("Business logic executed.");
	}
}
```

BeforeAdviceTest.java

```java
package springframework.aop;

import java.lang.reflect.Method;

import org.springframework.aop.MethodBeforeAdvice;

public class BeforeAdviceTest implements MethodBeforeAdvice {

	@Override
	public void before(Method method, Object[] args, Object target) throws Throwable {
		System.out.println("Additional concern " + "before business logic.");
	}

}
```

applicationContext.xml

```java
	<bean id="businessLogic" class="springframework.aop.BusinessLogic" />
	<bean id="beforeAdviceTest" class="springframework.aop.BeforeAdviceTest" />
	<bean id="proxy" class="org.springframework.aop.framework.ProxyFactoryBean">
		<property name="target" ref="businessLogic"></property>
		<property name="interceptorNames">
			<list>
				<value>beforeAdviceTest</value>
			</list>
		</property>
	</bean>
```

Java code 

```java
// Get BusinessLogic bean object from ApplicationContext instance.
BusinessLogic businessLogic = (BusinessLogic) context.getBean("proxy", BusinessLogic.class);

// Call implementBusinessLogic method of BusinessLogic bean.
businessLogic.implementBusinessLogic();
```

### Spring AOP AspectJ Xml Configuration after-returning Advice Example:

AfterReturningAdviceTest.java

```java
package springframework.aop;

import java.lang.reflect.Method;

import org.springframework.aop.AfterReturningAdvice;

public class AfterReturningAdviceTest implements AfterReturningAdvice {

	@Override
	public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
		System.out.println("Additional concern " + "after returning business logic.");
	}

}

```

applicationContext.xml

```java
	<bean id="businessLogic" class="springframework.aop.BusinessLogic" />
	<bean id="beforeAdviceTest" class="springframework.aop.BeforeAdviceTest" />
	<bean id="afterReturningAdviceTest" class="springframework.aop.AfterReturningAdviceTest" />
	<bean id="proxy" class="org.springframework.aop.framework.ProxyFactoryBean">
		<property name="target" ref="businessLogic"></property>
		<property name="interceptorNames">
			<list>
				<value>beforeAdviceTest</value>
				<value>afterReturningAdviceTest</value>
			</list>
		</property>
	</bean>
```

### Spring AOP AspectJ Xml Configuration after-throwing Advice Example:

AfterThrowingAdviceTest.java

```java
package springframework.aop;

import java.lang.reflect.Method;

import org.springframework.aop.ThrowsAdvice;

public class AfterThrowingAdviceTest implements ThrowsAdvice {
	public void afterThrowing(Method m, Object args[], Object target, Exception e) {
		System.out.println("Additional concern after" + " throwing exception in business logic.");
	}
}

```

applicationContext.xml

```java
	<bean id="businessLogic" class="springframework.aop.BusinessLogic" />
	<bean id="beforeAdviceTest" class="springframework.aop.BeforeAdviceTest" />
	<bean id="afterReturningAdviceTest" class="springframework.aop.AfterReturningAdviceTest" />
	<bean id="afterThrowingAdviceTest" class="springframework.aop.AfterThrowingAdviceTest" />
	
	<bean id="proxy" class="org.springframework.aop.framework.ProxyFactoryBean">
		<property name="target" ref="businessLogic"></property>
		<property name="interceptorNames">
			<list>
				<value>beforeAdviceTest</value>
				<value>afterReturningAdviceTest</value>
				<value>afterThrowingAdviceTest</value>
			</list>
		</property>
	</bean>
```

### Spring AOP AspectJ Xml Configuration Around Advice Example:

AroundAdviceTest.java

```java
package springframework.aop;

import org.aopalliance.intercept.MethodInterceptor;
import org.aopalliance.intercept.MethodInvocation;

public class AroundAdviceTest implements MethodInterceptor {

	@Override
	public Object invoke(MethodInvocation invocation) throws Throwable {
		Object obj;
		System.out.println("Additional concern before business logic.");
		obj = invocation.proceed();
		System.out.println("Additional concern after business logic.");
		return obj;
	}

}

```

applicationContext.xml

```java
	<bean id="businessLogic" class="springframework.aop.BusinessLogic" />
	<bean id="beforeAdviceTest" class="springframework.aop.BeforeAdviceTest" />
	<bean id="afterReturningAdviceTest" class="springframework.aop.AfterReturningAdviceTest" />
	<bean id="afterThrowingAdviceTest" class="springframework.aop.AfterThrowingAdviceTest" />
	<bean id="aroundAdviceTest" class="springframework.aop.AroundAdviceTest" />
	
	<bean id="proxy" class="org.springframework.aop.framework.ProxyFactoryBean">
		<property name="target" ref="businessLogic"></property>
		<property name="interceptorNames">
			<list>
				<value>beforeAdviceTest</value>
				<value>afterReturningAdviceTest</value>
				<value>afterThrowingAdviceTest</value>
				<value>aroundAdviceTest</value>
			</list>
		</property>
	</bean>
```

<br>

## Spring AOP AspectJ Annotation Configuration Example

AspectJ libraries provides the facility to declare aspect, pointcut etc with the help of annotations. Let us discuss the commonly used AspectJ annotations first.

### Declaring an aspect:

The **@Aspect** annotation is used to declare a class as an aspect.

```java
@Aspect
public class AspectModule {
 
}
```

### Declaring a pointcut:

The **@Pointcut** annotation is used to declare a pointcut. The expression parameter represents the expression used for matching the join point.

```java
@Pointcut("execution(expression)")
private void businessService() {
	//Block of code.
}
```

### Declaring advices:

The **@{ADVICE-NAME}** annotations is used to declare an advice.

### Spring AOP AspectJ Annotation Configuration Advice Example:

AdviceAnnotationTest.java

```java
package springframework.aop;

import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.AfterReturning;
import org.aspectj.lang.annotation.AfterThrowing;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.annotation.Pointcut;

@Aspect
public class AdviceAnnotationTest {

	@Pointcut("execution(* springframework.aop.*.*(..))")
	private void selectAll() {

	}

	@Before("selectAll()")
	public void beforeAdvice() {
		System.out.println("Before advice executed.");
	}

	@After("selectAll()")
	public void afterAdvice() {
		System.out.println("After advice executed.");
	}

	@AfterReturning(pointcut = "selectAll()", returning = "retVal")
	public void afterReturningAdvice(Object retVal) {
		System.out.println("After returning advice executed.");
		System.out.println("Returning value: " + retVal);
	}

	@AfterThrowing(pointcut = "selectAll()", throwing = "ex")
	public void afterThrowingAdvice(ArithmeticException ex) {
		System.out.println("Throwing advice executed.");
		System.out.println("Exception: " + ex.getMessage());
	}
}
```

applicationContext.xml

```java
<aop:config>
		<aop:aspect id="log" ref="adviceTest">
			<aop:pointcut id="selectAll" expression="execution(* springframework.aop.*.*(..))" />
			<aop:before pointcut-ref="selectAll" method="beforeAdvice" />
			<aop:after pointcut-ref="selectAll" method="afterAdvice" />
			<aop:after-returning pointcut-ref="selectAll" returning="retVal" method="afterReturningAdvice" />
			<aop:after-throwing pointcut-ref="selectAll" throwing="ex" method="afterThrowingAdvice" />
		</aop:aspect>
	</aop:config>

	<bean id="adviceTest" class="springframework.aop.AdviceAnnotationTest" />
```




































