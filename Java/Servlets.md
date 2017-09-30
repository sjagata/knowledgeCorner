
## Servlet architecture overview ([Ref:](http://tutorialspointexamples.com/servlet-architecture-overview-in-java/))



- Web application:
A web application or website is an application program which accessed over a network connection using HTTP and often runs inside a web browser.

- Web browser:
A web browser is a program which is act as an interface between user and web application e.g. Internet Explorer, Chrome, Safari, Mozilla firefox etc.

- CGI (Common gateway interface):
CGI was the first protocol or way of communication between web server and program. It passes a request from a web user to an application program and receives data back to forward to the web user i.e. It is responsible for dynamic content generation.

**Advantages of CGI :** 
1. Technology portability: CGI programming can be written in variety of languages like c, c++, perl.
2. Web server portability: All service providers support CGI Programs.

**Disadvantages :** 
1. Response time is high.
2. CGI scripts are platform-dependent.
3. For every request, a new process will be started and web server is limited to start processes.
4. CGI programs are not object oriented always.

**Servlet overcomes the above disadvantages.**


<dl>
  <dt>Servlet as technology</dt>
  <dd>As a technology servlet provides a model of communication between a web user request and the application or program on the web server.</dd>
  
  
  <dt>Servlet as component</dt>
  <dd>As a component servlet is a program which is executed in web server and responsible for dynamic content generation.</dd>
  
  
  <dt>Main tasks of servlet</dt>
  <dd>1. Read the implicit and explicit data sent by web browser.
2. Generate result by processing the data.
3. Send the implicit and explicit data as a response to the web browser.
</dd>
  
  <dt>Servlet Packages</dt>
  <dd>**javax.servlet** and **javax.servlet.http** packages contains the classes and interfaces for servlet API. These packages are the standard part of Java’s enterprise edition.</dd>
  
  <dd>**javax.servlet** contains a number of classes and interfaces which are mainly used by servlet container.</dd>
  
  <dd>**javax.servlet.http** contains a number of classes and interfaces which are mainly used by http protocol.

</dd>
</dl>




## Life cycle of a servlet




Life cycle of a servlet is managed by web container.


**Servlet life cycle steps:**
1. Load Servlet Class.
2. Create Servlet instance.
3. Call init() method.
4. Call service() method.
5. Call destoy() method.


<dl>
  <dt>Load Servlet Class:</dt>
  <dd>Web container loads the servlet when the first request is received. This step is executed only once at the time of first request.</dd>
  
  
  <dt>Create Servlet instance:</dt>
  <dd>After loading the servlet class web container creates the servlet instance. Only one instance is created for a servlet and all concurrent requests are executed on the same servlet instance.</dd>
  
  
  <dt>Call init() method:</dt>
  <dd>After creating the servlet instance web container calls the servlet’s init method. This method is used to initialize the servlet before processing first request. It is called only once by the web container.</dd>
  
  
  <dt>Call service() method:</dt>
  <dd>After initialization process web container calls service method. Service method is called for every request. For every request servlet creates a separate thread.</dd>
  
  
  <dt>Call destoy() method:</dt>
  <dd>This method is called by web container before removing the servlet instance. Destroy method asks servlet to releases all the resources associated with it. It is called only once by the web container when all threads of the servlet have exited or in a timeout case.</dd>

</dl>
  
  
  
  
## Servlet interface in java



  
**Servlet interface:**
Servlet interface contains the common methods for all servlets i.e. provides the common behaviour for all servlets.

```java
public interface Servlet
```

Servlet interface is in javax.servlet package (**_javax.servlet.Servlet_**).



**Methods of servlet interface:**
1. init(ServletConfig config)
2. service(ServletRequest request,ServletResponse response)
3. destory()
4. getServletConfig()
5. getServletInfo()



<dl>
  <dt>init(ServletConfig config):</dt>
  <dd>It is used to initialize the servlet. This method is called only once by the web container when it loads the servlet.</dd>
</dl>

```java
// Syntax :
public void init(ServletConfig config) throws ServletException
```

<dl>  
  <dt>service(ServletRequest request,ServletResponse response):</dt>
  <dd>It is used to respond to a request. It is called for every new request by web container.</dd>
</dl>

```java
// Syntax :
public void service(ServletRequest req,ServletResponse res) throws ServletException, IOException
```

<dl> 
  <dt>destroy():</dt>
  <dd>It is used to destroy the servlet. This method is called only once by the web container when all threads of the servlet have exited or in a timeout case.</dd>
</dl>

```java
// Syntax :
public void destroy()
```

