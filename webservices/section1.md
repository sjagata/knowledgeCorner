
### What is webservices ?

Webservices are `client-server` or `consumer-provider` applications that communicate on the n/w through the **HTTP protocol** and exchange messages or data as XML and in various other formats like JSON.

* They provide **interoperability** between software applications - meaning s/w applications running or developed in different programming languages can communicate with each other irrespective of the platform they are running on. 
_(A JAVA application running on a linux can communicate with a dotnet or python application running in windows environment)_
* They allow applications to be developed in a **loosely coupled** fashion - that is two or more applications can communicate with each other or can be integrated in a loosely coupled fashion. 
_(Application A which is using the services of Application B through WebServices today can easily switch to Application C to get same functionality as what the application B was providing it in a very loosely coupled fashion without changing a lot of code.)_
* Our clients can **extend** our applications through webservices. They can integrate the inhouse products which they have or products from another company with the product which we sell them throught the webservices which we expose. They can come up with their own logic by consuming our webservices.
* we can also develop **mashup application** which can be consumers of more that one webservices. 
Ex: demo app using google map webservices.

### Types

1. SOAP - Use XML based SOAP messaages on http post method to do message exchange
2. RESTFUL - Use http method to the full that is they use all the methods available in the http protocol as a standard and support multiple data formats - along with XML they support JSON, Text etc..

> `JAX-WS` (JAVA API for AXML based webservices) is the standard for implementing SOAP based webservices.

> `JAX-RS` (JAVA API for RESTFul webservices) is a standard for implementing RESTFul webservices 

### SOA Standard

**SOA** is collection of `architectural priniciples` to design and implement our software applications in such a way that they are composed of serveral s/w `services` that have simple well-defined intefaces and can use each other in a `loosely coupled` manner that withstand them.

SOA standard is maintained by open parties like `W3C` and `OASIS` who come up with the architectural principles which we will then use in our applications to build good design and implement our applications so that they will benefit from all the advantages that SOA have.

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

**1. Platform Independent 
2. Focussed Developer roles (ex : Doctor services, client services etc..)
3. Loosely Coupled
4. Reusability
5. Cost Reduction
6. Scalability (we can deploy services in multiple servers)
7. Availability (one servers goes down our consumers can call another server)**



































