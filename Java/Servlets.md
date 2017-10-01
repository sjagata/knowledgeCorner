
# Servlet architecture overview ([ref:](http://tutorialspointexamples.com/servlet-architecture-overview-in-java/))



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




# Life cycle of a servlet




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
  
  
  
  
# Servlet interface in java



  
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


### Servlet “ServletDemo” example by implementing Servlet interface.

```java

// ServletDemo.java

package servlets;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.Servlet;
import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;

public class ServletDemo implements Servlet {

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
		<servlet-name>ServletDemo</servlet-name>
		<servlet-class>servlets.ServletDemo</servlet-class>
	</servlet>

	<servlet-mapping>
		<servlet-name>ServletDemo</servlet-name>
		<url-pattern>/ServletDemo</url-pattern>
	</servlet-mapping>
</web-app>

```





# GenericServlet class in java

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

<dl> 
  <dt>Init(): </dt>
  <dd>It is a convenience method which can be overridden so that there is no need to call super.init(config).</dd>
</dl>

```java
public void init() throws ServletException
```

<dl> 
  <dt>getServletContext():</dt>
  <dd>It returns the ServletContext object in which this servlet is running.</dd>
</dl>

```java
public ServletContext getServletContext()
```

<dl> 
  <dt>getInitParameter(String name):</dt>
  <dd> It returns the value for given parameter name. It returns null if parameter not exist.</dd>
</dl>

```java
public String getInitParameter(String name)
```

<dl> 
  <dt>getInitParameterNames():</dt>
  <dd> It returns the names of the servlet’s initialization parameters defined in web.xml file.</dd>
</dl>

```java
public Enumeration getInitParameterNames()
```

<dl> 
  <dt>getServletName():</dt>
  <dd> It returns the name of this servlet object.</dd>
</dl>

```java
public String getServletName()
```

<dl> 
  <dt>log(String msg):</dt>
  <dd> This method writes the specified message to the servlet log file.</dd>
</dl>

```java
public void log(String msg)
```

<dl> 
  <dt>log(String msg,Throwable t):</dt>
  <dd> This method writes an explanatory message and a stack trace for a given exception to the servlet log file.</dd>
</dl>

```java
public void log(String msg,Throwable t)
```



### Servlet “GenericServletDemo” example by extending GenericServlet class.

```java

// GenericServletDemo.java

package servlets;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.GenericServlet;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;

public class GenericServletDemo extends GenericServlet {

	private static final long serialVersionUID = 1L;

	@Override
	public void service(ServletRequest request, ServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		out.println("<h1>Hello World example using" + " GenericServlet class.</h1>");
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
		<servlet-name>GenericServletDemo</servlet-name>
		<servlet-class>servlets.GenericServletDemo</servlet-class>
	</servlet>

	<servlet-mapping>
		<servlet-name>GenericServletDemo</servlet-name>
		<url-pattern>/GenericServletDemo</url-pattern>
	</servlet-mapping>
</web-app>

```


# HttpServlet class in java

**HttpServlet class:**

HttpServlet class extends the GenericServlet. It is protocol-dependent.

```java
public abstract class HttpServlet extends GenericServlet
```

HttpServlet class is in javax.servlet.http package (**_javax.servlet.http.HttpServlet_**).


**Methods of HttpServlet class:**
1. service(ServletRequest req,ServletResponse res)
2. service(HttpServletRequest req, HttpServletResponse res)
3. doGet(HttpServletRequest req, HttpServletResponse res)
4. doPost(HttpServletRequest req, HttpServletResponse res)
5. doHead(HttpServletRequest req, HttpServletResponse res)
6. doOptions(HttpServletRequest req, HttpServletResponse res)
7. doPut(HttpServletRequest req, HttpServletResponse res)
8. doTrace(HttpServletRequest req, HttpServletResponse res)
9. doDelete(HttpServletRequest req, HttpServletResponse res)
10. getLastModified(HttpServletRequest req)


<dl>  
  <dt>service(ServletRequest request,ServletResponse response):</dt>
  <dd>Dispatches the requests to the protected service method. It converts the request and response object into http type before dispatching request.</dd>
</dl>

```java
// Syntax :
public void service(ServletRequest req,ServletResponse res) throws ServletException, IOException
```

<dl>  
  <dt>service(HttpServletRequest req, HttpServletResponse res):</dt>
  <dd>Receives HTTP requests from the public service method and dispatches the request to the doXXX methods defined in this class.</dd>
</dl>

```java
protected void service(HttpServletRequest req, HttpServletResponse res) throws ServletException,IOException
```

<dl>  
  <dt>doGet(HttpServletRequest req, HttpServletResponse res): </dt>
  <dd>This method is called by web container for handling GET requests.</dd>
