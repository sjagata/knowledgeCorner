### 1. What is Inversion of Control (IoC) and Dependency Injection?
In software engineering, **inversion of control (IoC)** is a programming technique in which object coupling is bound at run time by an assembler object and is typically not known at compile time using static analysis. In traditional programming, the flow of the business logic is determined by objects that are statically assigned to one another. With inversion of control, the flow depends on the object graph that is instantiated by the assembler and is made possible by object interactions being defined through abstractions. The binding process is achieved through “dependency injection”.

Inversion of control is a **design paradigm with the goal of giving more control to the targeted components of your application, the ones that are actually doing the work.**

**Dependency injection** is a pattern used to create instances of objects that other objects rely on without knowing at compile time which class will be used to provide that functionality. **Inversion of control** relies on dependency injection because a mechanism is needed in order to activate the components providing the specific functionality. Otherwise how will the framework know which components to create if it is no longer in control?

In Java, dependency injection may happen through 3 ways:

1. A constructor injection
2. A setter injection
3. An interface injection

### 2. Explain IoC in Spring Framework?
The `org.springframework.beans` and `org.springframework.context` packages provide the basis for the Spring Framework’s IoC container. The `BeanFactory` interface provides an advanced configuration mechanism capable of managing objects of any nature. The `ApplicationContext` interface builds on top of the BeanFactory (it is a sub-interface) and adds other functionality such as easier integration with Spring’s AOP features, message resource handling (for use in internationalization), event propagation, and application-layer specific contexts such as the WebApplicationContext for use in web applications.

**The `org.springframework.beans.factory.BeanFactory` is the actual representation of the Spring IoC container that is responsible for containing and otherwise managing the aforementioned beans. The BeanFactory interface is the central IoC container interface in Spring.**

### 3. Difference between BeanFactory and ApplicationContext?
A `BeanFactory` is like a factory class that contains a collection of beans. The `BeanFactory` holds Bean Definitions of multiple beans within itself and then instantiates the bean whenever asked for by clients. `BeanFactory` is able to create associations between collaborating objects as they are instantiated. This removes the burden of configuration from bean itself and the beans client. `BeanFactory` also takes part in the life cycle of a bean, making calls to custom initialization and destruction methods.

On the surface, an `application context` is same as a bean factory.Both load bean definitions, wire beans together, and dispense beans upon request. But it also provides:

1. A means for resolving text messages, including support for internationalization.
2. A generic way to load file resources.
3. Events to beans that are registered as listeners.

The three commonly used implementations of `ApplicationContext` are:

1. **ClassPathXmlApplicationContext :** It Loads context definition from an XML file located in the classpath, treating context definitions as classpath resources. The application context is loaded from the application’s classpath by using the code.

```java
ApplicationContext context = new ClassPathXmlApplicationContext(“bean.xml”);
```

2. **FileSystemXmlApplicationContext :** It loads context definition from an XML file in the filesystem. The application context is loaded from the file system by using the code.

```java
ApplicationContext context = new FileSystemXmlApplicationContext(“bean.xml”);
```

3. **XmlWebApplicationContext :** It loads context definition from an XML file contained within a web application.

### 4. Explain Spring Bean Autowiring?
In spring framework, setting bean dependencies in configuration files is a good practice to follow, but the spring container is also able to autowire relationships between collaborating beans. This means that it is possible to automatically let Spring resolve collaborators (other beans) for your bean by inspecting the contents of the BeanFactory. **Autowiring** is specified per bean and can thus be enabled for some beans, while other beans will not be autowired.

The following excerpt from the XML configuration file shows a bean being autowired by name.

```java
<bean id="employeeDAO" class="com.howtodoinjava.EmployeeDAOImpl" autowire="byName" />
```

Apart from the autowiring modes provided in bean configuration file, autowiring can be specified in bean classes also using `@Autowired` annotation. To use `@Autowired` annotation in bean classes, you must first enable the annotation in spring application using below configuration.

```java
<context:annotation-config />
```

Same can be achieved using `AutowiredAnnotationBeanPostProcessor` bean definition in configuration file.

```java
<bean class ="org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor"/>
```

Now, when annotation configuration has been enables, you are free to autowire bean dependencies using @Autowired, the way you like.

```java
@Autowired
public EmployeeDAOImpl ( EmployeeManager manager ) {
    this.manager = manager;
}
```

### 5. Explain different modes of bean autowiring?
There are five auto wiring modes in spring framework. Lets discuss them one by one.

