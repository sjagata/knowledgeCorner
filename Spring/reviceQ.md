### Example for spring core dependency injection ?
When we make call to CustomerController spring will take care of injecting CustomerService - creatin object etc..

```java
@Controller
@RequestMapping("/customer")
public class CustomerController {

	// need to inject our customer service
	@Autowired
	private CustomerService customerService;

```

### Spring MVC

### 