</dl>

```java
protected void doGet(HttpServletRequest req, HttpServletResponse res) throws ServletException,IOException
```

<dl>  
  <dt>doPost(HttpServletRequest req, HttpServletResponse res): </dt>
  <dd>This method is called by web container for handling POST requests.</dd>
</dl>

```java
protected void doPost(HttpServletRequest req, HttpServletResponse res) throws ServletException,IOException
```

<dl>  
  <dt>doHead(HttpServletRequest req, HttpServletResponse res): </dt>
  <dd>This method is called by web container for handling HEAD requests.</dd>
</dl>

```java
protected void doHead(HttpServletRequest req, HttpServletResponse res) throws ServletException,IOException
```

<dl>  
  <dt>doOptions(HttpServletRequest req, HttpServletResponse res): </dt>
  <dd>This method is called by web container for handling OPTIONS requests.</dd>
</dl>

```java
protected void doOptions(HttpServletRequest req, HttpServletResponse res) throws ServletException,IOException
```

<dl>  
  <dt>doPut(HttpServletRequest req, HttpServletResponse res): </dt>
  <dd>This method is called by web container for handling PUT requests.</dd>
</dl>

```java
protected void doPut(HttpServletRequest req, HttpServletResponse res) throws ServletException,IOException
```

<dl>  
  <dt>doTrace(HttpServletRequest req, HttpServletResponse res): </dt>
  <dd>This method is called by web container for handling TRACE requests.</dd>
</dl>

```java
protected void doTrace(HttpServletRequest req, HttpServletResponse res) throws ServletException,IOException
```

<dl>  
  <dt>doDelete(HttpServletRequest req, HttpServletResponse res): </dt>
  <dd>This method is called by web container for handling DELETE requests.</dd>
</dl>

```java
protected void doDelete(HttpServletRequest req, HttpServletResponse res) throws ServletException,IOException
```

<dl>  
  <dt>getLastModified(HttpServletRequest req): </dt>
  <dd>It returns the time the HttpServletRequest  object was last modified since midnight January 1, 1970 GMT. It returns a negative number if time is unknown.</dd>
</dl>

```java
protected long getLastModified(HttpServletRequest req)
```





### Servlet “HttpServletDemo” example by extending HttpServlet class.

```java

// HttpServletDemo.java

package servlets;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class HttpServletDemo extends HttpServlet {

	private static final long serialVersionUID = 1L;

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		out.println("<h1>Hello World using HttpServlet class.</h1>");
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
		<servlet-name>HttpServletDemo</servlet-name>
		<servlet-class>servlets.HttpServletDemo</servlet-class>
	</servlet>

	<servlet-mapping>
		<servlet-name>HttpServletDemo</servlet-name>
		<url-pattern>/HttpServletDemo</url-pattern>
	</servlet-mapping>
</web-app>

```



# Deployment Descriptor: web.xml file

**Deployment Descriptor:** 

In a java web application a file named web.xml is known as deployment descriptor. It is a xml file and <web-app> is the root element for it. When a request comes web server uses web.xml file to map the URL of the request to the specific code that handle the request.

```java
// sample code of web.xml file
<web-app>

	<servlet>
		<servlet-name>servletName</servlet-name>
		<servlet-class>servletClass</servlet-class>
	</servlet>

	<servlet-mapping>
		<servlet-name>servletName</servlet-name>
		<url-pattern>*.*</url-pattern>
	</servlet-mapping>

</web-app>
```

**How web.xml works:** 

When a request comes it is matched with url pattern in servlet mapping attribute. In the above example all urls mapped with the servlet. You can specify a url pattern according to your need. When url matched with url pattern web server try to find the servlet name in servlet attributes same as in servlet mapping attribute. When match found control is goes to the associated servlet class.


### Servlet “Hello World” example by extending HttpServlet class.


```java

// HelloWorld.java

package servlets;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class HelloWorld extends HttpServlet {

	private static final long serialVersionUID = 1L;

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		out.println("<h1>Hello World using HttpServlet class.</h1>");
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
		<servlet-name>HelloWorld</servlet-name>
		<servlet-class>servlets.HelloWorld</servlet-class>
	</servlet

	<servlet-mapping>
		<servlet-name>HelloWorld</servlet-name>
		<url-pattern>/HelloWorld</url-pattern>
	</servlet-mapping>
</web-app>

```



# welcome-file-list in web.xml

**welcome-file-list:**

The welcome-file-list attribute of web.xml file is used to define the list of welcome files.

**Sample code of welcome-file-list attribute in web.xml:**