* **no:** This option is default for spring framework and it means that autowiring is OFF. You have to explicitly set the dependencies using tags in bean definitions.
* **byName:** This option enables the dependency injection based on bean names. When autowiring a property in bean, property name is used for searching a matching bean definition in configuration file. If such bean is found, it is injected in property. If no such bean is found, a error is raised.
* **byType:** This option enables the dependency injection based on bean types. When autowiring a property in bean, property’s class type is used for searching a matching bean definition in configuration file. If such bean is found, it is injected in property. If no such bean is found, a error is raised.
* **constructor:** Autowiring by constructor is similar to byType, but applies to constructor arguments. In autowire enabled bean, it will look for class type of constructor arguments, and then do a autowire by type on all constructor arguments. Please note that if there isn’t exactly one bean of the constructor argument type in the container, a fatal error is raised.
* **autodetect:** Autowiring by autodetect uses either of two modes i.e. constructor or byType modes. First it will try to look for valid constructor with arguments, If found the constructor mode is chosen. If there is no constructor defined in bean, or explicit default no-args constructor is present, the autowire byType mode is chosen.

### 6. Explain @Required annotation with example?
In a production-scale application, there may be hundreds or thousands of beans declared in the IoC container, and the dependencies between them are often very complicated. One of the shortcomings of setter injection is that it’s very hard for you to check if all required properties have been set or not. To overcome this problem, you can set **“dependency-check”** attribute of <bean> and set one of four attributes i.e. none, simple, objects or all (none is default option).

In real life application, you will not be interested in checking all the bean properties configured in your context files. Rather you would like to check if particular set of properties have been set or not in some specific beans only. Spring’s dependency checking feature using “dependency-check” attribute, will not able to help you in this case. So solve this problem, you can use `@Required` annotation.

To Use the `@Required` annotation over setter method of bean property in class file as below:

```java
public class EmployeeFactoryBean extends AbstractFactoryBean<Object>
{
    private String designation;
      
    public String getDesignation() {
        return designation;
    }
  
    @Required
    public void setDesignation(String designation) {
        this.designation = designation;
    }
      
    //more code here
}
```

`RequiredAnnotationBeanPostProcessor` is a spring bean post processor that checks if all the bean properties with the `@Required` annotation have been set. To enable this bean post processor for property checking, you must register it in the Spring IoC container.

```java
<bean class="org.springframework.beans.factory.annotation.RequiredAnnotationBeanPostProcessor" />
```

If any properties with `@Required` have not been set, a `BeanInitializationException` will be thrown by this bean post processor.

### 7. Explain @Autowired annotation with example?
The `@Autowired` annotation provides more fine-grained control over where and how autowiring should be accomplished. The `@Autowired` annotation can be used to autowire bean on the setter method just like @Required annotation, constructor, a property or methods with arbitrary names and/or multiple arguments.

E.g. You can use `@Autowired` annotation on setter methods to get rid of the `<property>` element in XML configuration file. When Spring finds an `@Autowired` annotation used with setter methods, it tries to perform byType autowiring on the method.

You can apply `@Autowired` to constructors as well. A constructor `@Autowired` annotation indicates that the constructor should be autowired when creating the bean, even if no `<constructor-arg>` elements are used while configuring the bean in XML file.

```java
public class TextEditor {
   private SpellChecker spellChecker;
 
   @Autowired
   public TextEditor(SpellChecker spellChecker){
      System.out.println("Inside TextEditor constructor." );
      this.spellChecker = spellChecker;
   }
 
   public void spellCheck(){
      spellChecker.checkSpelling();
   }
}
```

And it’s configuration without constructor arguments.

```java
<beans>
 
   <context:annotation-config/>
 
   <!-- Definition for textEditor bean without constructor-arg -->
   <bean id="textEditor" class="com.howtodoinjava.TextEditor">
   </bean>
 
   <!-- Definition for spellChecker bean -->
   <bean id="spellChecker" class="com.howtodoinjava.SpellChecker">
   </bean>
 
</beans>
```

### 8. Explain @Qualifier annotation with example?
`@Qualifier` means, which bean is qualify to autowired on a field. The qualifier annotation helps disambiguate bean references when Spring would otherwise not be able to do so.

See below example, it will autowired a “person” bean into customer’s person property.

```java
public class Customer
{
    @Autowired
    private Person person;
}
```

And we have two bean definitions for Person class.

```java
<bean id="customer" class="com.howtodoinjava.common.Customer" />
 
<bean id="personA" class="com.howtodoinjava.common.Person" >
    <property name="name" value="lokesh" />
</bean>
 
<bean id="personB" class="com.howtodoinjava.common.Person" >
    <property name="name" value="alex" />
</bean>
```

Will Spring know which person bean should autowired? NO. When you run above example, it hits below exception :

```java
Caused by: org.springframework.beans.factory.NoSuchBeanDefinitionException:
    No unique bean of type [com.howtodoinjava.common.Person] is defined:
        expected single matching bean but found 2: [personA, personB]
```
        
To fix above problem, you need `@Quanlifier` to tell Spring about which bean should autowired.

