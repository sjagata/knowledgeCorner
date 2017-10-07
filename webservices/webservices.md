
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


```xml

<!-- XSD -->
<?xml version="1.0" encoding="UTF-8"?>
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://www.test.com/Patient"
	xmlns:tns="http://www.test.com/Patient" xmlns:common="http://www.test.com/Common"
	elementFormDefault="qualified">

<!-- 	<include schemaLocation="PaymentType.xsd" /> -->

<!-- 	<import schemaLocation="Common.xsd" namespace="http://www.test.com/Common" /> -->

	<element name="patient" type="tns:Patient" />

	<complexType name="Patient">
		<sequence>
			<element name="name" type="tns:String15Chars" />
			<element name="age" type="int" />
			<element name="dob" type="date" />
			<element name="email" type="string" maxOccurs="unbounded" />
			<element name="gender" type="tns:Gender" />
			<element name="phone" type="string" />
			<element name="payment" type="tns:PaymentType" />
		</sequence>
		<attribute name="id" type="tns:Id" use="required" />
	</complexType>
	<complexType name="PaymentType">
		<choice>
			<element name="cash" type="int" />
			<element name="insurance" type="tns:Insurance" />
		</choice>
	</complexType>
	<complexType name="Insurance">
		<all>
			<element name="provider" type="string" />
			<element name="limit" type="int" />
		</all>
	</complexType>
	
	
	<simpleType name="Id">
		<restriction base="int">
			<pattern value="[0-9]*"></pattern>
		</restriction>
	</simpleType>
	<simpleType name="String15Chars">
		<restriction base="string">
			<maxLength value="15" />
		</restriction>
	</simpleType>
	<simpleType name="Gender">
		<restriction base="string">
			<enumeration value="M" />
			<enumeration value="F" />
		</restriction>
	</simpleType>

</schema>

```


```xml
<?xml version="1.0" encoding="UTF-8"?>
<tns:patient id="0" xmlns:tns="http://www.test.com/Patient"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.test.com/Patient Patient.xsd ">
	<tns:name>tns:name</tns:name>
	<tns:age>0</tns:age>
	<tns:dob>2001-01-01</tns:dob>
	<tns:email>tns:email</tns:email>
	<tns:gender>M</tns:gender>
	<tns:phone>tns:phone</tns:phone>
	<tns:payment>
		<tns:cash>0</tns:cash>
	</tns:payment>
</tns:patient>
```

<br>
<br>

** **

<br>
<br>

### SOAP

SOAP stands for Simple Object Access Protocol. It is used to transfer the data. It is a XML-based messaging-layer protocol. SOAP can be used in combination with a variety of transport protocols like HTTP, SMTP, and JMS etc.

**_Note: SOAP is part of the set of standards specified by the W3C._**

**Pros**
* They are platform independet
   * HTTP - Transport Independent
   * XML - Data Independent
* Application Tailoring/Customization
* Legacy Application are Great
   * HTML and XML
* New Revenue/Profit Channels
* Firewalls like Web Services

**Cons**
* Ambiguous web services standards
* Performance Impact due to Serialization and De-Serialization

#### When we have to use SOAP ?

* If a **Formal Contract is Required**  b/w webservice provider and consumer ---> WSDL
* lot of **Non Functional Requirements**
   * Security
   * Transaction Management
* If we need **Reliable Asynchronous Processing** or messaging b/w our webservice provider and consumer.

#### SOAP message structure:

* **Envelope:** It is a mandatory element and used to define the start and the end of the message. Root element in SOAP namespace
* **Header:** It is an optional element which provides the information on authentication, encoding of data, or how a recipient of a SOAP message should process the message. Used to send Meta information.
* **Body:** It is a mandatory element and contains the XML data comprising the message being sent.
* **Fault:** It is an optional element which provides information about errors that occur while processing the message.


```xml
<soap:Envelope>
	<soap:header>
		<soap:Body>
			<creditcard>
				...
			</creditcard>
			<soap:Fault>
				<soap:code>soap:Server</soap:code>
				<soap:Reason>
					<soap:text>
						Card Expired
					</soap:text>
				</soap:Reason>
			</soap:Fault>
		</soap:Body>
	</soap:header>
</soap:Envelope>
```