```java
<web-app>

	//other attributes

	<welcome-file-list>
		<welcome-file>home.html</welcome-file>
		<welcome-file>welcome.html</welcome-file>
	</welcome-file-list>

	//other attributes

</web-app>

```

**How it works:**

First web server looks for welcome-file-list if it exist then it looks for file defined in first welcome-file. If this file exists then control is transferred to this file otherwise web server will look at the next welcome file and so on.

If the welcome-file-list is not exists or files defined in welcome-file-list are not exists then server will looks at the default welcome files in following order **_index.html, index.htm, index.jsp, default.html, default.htm and default.jsp._**

**Default welcome file list:**

```java
<welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.htm</welcome-file>
    <welcome-file>default.jsp</welcome-file>
</welcome-file-list>
```

**Example of welcome-file-list:**

```java

// web.xml

<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="http://java.sun.com/xml/ns/javaee" xmlns:web="http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee 
http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
	id="WebApp_ID" version="2.5">

	<welcome-file-list>
		<welcome-file>welcome.html</welcome-file>
	</welcome-file-list>

</web-app>
```

```java

// welcome.html

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 
Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<title>welcome</title>
</head>
<body>
	<h1>This is a welcome file list program.</h1>
</body>
</html>

```



# load-on-startup in web.xml

**load-on-startup:**

The load-on-startup is the sub attribute of servlet attribute in web.xml. It is used to control when the web server loads the servlet. As we discussed that servlet is loaded at the time of first request. In this case response time is increased for first request. If load-on-startup is specified for a servlet in web.xml then this servlet will be loaded when the server starts. So the response time will not increase for fist request.

Any positive or negative value can be passed in the load-on-startup. If positive value is passed then all servlets having load-on-startup sub attribute will be loaded when server starts but a servlet having low positive value will be loaded first. In case of negative value servlet will be loaded at the time of first request.

**Sample code of load-on-startup in web.xml.**

```java
<web-app>
 
   //other attributes  
 
   <servlet>  
 	<servlet-name>servlet1</servlet-name>  
  	<servlet-class>com.javawithease.business.Servlet1 </servlet-class>
   	<load-on-startup>0</load-on-startup>  
   </servlet>  
 
  <servlet>  
  	 <servlet-name>servlet2</servlet-name>  
   	<servlet-class> com.javawithease.business.Servlet2</servlet-class>
   	<load-on-startup>1</load-on-startup>  
  </servlet>    
 
  <servlet>  
  	<servlet-name>servlet3</servlet-name>  
   	<servlet-class> com.javawithease.business.Servlet3</servlet-class>
   	<load-on-startup>-1</load-on-startup>  
  </servlet>  
 
  //other attributes
 
</web-app>
```

In the above example Servlet1 and Servlet2 will be loaded when server starts because positive value is passed in there load-on-startup. Servlet3 will be loaded at the time of first request because negative value is passed in there load-on-startup.




# RequestDispatcher interface

RequestDispacher is an interface that provides the facility to forward a request to another resource or include the content of another resource. RequestDispacher provides a way to call another resource from a servlet. Another resource can be servlet, jsp or html.

**Methods of RequestDispacher interface:**

1. forward(ServletRequest request, ServletResponse response)
2. include(SevletRequest request, ServletResponse response)

<dl>  
  <dt>forward(ServletRequest request,ServletResponse response):</dt>
  <dd>This method forwards a request from a servlet to another resource on the server.</dd>
</dl>

```java
// Syntax :
public void forward(ServletRequest request,ServletResponse response)throws ServletException, IOException
```

<dl>  
  <dt>include(SevletRequest request, ServletResponse response):</dt>
  <dd>This method includes the content of a resource in the response.</dd>
</dl>

```java
// Syntax :
public void include(ServletRequest request,ServletResponse response)throws ServletException, IOException
```

**How to get an object of RequestDispacher.**

RequestDispacher object can be gets from HttpServletRequest object. ServletRequest’s getRequestDispatcher() method is used to get RequestDispatcher object.

```java
RequestDispatcher requestDispatcher = request.getRequestDispatcher(“/another resource”);
```

After creating RequestDispatcher object you call forword or include method as per your requirement.

```java
requestDispatcher.forward(request, response);
or
requestDispatcher.include(request, response);
```

**Example:**