```java
public class Customer
{
    @Autowired
    @Qualifier("personA")
    private Person person;
}
```

### 9. Difference between constructor injection and setter injection?
Please find below the noticeable differences:

* In Setter Injection, partial injection of dependencies can possible, means if we have 3 dependencies like int, string, long, then its not necessary to inject all values if we use setter injection. If you are not inject it will takes default values for those primitives. In constructor injection, partial injection of dependencies is not possible, because for calling constructor we must pass all the arguments right, if not so we may get error.
* Setter Injection will overrides the constructor injection value, provided if we write setter and constructor injection for the same property. But, constructor injection cannot overrides the setter injected values. It’s obvious because constructors are called to first to create the instance.
* Using setter injection you can not guarantee that certain dependency is injected or not, which means you may have an object with incomplete dependency. On other hand constructor Injection does not allow you to construct object, until your dependencies are ready.
* In constructor injection, if Object A and B are dependent each other i.e A is depends on B and vice-versa, Spring throws ObjectCurrentlyInCreationException while creating objects of A and B because A object cannot be created until B is created and vice-versa. So spring can resolve circular dependencies through setter-injection because Objects are constructed before setter methods invoked.

### 10. What are the different types of events in spring framework?
Spring’s `ApplicationContext` provides the functionality to support events and listeners in code. We can create beans that listen for events which are published through our `ApplicationContext`. Event handling in the `ApplicationContext` is provided through the `ApplicationEvent` class and `ApplicationListener` interface. So if a bean implements the ApplicationListener, then every time an `ApplicationEvent` gets published to the `ApplicationContext`, that bean is notified.

```java
public class AllApplicationEventListener implements ApplicationListener < ApplicationEvent >
{
    @Override
    public void onApplicationEvent(ApplicationEvent applicationEvent)
    {
        //process event
    }
}
```

Spring provides the following **5 standard events**:

* **ContextRefreshedEvent :** This event is published when the ApplicationContext is either initialized or refreshed. This can also be raised using the refresh() method on the `ConfigurableApplicationContext` interface.
* **ContextStartedEvent :** This event is published when the `ApplicationContext` is started using the start() method on the `ConfigurableApplicationContext` interface. You can poll your database or you can re/start any stopped application after receiving this event.
* **ContextStoppedEvent :** This event is published when the `ApplicationContext` is stopped using the stop() method on the `ConfigurableApplicationContext` interface. You can do required house keeping work after receiving this event.
* **ContextClosedEvent :** This event is published when the `ApplicationContext` is closed using the close() method on the `ConfigurableApplicationContext` interface. A closed context reaches its end of life; it cannot be refreshed or restarted.
* **RequestHandledEvent :** This is a web-specific event telling all beans that an HTTP request has been serviced.

Apart from above, you can create your own custom events by extending `ApplicationEvent` class. e.g.

```java
public class CustomApplicationEvent extends ApplicationEvent
{
    public CustomApplicationEvent ( Object source, final String msg )
    {
        super(source);
        System.out.println("Created a Custom event");
    }
}
```

To listen this event, create a listener like this:

```java
public class CustomEventListener implements ApplicationListener < CustomApplicationEvent >
{
    @Override
    public void onApplicationEvent(CustomApplicationEvent applicationEvent) {
        //handle event
    }
}
```

And to publish this event, you will need the help of applicationContext instance.

```java
CustomApplicationEvent customEvent = new CustomApplicationEvent( applicationContext, "Test message" );
applicationContext.publishEvent ( customEvent );
```

### 11. Difference between FileSystemResource and ClassPathResource?
In `FileSystemResource` you need to give path of `spring-config.xml` (Spring Configuration) file relative to your project or the absolute location of the file.

In `ClassPathResource` spring looks for the file using `ClassPath` so `spring-config.xml` should be included in classpath. If `spring-config.xml` is in “src” so we can give just its name because src is in classpath path by default.

In one sentence, `ClassPathResource` looks in the class path and `FileSystemResource` looks in the file system.

### 12. Name some of the design patterns used in Spring Framework?
There are loads of different design patterns used, but there are a few obvious ones:

* **Proxy** – used heavily in AOP, and remoting.
* **Singleton** – beans defined in spring config files are singletons by default.
* **Template method** – used extensively to deal with boilerplate repeated code e.g. RestTemplate, JmsTemplate, JpaTemplate.
* **Front Controller** – Spring provides DispatcherServlet to ensure an incoming request gets dispatched to your controllers.
* **View Helper** – Spring has a number of custom JSP tags, and velocity macros, to assist in separating code from presentation in views.
* **Dependency injection** – Center to the whole BeanFactory / ApplicationContext concepts.
* **Factory pattern** – BeanFactory for creating instance of an object.
























