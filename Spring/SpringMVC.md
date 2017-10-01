# Spring MVC

Spring mvc framework provides the facility to build flexible and loosely coupled web applications. MVC stands for Model-View-Controller design pattern which separates the business logic, presentation logic and navigation logic.

**Model:**
Model is responsible for encapsulating the application data (POJO).

**View:**
View is responsible for rendering the model data.

**Controller:**
Controller is responsible for receiving the user request, building model object and passing the model object to the view.

_Spring MVC framework uses the DispatcherServlet class as the controller which is responsible for handling all the requests and responses._ 

![alt text][logo]

[logo]: http://tutorialspointexamples.com/wp-content/uploads/2015/12/SpringMVCFlowDiagram.jpg "Spring MVC"

### Spring mvc framework execution flow:

•	Receive the user request.
•	Choose the controller with the help of HandlerMapping.
•	Controller process the request by calling the appropriate service method and returns a ModeAndView object to the DispatcherServlet which contains the model data and view name.
•	DispatcherServlet sends the view name to ViewResolver which sends the actual view to the DispatcherServlet.
•	DispatcherServlet will pass the model data to the View and render response.