```java

// LoginServlet.java

package servlets;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class LoginServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		// get parameters from request object.
		String userName = request.getParameter("userName").trim();
		String password = request.getParameter("password").trim();

		// check for null and empty values.
		if (userName == null || userName.equals("") || password == null || password.equals("")) {
			out.print("Please enter both username" + " and password. <br/><br/>");
			RequestDispatcher requestDispatcher = request.getRequestDispatcher("/login.html");
			requestDispatcher.include(request, response);
		} // Check for valid username and password.
		else if (userName.equals("testLogin") && password.equals("servlet")) {
			RequestDispatcher requestDispatcher = request.getRequestDispatcher("WelcomeServlet");
			requestDispatcher.forward(request, response);
		} else {
			out.print("Wrong username or password. <br/><br/>");
			RequestDispatcher requestDispatcher = request.getRequestDispatcher("/login.html");
			requestDispatcher.include(request, response);
		}
	}
	
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		RequestDispatcher requestDispatcher = request.getRequestDispatcher("/login.html");
		requestDispatcher.include(request, response);
	}
}

```


```java

// WelcomeServlet.java

package servlets;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class WelcomeServlet extends HttpServlet {

	private static final long serialVersionUID = 1L;

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		out.println("<html><body>");
		out.println("<h1>You are logged " + "in successfully.</h1>");
		out.println("</html></body>");
	}

}
```

```java

// login.html

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 
Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
<title>Login</title>
</head>
<body>
	<form action="LoginServlet" method="post">
		Username:<input type="text" name="userName" /> <br />
		<br /> Password:<input type="password" name="password" /> <br />
		<br /> <input type="submit" value="login" />
	</form>
</body>
</html>
```

```java

// web.xml

<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.4" xmlns="http://java.sun.com/xml/ns/j2ee"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee
http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd">

	<welcome-file-list>
		<welcome-file>login.html</welcome-file>
	</welcome-file-list>

	<servlet>
		<servlet-name>LoginServlet</servlet-name>
		<servlet-class>servlets.LoginServlet</servlet-class>
	</servlet>

	<servlet-mapping>
		<servlet-name>LoginServlet</servlet-name>
		<url-pattern>/LoginServlet</url-pattern>
	</servlet-mapping>


	<servlet-mapping>
		<servlet-name>LoginServlet</servlet-name>
		<url-pattern></url-pattern>
	</servlet-mapping>

	<servlet>
		<servlet-name>WelcomeServlet</servlet-name>
		<servlet-class>servlets.WelcomeServlet</servlet-class>
	</servlet>

	<servlet-mapping>
		<servlet-name>WelcomeServlet</servlet-name>
		<url-pattern>/WelcomeServlet</url-pattern>
	</servlet-mapping>

</web-app>
```


# sendRedirect in servlet

sendRedirect() is the method of HttpServletResponse interface which is used to redirect response to another resource.

```java
response.sendRedirect(relative url);
```

| sendRedirect        | RequestDispatcher|
| ------------- |-------------|
| 1. Creates a new request from the client browser for the resource.      | 1. No new request is created.|
| 2. Accept relative url so control can go inside or outside the server.    | 2. Not accept relative url so can go only inside the server. |
| 3. New url can be seen in browser. | 3. New url can’t be seen in browser. |
| 4. Work on response object. | 4. Work on request object.|



### Example

```java

// LoginServlet.java

package servlets;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class LoginServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		// get parameters from request object.
		String userName = request.getParameter("userName").trim();
		String password = request.getParameter("password").trim();

		// check for null and empty values.
		if (userName == null || userName.equals("") || password == null || password.equals("")) {
			out.print("Please enter both username" + " and password. <br/><br/>");
			RequestDispatcher requestDispatcher = request.getRequestDispatcher("/login.html");
			requestDispatcher.include(request, response);
		} // Check for valid username and password.
		else if (userName.equals("testLogin") && password.equals("servlet")) {
			response.sendRedirect("/AdvJavaa/welcome.html");
		} else {
			out.print("Wrong username or password. <br/><br/>");
			RequestDispatcher requestDispatcher = request.getRequestDispatcher("/login.html");
			requestDispatcher.include(request, response);
		}
	}
	
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		RequestDispatcher requestDispatcher = request.getRequestDispatcher("/login.html");
		requestDispatcher.include(request, response);
	}
}

```


# Servlet Init parameters and ServletConfig interface

**Init parameters:**
Init parameters refers to the initialization parameters of a servlet or filter. <init-param> attribute is used to define a init parameter. <init-param> attribute has two main sub attributes <param-name> and <param-value>. The <param-name> contains the name of the parameter and <param-value> contains the value of the parameter.

## ServletConfig interface:
ServletConfig interface is used to access the init parameters.

**Methods of ServletConfig interface:**
1. getInitParameter(String name)
2. getInitParameterNames()
3. getServletContext()
4. getServletName()


<dl>  
  <dt>getInitParameter(String name):</dt>
  <dd>Returns the value of the specified parameter if parameter exist otherwise return null.</dd>
</dl>

```java
// Syntax :
public String getInitParameter(String name)
```

