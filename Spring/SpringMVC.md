# Spring MVC

## What is Spring MVC?
* Framework for building web applications in Java
* Based on Model-View-Controller design pattern
* Leverages features of the Core Spring Framework (IoC, DI)

## Model-View-Controller (MVC)
[logo]: https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Spring/images/mvc.png "Spring MVC"

## Spring MVC Benefits
* The Spring way of building web app UIs in Java
* Leverage a set of reusable UI components
* Help manage application state for web requests
* Process form data: validation, conversion etc
* Flexible configuration for the view layer

## Components of a Spring MVC Application
* A set of web pages to layout UI components **[Web Pages]**
* A collection of Spring beans (controllers, services, etc…) **[Beans]**
* Spring configuration (XML, Annotations or Java) **[Spring Configuration]**

## Spring MVC Front Controller
* Front controller known as DispatcherServlet
	* Part of the Spring Framework
	* Already developed by Spring Dev Team
* You will create
	* Model objects (orange)
	* View templates (dark green)
	* Controller classes (yellow)
[logo]: https://github.com/SandeepJagatha/knowledgeCorner/blob/master/Spring/images/mvc.png "Spring MVC"

## Controller
* Code created by developer
* Contains your business logic
	* Handle the request
	* Store/retrieve data (db, web service…)
	* Place data in model
* Send to appropriate view template

## Model
* Model: contains your data
* Store/retrieve data via backend systems
	* database, web service, etc…
	* Use a Spring bean if you like
* Place your data in the model
	* Data can be any Java object/collection

## View Template
* Spring MVC is flexible
	* Supports many view templates
* Most common is JSP + JSTL
* Developer creates a page
	* Displays data

<hr>

<br>
<br>
<br>

