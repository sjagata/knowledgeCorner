
### What is webservices ?

Webservices are `client-server` or `consumer-provider` applications that communicate on the n/w through the **HTTP protocol** and exchange messages or data as XML and in various other formats like JSON.

* They provide **_interoperability_** between software applications - meaning s/w applications running or developed in different programming languages can communicate with each other irrespective of the platform they are running on. 
_(A JAVA application running on a linux can communicate with a dotnet or python application running in windows environment)_
* They allow applications to be developed in a **_loosely coupled_** fashion - that is two or more applications can communicate with each other or can be integrated in a loosely coupled fashion. 
_(Application A which is using the services of Application B through WebServices today can easily switch to Application C to get same functionality as what the application B was providing it in a very loosely coupled fashion without changing a lot of code.)_
* Our clients can **_extend_** our applications through webservices. They can integrate the inhouse products which they have or products from another company with the product which we sell them throught the webservices which we expose. They can come up with their own logic by consuming our webservices. **_Extensibility_**
* we can also develop **_mashup application_** which can be consumers of more that one webservices. 
Ex: demo app using google map webservices.

### Types

1. SOAP - Use XML based SOAP messaages on http post method to do message exchange
2. RESTFUL - Use http method to the full that is they use all the methods available in the http protocol as a standard and support multiple data formats - along with XML they support JSON, Text etc..

> `JAX-WS` (JAVA API for XML based webservices) is the standard for implementing SOAP based webservices.

> `JAX-RS` (JAVA API for RESTFul webservices) is a standard for implementing RESTFul webservices 

### SOA Standard

**SOA** (Service Oriented Architecture) is a set of architectural principles to build loosely coupled applications.

**SOA** is collection of `architectural priniciples` to design and implement our software applications in such a way that they are composed of serveral s/w `services` that have simple well-defined intefaces and can use each other in a `loosely coupled` manner that withstand them.

In SOA world a service is an implementation of business logic that operates on its own.

SOA standard is maintained by open bodies like `W3C` and `OASIS` who come up with the architectural principles which we will then use in our applications to build good design and implement our applications so that they will benefit from all the advantages that SOA have.

Example:

`Appointment Management` ---> `Doctor Services` ---> `Client Services` ---> `Patient Service` ---> `Bed Management Service`

`Appointment Management` ---> `Patient Service` ---> `Bed Management Service`

They communicate with each other in a loosely coupled passion using a standard inteface meaning as long as this inteface b/w the doctor service and the clinical service remains the same. 

We can replace clinical service from a different company and use it as long as the contract b/w these DS and CS remain same.

This contract in case of 

SOAP ---> WSDL file
REST ---> WADL file

XML is the data format used to exchange messages.

### Advantages of WebServices 

1. Platform Independent 
2. Focussed Developer roles (ex : Doctor services, client services etc..)
3. Loosely Coupled
4. Reusability
5. Cost Reduction
6. Scalability (we can deploy services in multiple servers)
7. Availability (one servers goes down our consumers can call another server)

**XML** - carries both Data and MetaData, `Well-formedness` and `Validation`

Example : 

```xml
<OrderId>123</OrderId>
<ShippingInfo>...</ShippingInfo>
```

> MetaData - OrderID, ShippingInfo
> Data - 123 and info

* XML is mostly used for` data exchange`,  `configuration` files to `save data and manipulate and present` the data. 

Example : web.xml, server.xml, pom.xml and build.xml

**XML Schema Definition**
If XML follows XSD then it is called a valid xml document.

1. You can test the proper hierarchy of the XML nodes. [xsd defines which child should come under which parent, etc, abiding which will be counted as error, in above example, child_two cannot be the immediate child of root, but it is the child of "parent" tag which is in-turn a child of "root" node, there is a hierarchy..]
2. You can define Data type of the values of the nodes. [in above example child_two cannot have any-other data than number]
3. You can also define custom data_types, [example, for node <month>, the possible data can be one of the 12 months.. so you need to define all the 12 months in a new data type writing all the 12 month names as enumeration values .. validation shows error if the input XML contains any-other value than these 12 values .. ]
4. You can put the restriction on the occurrence of the elements, using minOccurs and maxOccurs, the default values are 1 and 1.


