<br>
<br>

### WSDL 
**WSDL** (Web Services Description Language) is a contract b/w the web services provider and the consumer. It is a XML file with a .wsdl extension.

Ex : userProfile.wsdl

It tells - **_what this web service proides_**, **_how it provides it_** and **_how you can consume it_**?

* It tells what message a consumer should send in the request and what response will go back as the webservice.
* The wsdl file is divided into `abstract` portion and `physical` portion. 

#### Abstract/What

* The root element of wsdl file is **_definitions_**. 
* The Abstract portion tells what this webservice provides is comprised of four elements
   * **_type_** - We define all the data types which we need to exchange information for a particular webservice
      * Ex: `<xsd:element name="GetUserProfile">`(Request), `<xsd:element name="GetUserProfileResponse">`(Response)
   * **_messages_** - are analogous to parameters and return types in JAVA. We use these messages to come up with operations whicch are analoguous to the methods in JAVA
      * Ex: `<wsdl:message name="GetUserProfileRequest">` , `<wsdl:message name="GetUserProfileResponse">`
   * **_operation_**
   * **_porttype_** - is a container of all the operations your WS is providing
   
#### Physcial/How
* It is comproses of two elements **_binding_** and **_service_** tells how to consume this WS from the consumer.
   *  **_binding_** - tells how the consumer can consume WS and how the providers is going to send the responses back. Binding element comprises of a soap binding which by default is document literal wrapped and that is the recommeneded binding because the XML engines like apache cxf can validate the entire soap message. For each operation we wil define a binding.
   * **_service_** - tells how to access this WS that actually url inside a sub lement called port. We define a port for each WS and a url to access that WS.
   
**_Note : The link b/w abstract and physical section of a wsdl file is PortType `type="tns:UserProfilePortType"`._**
   

> userProfile.wsdl 

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<wsdl:definitions 
		xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/"
		xmlns:tns="http://wsdltest.com/userProfile" 
		xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/" 
		xmlns:xsd="http://www.w3.org/2001/XMLSchema" 
		name="UserProfileService" 
		targetNamespace="http://wsdltest.com/userProfile"
		xmlns:upSchema="http://wsdltest.com/userProfile/schema/UserProfile.xsd">
		
  <wsdl:types>
    <xsd:schema targetNamespace="http://wsdltest.com/userProfile" elementFormDefault="qualified">
	  <xsd:import  namespace="http://wsdltest.com/userProfile/schema/UserProfile.xsd" schemaLocation="UserProfile.xsd"/>
		<xsd:element name="GetUserProfile">
		<xsd:complexType>
			<xsd:sequence>
				<xsd:element name="userName" type="xsd:string"/>
			</xsd:sequence>
		</xsd:complexType>
		</xsd:element>
	    <xsd:element name="GetUserProfileResponse">
		<xsd:complexType>
			<xsd:sequence>
				<xsd:element name="UserProfile" type="upSchema:UserProfile"/>
			</xsd:sequence>
		</xsd:complexType>
		</xsd:element>
    </xsd:schema>
  </wsdl:types> 
  
  <wsdl:message name="GetUserProfileRequest">
    <wsdl:part name="params" element="tns:GetUserProfile"/>
  </wsdl:message>
  <wsdl:message name="GetUserProfileResponse">
    <wsdl:part name="result" element="tns:GetUserProfileResponse"/>
  </wsdl:message>
  
  <wsdl:portType name="UserProfilePortType">
    <wsdl:operation name="GetUserProfile">
      <wsdl:input message="tns:GetUserProfileRequest"/>
      <wsdl:output message="tns:GetUserProfileResponse"/>
    </wsdl:operation>	
  </wsdl:portType>
  
  <wsdl:binding name="UserProfileBinding" type="tns:UserProfilePortType">
    <soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http"/>
    <wsdl:operation name="GetUserProfile">
      <soap:operation soapAction="urn:GetUserProfile"/>
      <wsdl:input>
        <soap:body use="literal"/>
      </wsdl:input>
      <wsdl:output>
        <soap:body use="literal"/>
      </wsdl:output>
    </wsdl:operation>
  </wsdl:binding>
  
  <wsdl:service name="UserProfileService">
    <wsdl:port binding="tns:UserProfileBinding" name="UserProfilePort">
		<soap:address location="http://localhost/services/UserProfileService"/>
    </wsdl:port>
  </wsdl:service>