[reference](http://tutorialspointexamples.com)

Spring mvc framework provides the facility to build flexible and loosely coupled web applications. MVC stands for Model-View-Controller design pattern which separates the business logic, presentation logic and navigation logic.

**Model:**
Model is responsible for encapsulating the application data (POJO).

**View:**
View is responsible for rendering the model data.

**Controller:**
Controller is responsible for receiving the user request, building model object and passing the model object to the view.

_Spring MVC framework uses the DispatcherServlet class as the controller which is responsible for handling all the requests and responses._ 

![alt text][logo]

[logo]: http://tutorialspointexamples.com/wp-content/uploads/2015/12/SpringMVCFlowDiagram.jpg "Spring MVC"

### Spring mvc framework execution flow:

* Receive the user request.
* Choose the controller with the help of HandlerMapping.
* Controller process the request by calling the appropriate service method and returns a ModeAndView object to the DispatcherServlet which contains the model data and view name.
* DispatcherServlet sends the view name to ViewResolver which sends the actual view to the DispatcherServlet.
* DispatcherServlet will pass the model data to the View and render response.

<br>

## Spring MVC configuration file

### web.xml file:

The web.xml file contains the entry of DispatcherServlet for handling the requests. Keep the web.xml file in WebContent/WEB-INF directory of your application. Spring framework first initialize the DispatcherServlet and then load the application context from file [servlet-name]-servlet.xml in WebContent/WEB-INF directory.

### Example:

```java
<?xml version="1.0" encoding="UTF-8"?>  
<web-app version="2.4"
   xmlns="http://java.sun.com/xml/ns/j2ee" 
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee 
   http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd">
 
   <servlet>
      <servlet-name>HelloWorld</servlet-name>
      <servlet-class>
         org.springframework.web.servlet.DispatcherServlet
      </servlet-class>
      <load-on-startup>1</load-on-startup>
   </servlet>
 
   <servlet-mapping>
      <servlet-name>HelloWorld</servlet-name>
      <url-pattern>*.html</url-pattern>
   </servlet-mapping>
 
</web-app>
```

_Note: The [servlet-name]-servlet.xml is the default name and WebContent/WEB-INF is the default location for application context file. If we want to use some other name or location we have to inform spring framework by adding ContextLoaderListener in web.xml file._

```java
<web-app...>
 
<!-------- DispatcherServlet definition ----->
....
<context-param>
   <param-name>contextConfigLocation</param-name>
   <param-value>/WEB-INF/HelloWorld-servlet.xml</param-value>
</context-param>
 
<listener>
   <listener-class>
      org.springframework.web.context.ContextLoaderListener
   </listener-class>
</listener>
</web-app>
```

### [servlet-name]-servlet.xml:

Spring framework loads the application context from [servlet-name]-servlet.xml file. It is used to create or override the beans definitions. The context:component-scan tag is used to activate Spring MVC annotation scanning. The InternalResourceViewResolver is used to define the rules to resolve the view names.

```java
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"
   xmlns:context="http://www.springframework.org/schema/context"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="
   http://www.springframework.org/schema/beans     
   http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
   http://www.springframework.org/schema/context 
   http://www.springframework.org/schema/context/spring-context-3.0.xsd">
 
   <context:component-scan base-package="springmvc" />
 
   <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
      <property name="prefix" value="/WEB-INF/jsp/" />
      <property name="suffix" value=".jsp" />
   </bean>
 
</beans>
```

### Controller:

A controller is responsible for executing the specific functionality for a request. The **@Controller** annotation is used define a class as Spring MVC controller. The **@RequestMapping** annotation is used to map a request URL. A request URL can be mapped to an entire class or a particular method.

```java
@Controller
public class HelloController {
	   @RequestMapping("/sayHello")  
	   public ModelAndView sayHello() {
	      String message = "Spring MVC Hello World Example.";
	      return new ModelAndView("helloWorld", "message", message);  
	   }
}
```

<br>

## Spring MVC hello world tutorial

Spring mvc framework provides the facility to build flexible and loosely coupled web applications. MVC stands for Model-View-Controller design pattern which separates the business logic, presentation logic and navigation logic. 

### Example:

Use http://localhost:8080/SpringMVCExample1/ url to start the application. When you click on “Say Hello” link, a request for sayHello.html will generate. Request will be handled by DispatcherServlet. It delegates the request to the HelloController controller. The HelloController controller resolve the request with help of RequestMapping annotation, executes the specific functionality and returns the ModelAndView object to the DispatcherServlet. The DispatcherServlet then take the help of InternalResourceViewResolver to get the actual view name. In our example it will return the “/WEB-INF/jsp/helloWorld.jsp”. The DispatcherServlet then insert the model data into view and render response.

web.xml

```java
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.5" xmlns="http://java.sun.com/xml/ns/javaee"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd">

	<!-- The definition of the Root Spring Container shared by all Servlets and Filters -->
	<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>/WEB-INF/spring/root-context.xml</param-value>
	</context-param>
	
	<!-- Creates the Spring Container shared by all Servlets and Filters -->
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>

	<!-- Processes application requests -->
	<servlet>
		<servlet-name>appServlet</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<init-param>
			<param-name>contextConfigLocation</param-name>
			<param-value>/WEB-INF/spring/appServlet/servlet-context.xml</param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>
		
	<servlet-mapping>
		<servlet-name>appServlet</servlet-name>
		<url-pattern>/</url-pattern>
	</servlet-mapping>

</web-app>
```

servlet-context.xml

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans:beans xmlns="http://www.springframework.org/schema/mvc"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:beans="http://www.springframework.org/schema/beans"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd
		http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

	<!-- DispatcherServlet Context: defines this servlet's request-processing infrastructure -->
	
	<!-- Enables the Spring MVC @Controller programming model -->
	<annotation-driven />

	<!-- Handles HTTP GET requests for /resources/** by efficiently serving up static resources in the ${webappRoot}/resources directory -->
	<resources mapping="/resources/**" location="/resources/" />

	<!-- Resolves views selected for rendering by @Controllers to .jsp resources in the /WEB-INF/views directory -->
	<beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<beans:property name="prefix" value="/WEB-INF/views/" />
		<beans:property name="suffix" value=".jsp" />
	</beans:bean>
	
	<context:component-scan base-package="com.tutorials.springmvc" />
	
</beans:beans>
```

HomeController.java

```java
package com.tutorials.springmvc;

import java.text.DateFormat;
import java.util.Date;
import java.util.Locale;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

/**
 * Handles requests for the application home page.
 */
@Controller
public class HomeController {

	private static final Logger logger = LoggerFactory.getLogger(HomeController.class);

	@RequestMapping(value = "/", method = RequestMethod.GET)
	public String home(Locale locale, Model model) {
		logger.info("Welcome home! The client locale is {}.", locale);

		Date date = new Date();
		DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG, locale);

		String formattedDate = dateFormat.format(date);

		model.addAttribute("serverTime", formattedDate);

		return "home";
	}

}
```

<br>

## Spring MVC multiple controller

* Use http://localhost:8080/SpringMVCExample3/ url to start the application. 
* When you click on any link, a request for respective resource will generate. 
* Request will be handled by DispatcherServlet. 
* The DispatcherServlet choose the controller with the help of HandlerMapping. 
* It delegates the request to the specified controller. 
* The specified controller resolve the request with help of RequestMapping annotation, executes the specific functionality and returns the ModelAndView object to the DispatcherServlet. 
* The DispatcherServlet then take the help of InternalResourceViewResolver to get the actual view name. 
* The DispatcherServlet then insert the model data into view and render response.

<br>

## Spring mvc login 

LoginController.java

```java
package com.tutorials.springmvc;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;

