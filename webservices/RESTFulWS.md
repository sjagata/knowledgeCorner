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



  

 
 
 
 
 
 
 
 
 
 
 
 
