# Servlets Interview Questions and Answers

### What is a Web application?

A web application or website is an application program which accessed over a network connection using HTTP and often runs inside a web browser.

### What is a Web browser?

A web browser is a program which is act as an interface between user and web application e.g. Internet Explorer, Chrome, Safari, Mozilla firefox etc.

### What is different between web server and application server?

A web server is used to handler HTTP requests from client browsers and respond with HTML response. A web server understands HTTP language and runs on HTTP protocol.
Apache Web Server is kind of a web server and then we have specific containers that can execute servlets and JSPs known as servlet container, for example Tomcat.

Application Servers provide additional features such as Enterprise JavaBeans support (EJB), JMS Messaging support, Transaction Management etc. i.e. Application server is a web server with additional functionalities to help developers with enterprise applications.

### What is a servlet container?

A Servlet container also known as Web container is the component of a web server that interacts with Java servlets. A web container is responsible for managing the lifecycle of servlets, mapping a URL to a particular servlet and ensuring that the URL requester has the correct access rights.

### What is MIME Type?

MIME stands for “Multipurpose Internet Mail Extensions. It is a standard way of classifying file types on the Internet. i.e. “Content-type” header value defined in a HTTP response. Commonly used mime types are text/html, text/xml, application/xml etc.

### What is a Servlet?

**Servlet as technology:**

As a technology servlet provides a model of communication between a web user request and the application or program on the web server.

**Servlet as component:**

As a component servlet is a program which is executed in web server and responsible for dynamic content generation
See more at: Servlet Overview

### What are the advantages of servlets over CGI?

1. CGI is process based. For every request a new process will be started. Servlet is thread based. For every request a new thread will be started.
2. CGI is Platform dependent. Servlet is Platform independent.
3. Response time is high in case of CGI. Response time is low in case of servlets.
See more at: Servlet Overview

### Explain servlet life cycle.

Life cycle of a servlet is managed by web container.
Servlet life cycle steps:
1.	Load Servlet Class.
2. Create Servlet instance.
3. Call init() method.
4. Call service() method.
5. Call destoy() method.
See more at: Servlet Life Cycle

### What are the life-cycle methods for a servlet?

1. **Call init() method:** After creating the servlet instance web container calls the servlet’s init method. This method is used to initialize the servlet before processing first request. It is called only once by the web container.
2. **Call service() method:** After initialization process web container calls service method. Service method is called for every request. For every request servlet creates a separate thread.
3. **Call destoy() method:** This method is called by web container before removing the servlet instance. Destroy method asks servlet to releases all the resources associated with it. It is called only once by the web container when all threads of the servlet have exited or in a timeout case.
See more at: Servlet Life Cycle

### Why do we need a constructor in a servlet if we use the init method?

As discussed init method in a servlet is used to initialize it but servlet container uses constructor to create an instance of the servlet. The init method will be called after servlet instance creation.

### When servlet object is created?

Web container creates the servlet object when the first request is received.

### Who is responsible for creating the servlet object?

The web container or servlet container is responsible for creating the servlet object.

### What is Servlet interface?

Servlet interface contains the common methods for all servlets i.e. provides the common behaviour for all servlets.
public interface Servlet
Servlet interface is in javax.servlet package (javax.servlet.Servlet).
See more at: Servlet interface .

### What is GenericServlet class?

GenericServlet class implements the Servlet and ServletConfig interfaces. GenericServlet is protocol-independent. It not provides the implementation of service method.
public abstract class GenericServlet implements Servlet, ServletConfig
GenericServlet class is in javax.servlet package (javax.servlet.GenericServlet).
See more at: GenericServlet Class.

### What is HttpServlet class?

HttpServlet class extends the GenericServlet. It is protocol-dependent.
public abstract class HttpServlet extends GenericServlet
HttpServlet class is in javax.servlet.http package (javax.servlet.http.HttpServlet).
See more at: HttpServlet class .

### What is the difference between HttpServlet and GenericServlet in Servlet API?

GenericServlet provides framework to create a Servlet for any protocol e.g. you can write Servlet to receive content from FTP, SMTP etc, while HttpServlet is built-in Servlet provided by Java for handling HTTP requests.

### What is HTTPServletRequest class?

When a browser requests for a web page, it sends lot of information to the web server which cannot be read directly because this information travel as a part of header of HTTP request. HTTPServletRequest represents this HTTP Request.

### What is HTTPServletResponse class?

When a Web server responds to a HTTP request to the browser, the response typically consists of a status line, some response headers, a blank line, and the document. HTTPServletResponse represents this HTTP Response.

### How can we create deadlock condition on our servlet?

We can create deadlock in servlet by calling doPost() method inside doGet() and doGet()method inside doPost() method.

### For initializing a servlet can we use a constructor in place of init()?

No, because we need an object of servletConfig at the time of servlet initialization which is used to get the all the parameter defined in deployment descriptor. In older version of java servlet class have only default constructor, so we cannot pass a parameter to constructor.

### What is ServletConfig object?

ServletConfig interface is used to access the init parameters. Init parameters refers to the initialization parameters of a servlet or filter. See more at: ServletConfig Interface .

### What is ServletContext object?

ServletContext interface is used to access the context parameters. Context parameters refers to the initialization parameters for all servlets of an application. See more at: ServletContext Interface .

### How to read form data in servlet?