@Controller
public class LoginController {

	@RequestMapping("/login")
	public ModelAndView login(HttpServletRequest request, HttpServletResponse response) {
		String userName = request.getParameter("userName");
		String password = request.getParameter("password");
		String message;
		if (userName != null && !userName.equals("") && userName.equals("test") && password != null
				&& !password.equals("") && password.equals("123")) {
			message = "Welcome " + userName + ".";
			return new ModelAndView("welcome", "message", message);

		} else {
			message = "Wrong username or password.";
			return new ModelAndView("errorPage", "message", message);
		}
	}
}
```


<br>

## Spring MVC exception handling

### Example :

* Use http://localhost:8080/SpringMVCExample6/ student url to start the application. 
* A request for respective resource will generate. 
* Request will be handled by DispatcherServlet. 
* It delegates the request to the ExceptionHandlingController controller. 
* The LoginController controller resolve the request with help of RequestMapping annotation, executes the specific functionality and returns the ModelAndView object to the DispatcherServlet. 
* The DispatcherServlet then take the help of InternalResourceViewResolver to get the actual view name. 
* In our example it will return the “/WEB-INF/jsp/student.jsp. 
* The DispatcherServlet then insert the model data into view and render response. Same request response cycle will execute when we click on submit button after entering the student details.

ExceptionHandling-servlet.xml

```java
<bean class=
   "org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
   <property name="exceptionMappings">
      <props>
         <prop key="springmvc.SpringException">
            exceptionpage
         </prop>
      </props>
   </property>
   <property name="defaultErrorView" value="error"/>
  </bean>
```

ExceptionHandlingController.java

```java
@Controller
public class ExceptionHandlingController {
   @RequestMapping(value = "/student", method = RequestMethod.GET)
   public ModelAndView student() {
      return new ModelAndView("student", "command", new Student());
   }
 
   @RequestMapping(value = "/addStudent", method = RequestMethod.POST)
   @ExceptionHandler({SpringException.class})
   public String addStudent(@ModelAttribute("SpringWeb")Student student, ModelMap model) {
      if(student.getName().length() < 5 ){
         throw new SpringException("Student name should contain atleast 5 characters.");
      }else{
    	  model.addAttribute("name", student.getName());
      }
 
      model.addAttribute("className", student.getClassName());     
      model.addAttribute("rollNo", student.getRollNo());
 
      return "welcome";
   }
}
```













































