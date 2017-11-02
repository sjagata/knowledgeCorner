### What is Spring MVC framework?

**The Spring web MVC framework provides model-view-controller architecture and ready components that can be used to develop flexible and loosely coupled web applications.** The MVC pattern results in separating the different aspects of the application (input logic, business logic, and UI logic), while providing a loose coupling between model, view and controller parts of application. Spring framework provides lots of advantages over other MVC frameworks e.g.

1. Clear separation of roles – controller, validator, command object, form object, model object, DispatcherServlet, handler mapping, view resolver, etc. Each role can be fulfilled by a specialized object.
2. Powerful and straightforward configuration of both framework and application classes as JavaBeans.
3. Reusable business code – no need for duplication. You can use existing business objects as command or form objects instead of mirroring them in order to extend a particular framework base class.
4. Customizable binding and validation
5. Customizable handler mapping and view resolution
6. Customizable locale and theme resolution
7. A JSP form tag library, introduced in Spring 2.0, that makes writing forms in JSP pages much easier. etc.

### What is DispatcherServlet and ContextLoaderListener?
Spring’s web MVC framework is, like many other web MVC frameworks, request-driven, designed around a central Servlet that handles all the HTTP requests and responses. Spring’s DispatcherServlet however, does more than just that. It is completely integrated with the Spring IoC container so it allows you to use every feature that Spring has.


1. **After receiving an HTTP request**, **DispatcherServlet** consults the **HandlerMapping** (configuration files) to **call the appropriate Controller.**
2. The **Controller** takes the request and **calls the appropriate service methods** and **set model data** and then **returns view name to the DispatcherServlet.** 
3. The **DispatcherServlet** will take help from **ViewResolver** to **pickup the defined view for the request.** 
4. Once view is finalized, The **DispatcherServlet passes the model data** to the **view** which is finally rendered on the browser.

```java
<web-app>
  <display-name>Archetype Created Web Application</display-name>
   
  <servlet>
        <servlet-name>spring</servlet-name>
            <servlet-class>
                org.springframework.web.servlet.DispatcherServlet
            </servlet-class>
        <load-on-startup>1</load-on-startup>
    </servlet>
 
    <servlet-mapping>
        <servlet-name>spring</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
     
</web-app>
```

By default, `DispatcherServlet` loads its configuration file using <servlet_name>-servlet.xml. E.g. with above web.xml file, DispatcherServlet will try to find spring-servlet.xml file in classpath.

`ContextLoaderListener` reads the spring configuration file (with value given against “contextConfigLocation” in web.xml), parse it and loads the beans defined in that config file. e.g.

```java
<servlet>
    <servlet-name>spring</servlet-name>
    <servlet-class>
        org.springframework.web.servlet.DispatcherServlet
    </servlet-class>
     
    <init-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/applicationContext.xml</param-value>
    </init-param>
     
    <load-on-startup>1</load-on-startup>
</servlet>
```

### What is the front controller class of Spring MVC?
A front controller is defined as **“a controller which handles all requests for a Web Application.”** `DispatcherServlet` (actually a servlet) is the front controller in Spring MVC that intercepts every request and then dispatches/forwards requests to an appropriate controller.

When a web request is sent to a Spring MVC application, dispatcher servlet first receives the request. Then it organizes the different components configured in Spring’s web application context (e.g. actual request handler controller and view resolvers) or annotations present in the controller itself, all needed to handle the request.

### How can we use Spring to create Restful Web Service returning JSON response?

For adding JSON support to your spring application, you will need to add `Jackson dependency` in first step.

```java
<!-- Jackson JSON Processor -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.4.1</version>
</dependency>
```

Now you are ready to return JSON response from your MVC controller. All you have to do is return JAXB annotated object from method and use `@ResponseBody` annotation on this return type.

```java
@Controller
public class EmployeeRESTController
{
    @RequestMapping(value = "/employees")
    public @ResponseBody EmployeeListVO getAllEmployees()
    {
        EmployeeListVO employees = new EmployeeListVO();
        //Add employees
        return employees;
    }
}
```

Alternatively, you can use `@RestController` annotation in place of `@Controller` annotation. This will remove the need to using `@ResponseBody`.

> @RestController = @Controller + @ResponseBody

```java
@RestController
public class EmployeeRESTController
{
    @RequestMapping(value = "/employees")
    public EmployeeListVO getAllEmployees()
    {
        EmployeeListVO employees = new EmployeeListVO();
        //Add employees
        return employees;
    }
}
```

### Can we have multiple Spring configuration files?
YES. You can have multiple spring context files. There are two ways to make spring read and configure them.

a) Specify all files in web.xml file using contextConfigLocation init parameter.

```java
<servlet>
        <servlet-name>spring</servlet-name>
        <servlet-class>
            org.springframework.web.servlet.DispatcherServlet
        </servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>
                WEB-INF/spring-dao-hibernate.xml,
                WEB-INF/spring-services.xml,
                WEB-INF/spring-security.xml
            </param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
 
    <servlet-mapping>
        <servlet-name>spring</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
```

b) OR, you can import them into existing configuration file you have already configured.

```java
<beans>
    <import resource="spring-dao-hibernate.xml"/>
    <import resource="spring-services.xml"/>
    <import resource="spring-security.xml"/>
     
    ... //Other configuration stuff
 
</beans>
```

### Difference between <context:annotation-config> vs <context:component-scan>?

