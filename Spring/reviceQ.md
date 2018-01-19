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

### Differences between Line and Branch coverage
Sol:  [stackoverflow](https://stackoverflow.com/questions/8229236/differences-between-line-and-branch-coverage)