<dl>  
  <dt>getInitParameterNames():</dt>
  <dd>Returns the names of init parameters as Enumeration if servlet has init parameters otherwise returns an empty Enumeration.</dd>
</dl>

```java
// Syntax :
public Enumeration getInitParameterNames()
```

<dl>  
  <dt>getServletContext():</dt>
  <dd>Returns an instance of ServletContext.</dd>
</dl>

```java
// Syntax :
public ServletContext getServletContext()
```

<dl>  
  <dt>getServletName():</dt>
  <dd>Returns the name of the servlet.</dd>
</dl>

```java
// Syntax :
public String getServletName()
```

## Example

```java

// InitParamExample.java

package servlets;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class InitParamExample extends HttpServlet {
	private static final long serialVersionUID = 1L;

	// no-argument constructor
	public InitParamExample() {

	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();
		// get ServletConfig object.
		ServletConfig config = getServletConfig();
		// get init parameter from ServletConfig object.
		String appUser = config.getInitParameter("appUser");

		out.print("<h1>Application User: " + appUser + "</h1>");

		out.close();
	}
}

```

```java

// web.xml

	<servlet>
		<servlet-name>InitParamExample</servlet-name>
		<servlet-class>servlets.InitParamExample</servlet-class>
		<init-param>
			<param-name>appUser</param-name>
			<param-value>Jagata</param-value>
		</init-param>
	</servlet>

	<servlet-mapping>
		<servlet-name>InitParamExample</servlet-name>
		<url-pattern>/InitParamExample</url-pattern>
	</servlet-mapping>

```


# Servlet context parameters and ServletContext interface

**Context parameters:**
Context parameters refers to the initialization parameters for all servlets of an application. <context-param> attribute is used to define a context parameter. <context-param> attribute has two main sub attributes <param-name> and <param-value>. The <param-name> contains the name of the parameter and <param-value> contains the value of the parameter.

## ServletContext interface:

ServletContext interface is used to access the context parameters.

**Commonly used methods of ServletContext interface:**
1. getInitParameter(String name)
2. getInitParameterNames()
3. setAttribute(String name,Object object)
4. getAttribute(String name)
5. removeAttribute(String name)

<dl>  
  <dt>getInitParameter(String name):</dt>
  <dd>Returns the value of the specified parameter if parameter exist otherwise return null.</dd>
</dl>

```java
// Syntax :
public String getInitParameter(String name)
```

<dl>  
  <dt>getInitParameterNames():</dt>
  <dd>Returns the names of init parameters as Enumeration if servlet has init parameters otherwise returns an empty Enumeration.</dd>
</dl>

```java
// Syntax :
public Enumeration getInitParameterNames()
```

<dl>  
  <dt>setAttribute(String name,Object object):</dt>
  <dd>Binds the specified object to the specified attribute name and put this attribute in application scope. </dd>
</dl>

```java
public void setAttribute(String name,Object object). 
```

<dl>  
  <dt>getAttribute(String name):</dt>
  <dd>Returns the specified attribute if exist otherwise returns null.</dd>
</dl>

```java
public Object getAttribute(String name)
```

<dl>  
  <dt>removeAttribute(String name):</dt>
  <dd>Removes the specified attribute.</dd>
</dl>

```java
public void removeAttribute(String name).
```

## Example

```java

// ContextParamExample.java

package servlets;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class ContextParamExample extends HttpServlet {
	private static final long serialVersionUID = 1L;

	// no-argument constructor.
	public ContextParamExample() {

	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();
		// get ServletContext object.
		ServletContext context = getServletContext();
		// get context parameter from ServletContext object.
		String appUser = context.getInitParameter("appUser");

		out.print("<h1>Application User: " + appUser + "</h1>");

		out.close();
	}

}

```

```java

// web.xml

	<servlet>
		<servlet-name>ContextParamExample</servlet-name>
		<servlet-class>servlets.ContextParamExample</servlet-class>
	</servlet>

	<context-param>
		<param-name>appUser</param-name>
		<param-value>SJAGATA</param-value>
	</context-param>

	<servlet-mapping>
		<servlet-name>ContextParamExample</servlet-name>
		<url-pattern>/ContextParamExample</url-pattern>
	</servlet-mapping>

```



# Servlet Hello World Example using annotation.

This servlet program is used to print "Hello World" on client browser using annotations.

```java

// ServletAnnotationExample.java

package servlets;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/servletAnnotationTest")
public class ServletAnnotationExample extends HttpServlet {

	private static final long serialVersionUID = 1L;

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		out.print("<h1>Hello World example using annotations.</h1>");

		out.close();
	}

}

```


# Session management and cookies in servlet

**Session:**

Session is a time interval devoted to an activity.

**Session Tracking:**