1) First big difference between both tags is that `<context:annotation-config> is **used to activate applied annotations in already registered beans in application context.** Note that it simply does not matter whether bean was registered by which mechanism e.g. using <context:component-scan> or it was defined in application-context.xml file itself.

2) Second difference is driven from first difference itself. It **registers the beans defined in config file into context + it also scans the annotations inside beans and activate them.** So <context:component-scan> does what <context:annotation-config> does, but additionally it scan the packages and register the beans in application context.

> `<context:annotation-config>` = Scanning and activating annotations in “already registered beans”.
> `<context:component-scan>` = Bean Registration + Scanning and activating annotations

### Difference between @Component, @Controller, @Repository & @Service annotations?

* The `@Component` annotation marks a java class as a bean so the component-scanning mechanism of spring can pick it up and pull it into the application context. To use this annotation, apply it over class as below:

```java
@Component
public class EmployeeDAOImpl implements EmployeeDAO {
    ...
}
```

* The `@Repository` annotation is a specialization of the `@Component annotation with similar use and functionality. In addition to importing the DAOs into the DI container, it also makes the unchecked exceptions (thrown from DAO methods) eligible for translation into Spring `DataAccessException`.

* The `@Service annotation is also a specialization of the component annotation. It doesn’t currently provide any additional behavior over the @Component annotation, but it’s a good idea to use `@Service` over `@Component` in service-layer classes because it specifies intent better.

* `@Controller` annotation marks a class as a Spring Web MVC controller. It too is a `@Component` specialization, so beans marked with it are automatically imported into the DI container. When you add the @Controller annotation to a class, you can use another annotation i.e. `@RequestMapping;` to map URLs to instance methods of a class.

### What does the ViewResolver class?
`ViewResolver` is an interface to be implemented by objects that can resolve views by name. There are plenty of ways using which you can resolve view names. These ways are supported by various in-built implementations of this interface. Most commonly used implementation is InternalResourceViewResolver class. It defines prefix and suffix properties to resolve the view component.

```java
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/views/" />
    <property name="suffix" value=".jsp" />
</bean>
```

So with above view resolver configuration, if controller method return `“login”` string, then the `“/WEB-INF/views/login.jsp”` file will be searched and rendered.

### What is a MultipartResolver and when its used?
Spring comes with MultipartResolver to handle file upload in web application. There are two concrete implementations included in Spring:

1. **CommonsMultipartResolver** for Jakarta Commons FileUpload
2. **StandardServletMultipartResolver** for Servlet 3.0 Part API

To define an implementation, create a bean with the id “multipartResolver” in a DispatcherServlet’s application context. Such a resolver gets applied to all requests handled by that DispatcherServlet.

If a DispatcherServlet detects a multipart request, it will resolve it via the configured MultipartResolver and pass on a wrapped HttpServletRequest. Controllers can then cast their given request to the MultipartHttpServletRequest interface, which permits access to any MultipartFiles.

### What is Spring MVC Interceptor and how to use it?
As you know about `servlet filters` that they can pre-handle and post-handle every web request they serve — before and after it’s handled by that servlet. In the similar way, you can use `HandlerInterceptor` interface in your spring mvc application **to pre-handle and post-handle web requests** that are handled by Spring MVC controllers. These handlers are mostly used to manipulate the model attributes returned/submitted they are passed to the views/controllers.

A handler interceptor can be registered for particular URL mappings, so it only intercepts requests mapped to certain URLs. Each handler interceptor must implement the `HandlerInterceptor` interface, which contains three callback methods for you to implement: `preHandle()`, `postHandle()` and `afterCompletion()`.

Problem with `HandlerInterceptor` interface is that your new class will have to implement all three methods irrespective of whether it is needed or not. To avoid overriding, you can use `HandlerInterceptorAdapter` class. This class implements `HandlerInterceptor` and provide default blank implementations.

### How to handle exceptions in Spring MVC Framework?
In a Spring MVC application, you can register one or more exception resolver beans in the web application context to resolve uncaught exceptions. These beans have to implement the `HandlerExceptionResolver` interface for `DispatcherServlet` to auto-detect them. Spring MVC comes with a simple exception resolver for you to map each category of exceptions to a view i.e. `SimpleMappingExceptionResolver` to map each category of exceptions to a view in a configurable way.

Let’s say we have an exception class i.e. `AuthException`. And we want that everytime this exception is thrown from anywhere into application, we want to show a pre-determined view page `/WEB-INF/views/error/authExceptionView.jsp`. So the configuration would be.

```java
<bean class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
    <property name="exceptionMappings">
        <props>
            <prop key="com.howtodoinjava.demo.exception.AuthException">
                error/authExceptionView
            </prop>
        </props>
    </property>
    <property name="defaultErrorView" value="error/genericView"/>
</bean>
```

The “**defaultErrorView**” property can be configured to show a generic message for all other exceptions which are not configured inside “exceptionMappings” list.

### How to get ServletContext and ServletConfig object in a Spring Bean?
Simply implement `ServletContextAware` and `ServletConfigAware` interfaces and override below methods.

```java
@Controller
@RequestMapping(value = "/magic")
public class SimpleController implements ServletContextAware, ServletConfigAware {
 
    private ServletContext context;
    private ServletConfig config;
 
    @Override
    public void setServletConfig(final ServletConfig servletConfig) {
        this.config = servletConfig;
 
    }
 
    @Override
    public void setServletContext(final ServletContext servletContext) {
        this.context = servletContext;
    }
     
    //other code
}
```

### How would you relate Spring MVC Framework to 3 tier architecture?

![alt text](https://howtodoinjava.com/wp-content/uploads/2015/02/3-tier-architechture-with-mvc-part-of-it.png "MVC 3tier")























































