Servlets handles form data parsing by the following methods depending on the situation:
* **getParameter():** This method is used to get the value of a form parameter.
* **getParameterValues():** This method is used to get the values of a parameter which appears more than once and returns multiple values, for example checkbox.
* **getParameterNames():** This method is used to get complete list of all parameters in the current request.

### How to write html contents using servlets?

Get the object of PrintWriter using request and print html.

```java
PrintWriter out = response.getWriter();
out.println("Hello World");
```

### How to send an authentication error from a servlet?

The setStatus(statuscode) method of HttpServletResponse to send an authentication error.

```java
// Set error code and reason.
response.sendError(407, "Need authentication!" );
```

### What is servlet collaboration?

Servlet collaboration is a way communication between two servlets. Servlet collaboration can be achieved by 3 ways.
1. RequestDispatchers include () and forward() method .
2. Using sendRedirect()method of Response object.
3. Using servlet Context methods

### What is lazy loading?

As we discussed servlets are initialized by the container at the time of first request for the servlet. This is called lazy loading.

### How do we call one servlet from another servlet?

The forward() method of RequestDispatcher is used to forward the request to a resource in same application. The sendRedirect() method of ServletResponse is used to forward the request to a resource in another application.

### What is the difference between sendRedirect and RequestDispatcher?

| sendRedirect        | RequestDispatcher|
| ------------- |-------------|
| 1. Creates a new request from the client browser for the resource.      | 1. No new request is created.|
| 2. Accept relative url so control can go inside or outside the server.    | 2. Not accept relative url so can go only inside the server. |
| 3. New url can be seen in browser. | 3. New url can’t be seen in browser. |
| 4. Work on response object. | 4. Work on request object.|

### Can we call a jsp from the servlet?

Yes, we can call a jsp from the servlet using RequestDispatcher interface for example:

```java
RequestDispatcher rd=request.getRequestDispatcher("/login.jsp");  
rd.forward(request,response);
```

### What are servlets filters?

Servlet filters are the objects which are used to perform some filtering task. A filter can be applied to a servlet, jsp or html.
See more at: Servlet filter.

### What are the life-cycle methods for a servlet filter?

1. init(FilterConfig config): This method is used to initialize the filter. It is called only once by web container.

```java
public void init(FilterConfig config)
```

2. doFilter(HttpServletRequest request,HttpServletResponse response, FilterChain chain): This method is used for performing pre-processing and post-processing tasks. It is called every time for a request/response comes for a resource to which filter is mapped.

```java
public void doFilter(HttpServletRequest request,HttpServletResponse response, FilterChain chain)
```

3. destroy(): This method is called only once by the web container when filter is taken out of the service.

```java
public void destroy()
```

See more at: Servlet filter.

### Can multiple filters be configured?

Yes.

### Can filtering be done in an ordered way? If so then how to achieve it?

Yes. The order of filter-mapping elements in web.xml determines the order in which the web container applies the filter to the servlet. To reverse the order of the filter, we just need to reverse the filter-mapping elements in the web.xml file.

### How to configure a central error handling page in servlets?

We have to use the error-page element in web.xml to specify the invocation of servlets in response to certain exceptions or HTTP status codes.
How to configure a central error handler in servlets?
If we want to have a generic Error Handler for all the exceptions then we should define following error-page instead of defining separate error-page elements for every exception:

```java
<error-page>
   <exception-type>java.lang.Throwable</exception-type >
   <location>/ErrorHandler</location>
</error-page>
```

### What are cookies?

A cookie is a small piece of information as a text file stored on client’s machine by a web application.
See more at: Cookie in servlet.

### How to create a cookie using servlet?

HttpServletResponse interface’s addCookie(Cookie ck) method is used to add a cookie in response object.
Syntax: public void addCookie(Cookie ck)
See more at: Cookie in servlet.

### How to read a cookie using servlet?

HttpServletRequest interface’s getCookies() method is used to get the cookies from request object.
Syntax: public Cookie[] getCookies()
See more at: Cookie in servlet.

### How to delete a cookie using servlet?

Cookies can be removed by setting its expiration time to 0 or -1. If expiration time set to 0 than cookie will be removed immediately. If expiration time set to -1 than cookie will be removed when browser closed.
See more at: Cookie in servlet.

### What is URL rewriting?

URL rewriting is a way of appending data at the end of URL. Data is appended in name value pair form. Multiple parameters can be appended in one URL with name value pairs.

```html
 URL?paramName1=paramValue1& paramName2=paramValue2
```

See more at: URL rewriting in servlet.

### What is session?

HttpSession is an interface that provides a way to identify a user in multiple page requests. A unique session id is given to the user when first request comes. This id is stored in a request parameter or in a cookie.
See more at: HttpSession in servlet.

### How to get session object?

HttpServletRequest interface’s getSession() method is used to get the session object.

```java
HttpSession session = request.getSession();
```

See more at: HttpSession in servlet.

### How to set attribute in session object?

HttpSession interface’s setAttribute() method is used to set attribute in session object.
Syntax: public void setAttribute(String name,Object value);

```java
session.setAttribute(“attName”, “attValue”);
```

See more at: HttpSession in servlet.

### How to get attribute from session object?

HttpSession interface’s getAttribute() method is used to get attribute from session object.
Syntax: public Object getAttribute(String name);

```java
String value = (String) session.getAttribute(“attName”);
```

See more at: HttpSession in servlet.
