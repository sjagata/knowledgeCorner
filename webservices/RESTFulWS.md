### [REST Web Services](http://docs.oracle.com/javaee/6/tutorial/doc/gijqy.html)

In the REST architectural style, data and functionality are considered resources and are accessed using **Uniform Resource Identifiers (URIs)**, typically links on the Web. The resources are acted upon by using a set of simple, well-defined operations. The REST architectural style constrains an architecture to a client/server architecture and is designed to use a stateless communication protocol, typically HTTP. In the REST architecture style, clients and servers exchange representations of resources by using a standardized interface and protocol.

The following principles encourage RESTful applications to be simple, lightweight, and fast:

* **Resource identification through URI:** A RESTful web service exposes a set of resources that identify the targets of the interaction with its clients. Resources are identified by URIs, which provide a global addressing space for resource and service discovery. See [The @Path Annotation and URI Path Templates](http://docs.oracle.com/javaee/6/tutorial/doc/gilik.html#ginpw) for more information.

* **Uniform interface:** Resources are manipulated using a fixed set of four create, read, update, delete operations: PUT, GET, POST, and DELETE. PUT creates a new resource, which can be then deleted by using DELETE. GET retrieves the current state of a resource in some representation. POST transfers a new state onto a resource. See [Responding to HTTP Methods and Requests](http://docs.oracle.com/javaee/6/tutorial/doc/gilik.html#gipys) for more information.

* **Self-descriptive messages:** Resources are decoupled from their representation so that their content can be accessed in a variety of formats, such as HTML, XML, plain text, PDF, JPEG, JSON, and others. Metadata about the resource is available and used, for example, to control caching, detect transmission errors, negotiate the appropriate representation format, and perform authentication or access control. See [Responding to HTTP Methods and Requests](http://docs.oracle.com/javaee/6/tutorial/doc/gilik.html#gipys) and [Using Entity Providers to Map HTTP Response and Request Entity Bodies](http://docs.oracle.com/javaee/6/tutorial/doc/gilik.html#gipze) for more information.

* **Stateful interactions through hyperlinks:** Every interaction with a resource is stateless; that is, request messages are self-contained. Stateful interactions are based on the concept of explicit state transfer. Several techniques exist to exchange state, such as URI rewriting, cookies, and hidden form fields. State can be embedded in response messages to point to valid future states of the interaction. See [Using Entity Providers to Map HTTP Response and Request Entity Bodies](http://docs.oracle.com/javaee/6/tutorial/doc/gilik.html#gipze) and “Building URIs” in the JAX-RS Overview document for more information.

**Uniform Interface and Easy Access:**

HTTP Methods:
* POST
* GET
* PUT
* DELETE


### PUT vs POST
Both PUT and POST can be used for creating.

You have to ask "what are you performing the action to?" to distinguish what you should be using. Let's assume you're designing an API for asking questions. If you want to use POST then you would do that to a list of questions. If you want to use PUT then you would do that to a particular question.

#### Great both can be used, so which one should I use in my RESTful design:
You do not need to support both PUT and POST.

Which is used is left up to you. But just remember to use the right one depending on what object you are referencing in the request.

Some considerations:

* Do you name your URL objects you create explicitly, or let the server decide? If you name them then use PUT. If you let the server decide then use POST.
* PUT is idempotent, so if you PUT an object twice, it has no effect. This is a nice property, so I would use PUT when possible.
* You can update or create a resource with PUT with the same object URL
* With POST you can have 2 requests coming in at the same time making modifications to a URL, and they may update different parts of the object.


> POST:
Used to modify and update a resource
```html
POST /questions/<existing_question> HTTP/1.1
Host: www.example.com/
```
Note that the following is an error:
```html
POST /questions/<new_question> HTTP/1.1
Host: www.example.com/
```
**If the URL is not yet created, you should not be using POST to create it while specifying the name.** This should result in a 'resource not found' error because <new_question> does not exist yet. You should PUT the <new_question> resource on the server first.

You could though do something like this to create a resources using POST:
```html
POST /questions HTTP/1.1
Host: www.example.com/
```
Note that in this case the resource name is not specified, the new objects URL path would be returned to you.

> PUT:
Used to create a resource, or overwrite it. While you specify the resources new URL.

For a new resource:
```js
PUT /questions/<new_question> HTTP/1.1
Host: www.example.com/
```
To overwrite an existing resource:
```js
PUT /questions/<existing_question> HTTP/1.1
Host: www.example.com/
```


**URI : /patients**
Example:
To create patients we use a POST request with URL like `/patients` <br>
POST /patients <br>

```xml
<patient>
  <name>John</name>
</patient>
```
  
 Once it create the patient in DB it sends 200 OK message with id `<id>1</id>`
 
 GET /patients/123 <br>
 will return 200 OK and entire patient information
 
 PUT /patients - to update <br>
 
 DELETE /patients/123 - to delete
 
 
 #### Advantages
 
* Single Interface - GET, POST, PUT, DELETE
* Easy to access
   * http://www.hospital.com/patients - for all patients
   * /patients/{id} - to get patient info
   * /prescriptions - to get prescriptions
   * /prescriptions/{id} - to get patients prescriptions
* Interoperable & Multiple Formats
   * `REST Client(HTML/JS)` --- `JSON` ---> `REST Provider(JAVA)`
   * `REST Client(.NET)` --- `XML` ---> `REST Provider(JAVA)`
   * `REST Client(Python)` --- `CSV` ---> `REST Provider(JAVA)`
* Stateless
   * Client server apps
   * State is maintained client side instead of server side
* Scalability
* HTTP requests can be easily cached, because they are idempotent. No matter how many times you run your GET, PUT and DELETE methods they don't impact the state of the application.

#### When ?
* Well defined contract exisits. 
* Multiple Data Formats where as SOAP supports XML
* Bandwidth and Memory
* Stateless applications
* Caching (GET - idempotent)
* Existing logic can be exposed easily


### [JAX-RS](http://docs.oracle.com/javaee/6/tutorial/doc/gilik.html)
JAX-RS is a Java programming language API designed to make it easy to develop applications that use the REST architecture.

The JAX-RS API uses Java programming language annotations to simplify the development of RESTful web services. Developers decorate Java programming language class files with JAX-RS annotations to define resources and the actions that can be performed on those resources. JAX-RS annotations are runtime annotations; therefore, runtime reflection will generate the helper classes and artifacts for the resource. A Java EE application archive containing JAX-RS resource classes will have the resources configured, the helper classes and artifacts generated, and the resource exposed to clients by deploying the archive to a Java EE server.
  

 **JAX-RS** provides :
* Specification - Apache CXF, Jersey
* API - for developers(Set of annonatations)

**import javax.ws.rs.**
1. **@Path("users/{username}")** : allows us to mark our Java classes and methods with a relative URI path.
2. **HTTP Methods**
   * @GET
   * @POST
   * @PUT
   * @DELETE
3. **Data Formats**
   * **@Consumes("text/plain)** - tells what kind of data this particular REST provider can accept
   * **@Produces({"application/json", "application/xml"})** - tells what kind od data REST provider can produce or send back to the client
4. **Parameter Calues:**
   * **@ParhParam** 
   * **@QueryParam** - to map the request query parameters in a GET method to a Java Object automatically.
   * **@FormParam** - map form submission
5. **Exception Mappers:**
   * **@Provider**
 
 <br>
 <br>
 
 ### HTTP Status Codes:
 * Success : 200 to 399
    * Ex : 200 OK
 * Failure : 400 to 599
    * EX : 404 Not Found
    
 #### Two Type
 * Standard Error
 * Application Errors


<br>
<br>

 ### javax.ws.rs.client.*
 
 * ClientBuilder
 * Client
 * WebTarget
 * Entity
 * Invoke.Builder
 
 <br>
 <br>
 
 ### JAX-RS Injection
 * @PathParam
 * @QueryParam
 * @FormParam
 * @HeaderParam
 * @CookieParam
 
 <br>
 <br>
 
 ### Async
 
 `Asynchronous` - JAX-RS - `Provider/Server` <br>
 
 `Asynchronous` - JAX-RS - `Client API` - `Polling` <br>
 `Asynchronous` - JAX-RS - `Client API` - `CallBAck`
 
 **Provider**
 * @javax.ws.rs.container.Suspended
 * javax.ws.rs.container.AsyncResponse
 
 **Client**
 * javax.ws.rs.client.AsyncInvoker
 * java.util.concurrent.Future
 * javax.ws.rs.client.InvocationCallback
 
 
 #### Furture vs Callback
 * If we need the control on the various web services client calls that we are making (If we all the data before doing something else) then Future else Callback 
 
 <br>
 <br>
 
 
### [Spring security](https://docs.spring.io/spring-security/site/docs/5.0.0.M3/reference/htmlsingle/)
 
Spring Security is a framework that focuses on providing both authentication and authorization to Java applications. Like all Spring projects, the real power of Spring Security is found in how easily it can be extended to meet custom requirements

Features

* Comprehensive and extensible support for both Authentication and Authorization
* Protection against attacks like session fixation, clickjacking, cross site request forgery, etc
* Servlet API integration
* Optional integration with Spring Web MVC
* Much more…
 
 It provides both authentication and authorization to Java applications at **URL level**, **Method level** and the **Object level**
 
 #### 4 steps:
 1. **pom.xml**
    * spring-security-core
    * spring-security-config
    * spring-security-web
 2. Add the Filter - **DelegatingFilterProxy**
    * to web.xml
 3. **SpringConfiguration.xml**
    * `<global-method-security/>` - enables the security annotations
    * `<http/>` - to configure what kind of security we want, 
       * form based security 
       * form based authentication
       * basic authentication etc..
    * `<AuthenticationManager/>` - to define users and rules 
 4. **@Security("ROLE_NAME")**
 
 ```xml
// web.xml
<filter>
	<filter-name>springSecurityFilterChain</filter-name>
	<filter-class>org.springframework.web.filter.DelegatingFilterProxy
	</filter-class>
</filter>
<filter-mapping>
	<filter-name>springSecurityFilterChain</filter-name>
	<url-pattern>/*</url-pattern>
</filter-mapping>
```
 
 ```xml
 //security.xml
<security:global-method-security
	secured-annotations="enabled" />

<security:http>
	<security:http-basic />
</security:http>

<security:authentication-manager>
	<security:authentication-provider>
		<security:user-service>
			<security:user name="customer" password="customer"
				authorities="ROLE_CUSTOMER" />
			<security:user name="admin" password="admin"
				authorities="ROLE_CUSTOMER,ROLE_ADMIN" />
		</security:user-service>
	</security:authentication-provider>
</security:authentication-manager>
  ```
 
 ```java
 //Java code
 public interface ProductService {

	@Secured("ROLE_CUSTOMER")
	@GET
	@Path("/products")
	List<Product> getProducts();

	@Secured("ROLE_ADMIN")
	@POST
	@Path("/products")
	int addProduct(Product product);
}
```
 
 <br>
 <br>
 
 ### OAuth
 
 When we access a secured web application, it first verifies our identity by logging us in and then it ensures that we have access only to that data or functionality in the application which we are authorized for.
 * So the basic requirements are identity and permissions or authentication and authorization.
 * REST applications are lightweight applications and are no exception to this kind of access.
 * OAuth is a authentication and authorization standard which allows an application to gain access to user's data within an other application without knowing the user's user ID and password for the second application. 
 
 Example: 
 
 * Below is called "Federated authentication"
 
 ![Alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/webservices/images/OAuth.png "OAuth")
 
 
 * Delegated Authorization
 
 ![Alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/webservices/images/DelegatedAuth.png "DelegatedAuth")
 
 
 #### Why OAuth?
 
 ![Alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/webservices/images/whyOAuth.png "whyOAuth")
 
 
 #### When OAuth?
 
 ![Alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/webservices/images/whenOAuth.png "whenOAuth")
 
 #### OAuth workflow
 1. JavaWorld registers with Google and gets a client ID
 2. Java world redirects
    * Ex : http://googleapis.com/oauth?client_id=javaworld&state=123456789&redirect_uri=http%3A%2F%2Fjavaworld.com
 3. User Logs In
 4. Google Authenticates and redirects
    * http://javaworld.com/state=12345678&code=000222
 5. Java world ---> code=000222 ---> Google
 6. JavaWorld <--- Token=2basd23445345sdfsdfsdf23423423412qwe ---> Google.
 
 
![Alt text](https://developers.google.com/accounts/images/webflow.png "OAuth")
 
 
 #### Roles
 
![Alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/webservices/images/roles.png "roles")

* Variation in implementation
* [OAuth Support](https://oauth.net/code/)
* [Apache CXF](http://cxf.apache.org/docs/jax-rs-oauth2.html)


* [Google OAuth Playground](https://developers.google.com/oauthplayground/)


<br>
<br>

### REST Attachements

* check the project

<br>
<br>

### [Jersey](https://jersey.github.io/)

Jersey is Sun's production quality reference implementation for JSR 311: JAX-RS: The Java API for RESTful Web Services. Jersey implements support for the annotations defined in JSR-311, making it easy for developers to build RESTful web services with Java and the Java JVM. Jersey also adds additional features not specified by the JSR.
* Jersey provide servlet implementation which scans through the predefined classes which we define to identify the RESTful resources
* we configure Jersey servlet in web.xml.
* It also provides several custom tools for security like OAuth, WADL generation, bean validation support etc...
* By implement one simple REST resource and a client using Jersey - it easy to use any WS stack.


<br>
<br>

### Spring MVC
* Spring is a popular Dependency Injection framework in the Java Enterprise world.
* Along with DI, Spring provides easy ways to implement JDBC, messaging, ORM support like JPA and Hibernate support and even the spring MVC which makes it every easy to implemnt the web layer ot tier of our application.
* Starting from Spring 3.0 version, spring also supports implementation of RESTful web services in very easy fashion.
* It does not implement the JAX-RS standard ot it does not use the JAX-RS API or annotations.
* It comes up with its own set of annotations like the `@RequestMapping` annotation which is similar to the `@Path` annotation in the JAX-RS API
* `@PathVariable` similar to the `@PathParam` in the JAX-RS API on so on..

#### Spring MVC Flow
1. Typically, a client sends in a HTTP request which will be handled by the Front Controller(Dispatcher Servelt) very similar to Apache CXF or any other web service stacks like Jersey.
2. Front Controller will read the handler mappings or scan through all the controllers 
3. These controllers will handle th incoming requests and send back the appropriate response which could be JSON or XML or whatever back to the client.
4. If it a pure Spring MVC application, this controller would return the next view like a JSP page to the dispatcher servlet and the dispatcher servlet would send that reponse back to the client. But in case of RESTful WS we usually skip that step of using the model view or returning a, or using a view resolver and we simply return a reponse directly back to the client.


 ![Alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/webservices/images/mvcflow.png "mvcflow")