</wsdl:definitions>
```

> userProfile.xsd

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsd:schema
	xmlns:up="http://wsdltest.com/userProfile/schema/UserProfile.xsd"
	xmlns:xsd="http://www.w3.org/2001/XMLSchema"
	xmlns="http://wsdltest.com/userProfile/schema/UserProfile.xsd"
	targetNamespace="http://wsdltest.com/userProfile/schema/UserProfile.xsd"
	elementFormDefault="qualified" attributeFormDefault="unqualified">

	<xsd:complexType name="UserProfile">
		<xsd:sequence>
			<xsd:element name="userName" type="xsd:string" minOccurs="0" />
			<xsd:element name="email" type="xsd:string" minOccurs="0" />
			<xsd:element name="address" type="up:Address" minOccurs="0" />
		</xsd:sequence>
	</xsd:complexType>

	<xsd:complexType name="Address">
		<xsd:sequence>
			<xsd:element name="streetAddress" type="xsd:string" />
			<xsd:element name="city" type="xsd:string" />
			<xsd:element name="state" type="xsd:string" />
			<xsd:element name="country" type="xsd:string" />
			<xsd:element name="zipcode" type="xsd:string" />
		</xsd:sequence>
	</xsd:complexType>
</xsd:schema>
```

#### WSDL binding styles
There are 3 styles that will be impacted depending on the style we choose.

1. SOAP Payload
2. Validation
3. Operation Name SOAP Message

A WSDL document describes a web service. A WSDL binding describes how the service is bound to a messaging protocol, particularly the SOAP messaging protocol. A WSDL SOAP binding can be either a Remote Procedure Call (RPC) style binding or a document style binding. A SOAP binding can also have an encoded use or a literal use. 

This gives you four style/use models:

* RPC/encoded
* RPC/literal
* Document/encoded
* Document/literal

Add to this collection a pattern which is commonly called the document/literal wrapped pattern and you have five binding styles to choose from when creating a WSDL file. 