Session Tracking or session management is a way of maintaining the state of the user.

**Need of Session Tracking:**

As we discussed in earlier tutorials we are using HTTP for completing request response cycle. HTTP is a stateless protocol which means when a new request comes it can’t keep any record or state of previous request of the user. That’s why we need session tracking for maintaining the state of the user.

## Way of Session Tracking in servlet:

1. Cookie.
2. Hidden form field.
3. Url rewriting.
4. HttpSession.

## Cookie in servlet

A cookie is a small piece of information as a text file stored on client’s machine by a web application.

**How cookie works?**

As HTTP is a stateless protocol so there is no way to identify that it is a new user or previous user for every new request. In case of cookie a text file with small piece of information is added to the response of first request. They are stored on client’s machine. Now when a new request comes cookie is by default added with the request. With this information we can identify that it is a new user or a previous user.

**Types of cookies:**

1. Session cookies/Non-persistent cookies
2. Permanent cookies/Persistent cookies

**_Session cookies/Non-persistent cookies:_** These types of cookies are session dependent i.e. they are accessible as long as session is open and they are lost when session is closed by exiting from the web application.

**_2. Permanent cookies/Persistent cookies:_** These types of cookies are session independent i.e. they are not lost when session is closed by exiting from the web application. They are lost when they expire.

**Advantages of cookies:**
1. They are stored on client side so don’t need any server resource.
2. and easy technique for session management.

**Disadvantages of cookies:**
1. Cookies can be disabled from the browser.
2. Security risk is there because cookies exist as a text file so any one can open and read user’s information.

## Cookie Class:
Cookie class provides the methods and functionality for session management using cookies. Cookie class is in **_javax.servlet.http_**

```java
Package javax.servlet.http.Cookie.
```

**Commonly used constructor of Cookie class:**

1. Cookie(String name,String value)
Creates a cookie with specified name and value pair.

```java
public Cookie(String name,String value)
```


**Commonly used methods of cookie class:**

1. setMaxAge(int expiry):
Sets the maximum age of the cookie.

```java
public void setMaxAge(int expiry)
```

2. getMaxAge(): 
Returns the maximum age of the cookie. Default value is -1.

```java
public int getMaxAge()
```

3. setValue(String newValue): 
Change the value of the cookie with new value.

```java
public void setValue(String newValue)
```

4. getValue(): 
Returns the value of the cookie.

```java
public String getValue()
```

5. getName(): 
Returns the name of the cookie.

```java
public String getName()
```

## How to create cookie?

**_HttpServletResponse_** interface’s addCookie(Cookie ck) method is used to add a cookie in response object.

```java
//Syntax : public void addCookie(Cookie ck)

//create cookie object  
Cookie cookie=new Cookie(“cookieName”,”cookieValue”);

//add cookie object in the response

response.addCookie(cookie);

```

## How to get cookie?

**_HttpServletRequest_** interface’s getCookies() method is used to get the cookies from request object.

```java

// Syntax: public Cookie[] getCookies()

//get all cookie objects.
Cookie[] cookies = request.getCookies();

//iterate cookies array to get individual cookie objects.

for(Cookie cookie : cookies){

            out.println(“Cookie Name: ” + cookie.getName());

            out.println(“Cookie Value: ” + cookie.getValue());

}
```

## How to remove or delete cookies?

Cookies can be removed by setting its expiration time to 0 or -1. If expiration time set to 0 than cookie will be removed immediately. If expiration time set to -1 than cookie will be removed when browser closed.

```java

//Remove value from cookie
Cookie cookie = new Cookie(“cookieName”, “”);

//Set expiration time to 0.

cookie.setMaxAge(0);

//add cookie object in the response.

response.addCookie(cookie);

```

## Session management example using cookie:

```java

// CreateCookieServlet.java

package servlets.cookies;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class CreateCookieServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		// get parameters from request object.
		String userName = request.getParameter("userName").trim();
		String password = request.getParameter("password").trim();

		// check for null and empty values.
		if (userName == null || userName.equals("") || password == null || password.equals("")) {
			out.print("Please enter both username " + "and password. <br/><br/>");
			RequestDispatcher requestDispatcher = request.getRequestDispatcher("/login2.html");
			requestDispatcher.include(request, response);
		} // Check for valid username and password.
		else if (userName.equals("test") && password.equals("1234")) {
			// create cookie objects.
			Cookie cookie1 = new Cookie("userName", userName);
			Cookie cookie2 = new Cookie("password", password);
			// add cookie in the response object.
			response.addCookie(cookie1);
			response.addCookie(cookie2);
			out.print("<h3>Cookies are created. Click on the " + "below button to get cookies.");
			out.print("<form action='GetCookieServlet' method='GET'>");
			out.print("<input type='submit' value='Get Cookie'>");
			out.print("</form>");

			out.close();
		} else {
			out.print("Wrong username or password. <br/><br/>");
			RequestDispatcher requestDispatcher = request.getRequestDispatcher("/login2.html");
			requestDispatcher.include(request, response);
		}
	}

}
```

