
## Servlet architecture overview


- Web application:
A web application or website is an application program which accessed over a network connection using HTTP and often runs inside a web browser.

- Web browser:
A web browser is a program which is act as an interface between user and web application e.g. Internet Explorer, Chrome, Safari, Mozilla firefox etc.

- CGI (Common gateway interface):
CGI was the first protocol or way of communication between web server and program. It passes a request from a web user to an application program and receives data back to forward to the web user i.e. It is responsible for dynamic content generation.

** Advantages of CGI : ** 
1. Technology portability: CGI programming can be written in variety of languages like c, c++, perl.
2. Web server portability: All service providers support CGI Programs.

** Disadvantages :  ** 
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
  <dd>**_javax.servlet_** and **_javax.servlet.http_** packages contains the classes and interfaces for servlet API. These packages are the standard part of Java’s enterprise edition.</dd>
  
  <dd>**javax.servlet ** contains a number of classes and interfaces which are mainly used by servlet container.</dd>
  
  <dd>**javax.servlet.http** contains a number of classes and interfaces which are mainly used by http protocol.

</dd>
</dl>