<dl> 
  <dt>getServletConfig():</dt>
  <dd>It returns a servlet config object. This config object is passed in init method.  Servlet config object contains initialization parameters and startup configuration for this servlet.</dd>
</dl>

```java
// Syntax :
public ServletConfig getServletConfig()
```

<dl> 
  <dt>getServletInfo():</dt>
  <dd>It returns a string of information about servlet’s author, version, and copyright etc..</dd>
</dl>

```java
// Syntax :
public String getServletInfo()
```


### Servlet “Hello World” example by implementing Servlet interface.

```java
//HelloWorld.java
package servlets;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.Servlet;
import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;

public class HelloWorld implements Servlet {

	ServletConfig config = null;

	@Override
	public void destroy() {
		System.out.println("Do clean-up process here.");
	}

	@Override
	public ServletConfig getServletConfig() {
		return config;
	}

	@Override
	public String getServletInfo() {
		return "Servlet Demo...";
	}

	@Override
	public void init(ServletConfig config) throws ServletException {
		this.config = config;
		System.out.println("Do initialization here.");
	}

	@Override
	public void service(ServletRequest arg0, ServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		out.println("<h1>Hello World example using " + "servlet interface.</h1>");
		out.close();
	}

}

```

```java
// web.xml

<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.4" xmlns="http://java.sun.com/xml/ns/j2ee"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee
http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd">

	<servlet>
		<servlet-name>Servlet Name For Demo1</servlet-name>
		<servlet-class>servlets.ServletDemo</servlet-class>
	</servlet>

	<servlet-mapping>
		<servlet-name>Servlet Name For Demo1</servlet-name>
		<url-pattern>/Demo1</url-pattern>
	</servlet-mapping>

	<servlet>
		<servlet-name>HelloWorld</servlet-name>
		<servlet-class>servlets.HelloWorld</servlet-class>
	</servlet>

	<servlet-mapping>
		<servlet-name>HelloWorld</servlet-name>
		<url-pattern>/HelloWorld</url-pattern>
	</servlet-mapping>
</web-app>

```





## GenericServlet class in java

**GenericServlet class :**

GenericServlet class implements the Servlet and ServletConfig interfaces. GenericServlet  is protocol-independent. It not provides the implementation of service method.

```java
public abstract class GenericServlet implements Servlet, ServletConfig
```

GenericServlet class is in javax.servlet package (**_javax.servlet.GenericServlet_**).

**Methods of GenericServlet class:**
1. init(ServletConfig config)
2. service(ServletRequest request,ServletResponse response)
3. destroy()
4. getServletConfig()
5. getServletInfo()
6. Init()
7. getServletContext()
8. getInitParameter(String name)
9. getInitParameterNames()
10. getServletName()
11. log(String msg)
12. log(String msg, Throwable t)





1. init(ServletConfig config): It is used to initialize the servlet. This method is called only once by the web container when it loads the servlet.

Syntax: public void init(ServletConfig config)throws ServletException

2. service(ServletRequest request,ServletResponse response): It is used to respond to a request. It is called for every new request by web container.

Syntax: public abstract void service(ServletRequest req,ServletResponse res)throws ServletException, IOException

3. destroy(): It is used to destroy the servlet. This method is called only once by the web container when all threads of the servlet have exited or in a timeout case.

Syntax: public void destroy()

4. getServletConfig(): It returns a servlet config object. This config object is passed in init method.  Servlet config object contains initialization parameters and startup configuration for this servlet.

Syntax: public ServletConfig getServletConfig()

5. getServletInfo(): It returns a string of information about servlet’s author, version, and copyright etc.

Syntax: public String getServletInfo()

6. Init(): It is a convenience method which can be overridden so that there is no need to call super.init(config).

Syntax: public void init() throws ServletException

7. getServletContext():It returns the ServletContext object in which this servlet is running.

Syntax: public ServletContext getServletContext()

8. getInitParameter(String name): It returns the value for given parameter name. It returns null if parameter not exist.

Syntax: public String getInitParameter(String name)

9. getInitParameterNames(): It returns the names of the servlet’s initialization parameters defined in web.xml file.

Syntax: public Enumeration getInitParameterNames()

10. getServletName(): It returns the name of this servlet object.

Syntax: public String getServletName()

11. log(String msg): This method writes the specified message to the servlet log file.

Syntax: public void log(String msg)

12. log(String msg,Throwable t): This method writes an explanatory message and a stack trace for a given exception to the servlet log file.

Syntax: public void log(String msg,Throwable t).


