```java

// GetCookieServlet.java

package servlets.cookies;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class GetCookieServlet extends HttpServlet {

	private static final long serialVersionUID = 1L;

	@Override
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		super.doPost(request, response);

		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		try {
			Cookie cookies[] = request.getCookies();
			for (Cookie cookie : cookies) {
				out.println("Cookie Name: " + cookie.getName());
				out.println("Cookie Value: " + cookie.getValue());
				out.println("");
			}

			out.println("Click on the below button to delete cookies.");
			out.print("<form action='DeleteCookieServlet' method='GET'>");
			out.print("<input type='submit' value='Delete Cookies'>");
			out.print("</form>");
			out.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

}

```

```java

// DeleteCookieServlet.java

package servlets.cookies;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.ServletResponse;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class DeleteCookieServlet extends HttpServlet {

	private static final long serialVersionUID = 1L;

	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		super.doPost(req, resp);

		resp.setContentType("text/html");
		PrintWriter out = ((ServletResponse) req).getWriter();

		try {
			Cookie cookies[] = req.getCookies();
			out.print("Deleted cookie are:");
			for (Cookie cookie : cookies) {
				cookie.setMaxAge(0);
				out.println("Cookie name: " + cookie.getName());
			}

			out.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

}

```


## Hidden field in servlet

**Hidden field:**

Hidden field is an input text with hidden type. This field will not be visible to the user.

```html
<input name=”fieldName” value=”fieldValue” type=”hidden”/> 
```

**How to get hidden field value in servlet?**

HttpServletRequest interface’s getParameter() method is used to get hidden field value in servlet.

```java
String value = request.getParameter(“fieldName”);  
```

_Note: Hidden field only works in case of form submission so they will not work in case of anchor tag as no form submission is there._

**Advantages of hidden field:**
1.  All browsers support hidden fields.
2. Simple to use.

**Disadvantages of hidden fields:**
1.  Not secure.
2.  Only work in case of form submission.


## HttpSession in servlet

**HttpSession:**
HttpSession is an interface that provides a way to identify a user in multiple page requests. A unique session id is given to the user when first request comes. This id is stored in a request parameter or in a cookie.

**How to get session object?**
HttpServletRequest interface’s getSession() method is used to get the session object.

```java
HttpSession session = request.getSession();  
```

**How to set attribute in session object?**

HttpSession interface’s setAttribute() method is used to set attribute in session object.

```java
public void setAttribute(String name,Object value); // syntax

// example 
HttpSession session=request.getSession();  
session.setAttribute("userName",userName);  
session.setAttribute("password",password);
```

**How to get attribute from session object?**
HttpSession interface’s getAttribute() method is used to get attribute from session object.

```java
public Object getAttribute(String name); // syntax

//get parameters from session object.
HttpSession session=request.getSession(false);  
String userName =(String)session.getAttribute("userName");  
String password =(String)session.getAttribute("password");  
```



# Servlet filter in java

**Servlet filter:**
Servlet filters are the objects which are used to perform some filtering task. A filter can be applied to a servlet, jsp or html.

**Servlet filters are mainly used for following tasks:**
1. **Pre-processing:** Servlet filter is used for pre-processing of request before it accesses any resource at server side.
2. **Post-processing:** Servlet filter is used for post-processing of response before it sent back to client.

**How to create a filter?**
Implement **_javax.servlet.Filter_** interface to create a filter.


## Filter interface:

To create a filter you have to implement filter interface. Filter interface is in javax.servlet package javax.servlet.Filter. It provides life cycle methods of a filter.


**Methods of filter interface:**

1. **init(FilterConfig config):** This method is used to initialize the filter. It is called only once by web container.

```java
public void init(FilterConfig config)
```

2. **doFilter(HttpServletRequest request,HttpServletResponse response, FilterChain chain):** This method is used for performing pre-processing and post-processing tasks. It is called every time for a request/response comes for a resource to which filter is mapped.

```java
public void doFilter(HttpServletRequest request,HttpServletResponse response, FilterChain chain)
```

3. **destroy():** This method is called only once by the web container when filter is taken out of the service.

```java
public void destroy()
```

## FilterChain interface:

FilterChain object is used to call the next filter or a resource if it is the last filter in filter chaining.

**Method of FilterChain interface:**

