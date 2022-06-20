# Payroll
 demo Employee
 https://spring.io/guides/tutorials/rest/

Spring makes accessing data easy. By simply declaring the following EmployeeRepository interface we automatically will be able to

Create new Employees

Update existing ones

Delete Employees

Find Employees (one, all, or search by simple or complex properties)

What happens when it gets loaded?

Spring Boot will run ALL CommandLineRunner beans once the application context is loaded.

This runner will request a copy of the EmployeeRepository you just created.

Using it, it will create two entities and store them.

HTTP is the Platform
To wrap your repository with a web layer, you must turn to Spring MVC. Thanks to Spring Boot, there is little in infrastructure to code. Instead, we can focus on actions:

@RestController indicates that the data returned by each method will be written straight into the response body instead of rendering a template.

An EmployeeRepository is injected by constructor into the controller.

We have routes for each operation (@GetMapping, @PostMapping, @PutMapping and @DeleteMapping, corresponding to HTTP GET, POST, PUT, and DELETE calls). (NOTE: It’s useful to read each method and understand what they do.)

EmployeeNotFoundException is an exception used to indicate when an employee is looked up but not found.

@ResponseBody signals that this advice is rendered straight into the response body.

@ExceptionHandler configures the advice to only respond if an EmployeeNotFoundException is thrown.

@ResponseStatus says to issue an HttpStatus.NOT_FOUND, i.e. an HTTP 404.

The body of the advice generates the content. In this case, it gives the message of the exception.

The return type of the method has changed from Employee to EntityModel<Employee>. EntityModel<T> is a generic container from Spring HATEOAS that includes not only the data but a collection of links.

linkTo(methodOn(EmployeeController.class).one(id)).withSelfRel() asks that Spring HATEOAS build a link to the EmployeeController 's one() method, and flag it as a self link.

linkTo(methodOn(EmployeeController.class).all()).withRel("employees") asks Spring HATEOAS to build a link to the aggregate root, all(), and call it "employees".


