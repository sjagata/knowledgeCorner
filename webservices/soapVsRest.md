### HTTP Methods and Caching

#### SOAP
1. SOAP uses the POST method to tunnel in the request and response messages and we define the operations or mthods separately for our business logic that should be exposed out as Web Service
2. SOAP uses the WSDL file which defines the strict contract not only for the operations but also for data. The WSDL type ection is where we define the entire schema for the request and response can be validated against that schema. 
3. SOAP has WS standards advatage wherein we can use the standards like Reliable Messaging to send messages reliably and transcations, if you want that transcation to span across web service calls, we can use WS-transcations. And finally the important piece, the WS-Security which can secure the message SOAP request and response messages.
   3a. Using these Standards it is very easy to implement the non-functional requirements for an application
4. SOAP Overhead - Very limited memory for mobile applications 
   4a. SOAP always have SOAP-ENVELOPE overhead - Which the mobile device will feel difficult to handle because of memory issues.
5. SOAP support or uses XML by default and I haven't seen another implementation or other data format.
6. Since SOPA exists for so long, ther are mature tools like WSDL2JAVA which can be used to generate the clients very easily from the WSDL file 
 

#### REST
1. REST simply relies on the methods available in the HTTP Standard
   * GET
   * POST
   * PUT
   * DELETE to perfor the CRUD operations
* It provides a uniques inteface for the developers
* We can also cache serveral methods which are used by REST like GET, PUT and DELETE because they are idempotent. Caching tools that are available do not cache POST bacause it is non-idempotent.
If you perform POST more than once, it could result in different results or it changes the state of the application.
* Improves the performance of the application

2. WADL file which is the contract for the restful services only define HTTP methods ad URL's that can be accessed through those methods to consume the rest services. It doesn't define any data contract. WSDL 2.0 which is evolving promises that data contract in the WSDL given for restful services.
3. Application developers ending up writing a lot of non-functional requirements 
4. REST is very simple, it will not have any overhead.
5. REST supports multiple data formats 
6. REST doen't have many tools to do that 



Finally, to make a choice SOAP or REST, the non-functional requirements play a key role. If you have a lot of non-functionality for your application especially  in a huge enterprise where there are several applications communicating with each other and if you non-functional requirements(Security, Transcations, Reliable messaging) you should use SOAP as the REST is still evolving and it doesn't have a matured stack to perform all these non-functional requirements out of box.

* If you are exposing out your web services to various clients whom you even don't know today and you need a stric contract for that data, that is when we should be using SOAP because SOPA allows us to use WSLD which can define the contract both for operations as well as the data that is being exchanged.

* REST should be used especially because it scales well and it performs better because all its requests can be cached.
 
 ![Alt text](https://github.com/SandeepJagatha/knowledgeCorner/blob/master/webservices/images/soapVsrest.png "soapVsrest")
 
 