1. **doFilter(HttpServletRequest request, HttpServletResponse response):** This method is used to call the next filter in filter chaining.

```java
public void doFilter(HttpServletRequest request, HttpServletResponse response) throws IOException, ServletException
```

**How to define a filter in web.xml?**
<filter> attribute is used to define a filter in web.xml.

```java
<web-app>
	//Other attributes.

	<filter>
		<filter-name>filterName</filter-name>
		<filter-class>filterClass</filter-class>
	</filter>

	<filter-mapping>
		<filter-name>filterName</filter-name>
		<url-pattern>urlPattern</url-pattern>
	</filter-mapping>

	//Other attributes.

</web-app>
```

## Example

```java

// LoginFilter.java

package servlets.httpSession;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

public class LoginServlet extends HttpServlet {

	private static final long serialVersionUID = 1L;

	@Override
	protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		super.doPost(req, resp);

		resp.setContentType("text/html");
		PrintWriter out = resp.getWriter();

		// get parameters from request object.
		String userName = req.getParameter("userName").trim();
		String password = req.getParameter("password").trim();

		// check for null and empty values.
		if (userName == null || userName.equals("") || password == null || password.equals("")) {
			out.print("Please enter both username " + "and password. <br/><br/>");
			RequestDispatcher requestDispatcher = req.getRequestDispatcher("/login.html");
			requestDispatcher.include(req, resp);
		} // Check for valid username and password.
		else if (userName.equals("jai") && password.equals("1234")) {
			HttpSession session = req.getSession();
			session.setAttribute("userName", userName);
			session.setAttribute("password", password);
			out.println("Logged in successfully.<br/>");
			out.println("Click on the below link to see " + "the values of Username and Password.<br/>");
			out.println("<a href='DisplaySessionValueServlet'>" + "Click here</a>");
			out.close();
		} else {
			out.print("Wrong username or password. <br/><br/>");
			RequestDispatcher requestDispatcher = req.getRequestDispatcher("/login.html");
			requestDispatcher.include(req, resp);
		}

	}

}

```

```java

	<filter>
		<filter-name>LoginFilter</filter-name>
		<filter-class>servlets.filters.LoginFilter</filter-class>
	</filter>

	<filter-mapping>
		<filter-name>LoginFilter</filter-name>
		<url-pattern>/WelcomeFilterServlet</url-pattern>
	</filter-mapping>
```


# FilterConfig interface

FilterConfig object is created and used by web container to pass init parameters to a filter during initialization.

**Methods of FilterConfig interface:**

1. **getFilterName():** Returns the name of the filter defined in web.xml.

```java
public String getFilterName() 
```

2. **getInitParameter(String name): Returns the value of the specified parameter.

```java
public String getInitParameter(String name) 
```

3. **getInitParameterNames():** Returns the names of all parameters as Enumeration.

```java
public Enumeration getInitParameterNames() 
```

4. **getServletContext():** Returns the object of ServletContext.

```java
public ServletContext getServletContext()
```

## Example

```java

// MyFilter.java

package servlets.filters;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;

public class MyFilter implements Filter {

	private FilterConfig filterConfig;

	@Override
	public void destroy() {
	}

	@Override
	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
			throws IOException, ServletException {
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		// get parameters from filterConfig object.
		String appUser = filterConfig.getInitParameter("appUser");
		if (appUser.equals("jai")) {
			chain.doFilter(request, response);
		} else {
			out.print("Invalid application user.");
		}
	}

	@Override
	public void init(FilterConfig filterConfig) throws ServletException {
		this.filterConfig = filterConfig;
	}

}

```

```java

// web.xml

	<filter>
		<filter-name>MyFilter</filter-name>
		<filter-class>servlets.filters.MyFilter</filter-class>
		<init-param>
			<param-name>appUser</param-name>
			<param-value>SJ</param-value>
		</init-param>
	</filter>

	<filter-mapping>
		<filter-name>MyFilter</filter-name>
		<url-pattern>/MyFilter</url-pattern>
	</filter-mapping>

```






















**P.S :**

### serialVersionUID

The serialization runtime associates with each serializable class a version number, called a serialVersionUID, which is used during deserialization to verify that the sender and receiver of a serialized object have loaded classes for that object that are compatible with respect to serialization. If the receiver has loaded a class for the object that has a different serialVersionUID than that of the corresponding sender's class, then deserialization will result in an  InvalidClassException. A serializable class can declare its own serialVersionUID explicitly by declaring a field named "serialVersionUID" that must be static, final, and of type long:

```java
ANY-ACCESS-MODIFIER static final long serialVersionUID = 42L;
```

if you don't explicitly specify serialVersionUID, a value is generated automatically - but that's brittle because it's compiler implementation dependent.