[Which style of wsdl i should use?](https://www.ibm.com/developerworks/library/ws-whichwsdl/)

<br>
<br>

### SOAP WS Design
Two different design approaches to impement SOAP WS: 
* Top Down or WSDL First or Contract First
* Code First or Bottom Up

#### Top Down or WSDL First or Contract First
Steps :
1. Create the WSDL File
2. Generate the java stubs using tools like wsdl2java
3. Implement the web services endpoint

**Advantages:**
* Contract with the consumer signed off.
* Better Interoperability
* Faster Integration


#### Code First or Bottom Up
Steps:
1. Write Java code and annotate
2. Generate the WSDL from the code using java2wsdl

**Advantages**
* Legacy Application Integration.

#### Which design to choose?

* Contract first except while exposing legacy applications as WS.
* If there we are designing a WS from scratch then use Contract First and if you going to expose a existing legacy application as WS then go with Code first.

<br>
<br>

### JAX - WS
JAVA API XML based WEB SERVICES

**JAX-WS** consists of:
* Specification - is a set of rules or guidelines from Oracle
   * This guidelines in the specification helps engines like `CXF`, `GlassFish` to implement JAX-WS
* API - is for developers.
   * It consists of a set of JAVA annotations 
   
#### CORE Annotations

:point_right: **@javax.jws.WebService**

```java
@javax.jws.WebService
public class OrderService
```

:point_right: **@javax.jws.WebMethod**

```java
@WebResult(name="order") Order getOrder(@WebParam(name="orderId") Long orderId)
```

:point_right: **@javax.xml.ws.WebFault**

```java
MyException extends Exception
```

:point_right: **@javax.jws.soap.SOAPBinding** -> document\literal

```java
@SOAPBinding(style=Style.RPC, use=Use.LITERAL)
public interface OrderService
```

:point_right: **@javax.xml.ws.RequestWrapper** 
:point_right: **@javax.xml.ws.ResponseWrapper** 

<br>
<br>

### JAXB
JAVA ARCHITECTURE for XML binding

* It provides an esay way to map Java classes and xml schema hiding the complexity of XML programming.
* Marshalling and Unmarshalling

`XML Schema` ---> `JAVA Objects` <br>
`Java Objects` ---> `XML Schema`

JAVA ---> JAXB ---> XML <br>
JAVA <--- JAXB <--- XML

**JAXB provides three tools:**

:one: **XJC** (XML Schema Compiler) <br> which can generate JAVA classes from a given xml schema file <br>
Ex: `XML Schema` ---> `XJC` ---> `JAVA Classes`

:two: SCHEMAGEN <br>
Ex: `Java Classes` --> SCHEMAGEN --> `XML Schema`

:three: RUNTIME API <br>
Ex: `JAVA Objects` --> Runtime API --> `XML`, `XML` --> Runtime API --> `JAVA Objects`

* Runtime API consists of marshalling class, unmarshalling class and then a set of annotations.

<br>
<br>

### Apache CXF
Using this we can develop the WS providers and WS Consumers for both SOAP and RESTFul WS

#### Why CXF?

* It comes with the both SOAP/REST Engine (JAX-WS and JAX-RS)
   * Serialize and De-Serialize
   * Publish and Dispatch <br>
   `XML` <--> `SOAP/Rest Engine` <--> `JAVA Objects` <--> `WS Endpoint Method` 
* It implements Web Service Standards 
   * WS-Security
   * WS-Policy etc
* Tools   
   * wsdl2java
   * java2wsdl
* Spring Configuration
* Extend and Customize
   * Interceptors and Handler
* Documentation and Samples

[More Info for cxf](http://cxf.apache.org)

_Note : Check SOAP WSDL First and Code First applications for more details_

<br>
<br>

### WS-Security
Since WS are used to communicate across applications running on heterogenous platforms they need to work with each other in a seamless fashion. 

Ex: 

`Online Shoppping Application` --> connect to a banks payment gateway(typically a WS) --> `Banks Payment Gateway WS`

Here, the bank will ask us to authenticate by passing a username and password to make sure it is genuine.
Banks uses some WS-Standards to make sure it is a genuine call.

:hocho: **WS-Security** standard addresses three important issues around security.

:bomb: **Authentication** - Three ways to do it: 
* User name token profile.
* X 508 Certificates
* SAML - single signon

:bomb: **Confidentiality** - Encryption and Decryption

:bomb: **Integrity** - XML Signature

:hocho: **MTOM** - For exchanging files

:hocho: **WS-Addressing** - Asynchronous Callbacks

:hocho: **WS-Policy** - Assert and mandate certain rules to consume our WS
	
:hocho: **WS-SecureConversation** - Improve performance while encrypting and decrypting by negotiating a key at the beginning
	
:hocho: **WS-SecurityPolicy** - Assert WS-Security requirements.

<br>
<br>

### JAX-WS Handler
As we create service oriented applications and develop several web service endpoints and web services consumers or clients, once in a while we need to address some cross-cutting concerns or non functional requirements whch have to be applied across WS clients ot across WS endpoints. These requirements might not have anything to do with the business logic, but they need us to manipulate the SOAP message/SOAP headers/SOAP body.

ll'ly to servlet Filters can be applied both on client side and server side.

* Used when we need custom authnetication mechanism.
* Caching calls
* Versioning (to call WS-Enpoint 1.0 or WS-Endpoint 1.1 can be declared in JAX-WS Handlers)

#### Two types of handlers

1. SOAP Handlers - have access to entire message [<soap-header>, <soap-body>]
2. Logical Handlers - payload only [<soap-body>...</soap-body>]


```java
SOAPHAndler<SOAPMessageContext>
```

* handleMessage
* handleFault
* getHandlers
* close

> `handleMessage` and `getHeaders` are called both on the way in as well as on way out on the client side as well as on the provider side. They are called twice

> `handleFault` is called only when there is a SOAP Fault

> `close` is called on the way out at the end of the entire flow. cleanup code 

```java
LogicalHandler<LogicalMessageContext
```

* handleMessage
* handleFault
* close


#### Steps:
* Design the handler chain
* Create the handlers
* Configure the handlers






























