
# WebAPI

# TOC
* [Getting an Employee the WCF Way](#getting-an-employee-the-wcf-way)
* [Getting an Employee the ASP.NET Web API Way](#getting-an-employee-the-aspnet-web-api-way)
* [Simple REST API](#simple-rest-api)
* [Routing](#routing)
* [Controllers](#controllers )
* [Actions](#actions)
* [Message Handlers](#message-handlers)
* [Filters](#filters)
* [Media Type Formatters ](#media-type-formatters )
* [Model Binding](#model-binding)
* [Input Validation](#input-validation)
* [Dependency Resolution](#dependency-resolution)
* [Testing](#testing)
* [Securing the Service](securing-the-service)
* [Optimization and Performance](#optimization-and-performance)
* [Hosting](#hosting)
* [Error Handling](#error-handling)
* [Tracing and Logging](#Tracing-and-Logging)
* [API Documentation](#api-documentation)
* [Useful URL](#useful-url)


## Getting an Employee the WCF Way
```cs
[ServiceContract]
public interface IEmployeeService
{
	[OperationContract]
	[WebGet(UriTemplate = "/Employees/{id}")]
	Employee GetEmployee(string id);
}
	
public class EmployeeService : IEmployeeService
{
	public Employee GetEmployee(string id)
	{
		return new Employee() { Id = id, Name = "John Q Human" };
	}
}

[DataContract]
public class Employee
{
	[DataMember]
	public int Id { get; set; }
	
	[DataMember]
	public string Name { get; set; }
	
	// other members
}
```

## Getting an Employee the ASP.NET Web API Way
```cs
public class EmployeeController : ApiController
{
	public Employee Get(string id)
	{
		return new Employee() { Id = id, Name = "John Q Human" };
	}
}
```

## Simple REST API 

```cs
public class EmployeesController : ApiController
{
	private static IList<Employee> list = new List<Employee>()
	{
		new Employee()
		{
		Id = 12345, FirstName = "John", LastName = "Human"
		},
		new Employee()
		{
		Id = 12346, FirstName = "Jane", LastName = "Public"
		},
		new Employee()
		{
		Id = 12347, FirstName = "Joseph", LastName = "Law"
		}
	};
	
	// GET api/employees
	public IEnumerable<Employee> Get()
	{
		return list;
	}
	
	// GET api/employees/12345
	public Employee Get(int id)
	{
		return list.First(e => e.Id == id);
	}

	// POST api/employees
	public void Post(Employee employee)
	{
		int maxId = list.Max(e => e.Id);
		employee.Id = maxId + 1;
		list.Add(employee);
	}
	
	// PUT api/employees/12345
	public void Put(int id, Employee employee)
	{
		int index = list.ToList().FindIndex(e => e.Id == id);
		list[index] = employee;
	}
	
	// DELETE api/employees/12345
	public void Delete(int id)
	{
		Employee employee = Get(id);
		list.Remove(employee);
	}
}
```


## Routing
```cs
// WebApiConfig.cs
public static class WebApiConfig
{
	public static void Register(HttpConfiguration config)
	{
	
		// Default catch-all
		config.Routes.MapHttpRoute(
			name: "DefaultApi",
			routeTemplate: "api/{controller}/{id}",
			defaults: new { id = RouteParameter.Optional }
		);
		
		//RPC-style
		config.Routes.MapHttpRoute(
            		name: "RpcApi",
            		routeTemplate: "api/{controller}/{action}/{id}",
            		defaults: new { id = RouteParameter.Optional }
        	);
        
	    // Matches route with the taskNum parameter
		config.Routes.MapHttpRoute(
			name: "FindByTaskNumberRoute",
			routeTemplate: "api/{controller}/{taskNum}",
			defaults: new { taskNum = RouteParameter.Optional }
		);
	
		config.Routes.MapHttpRoute( 
			name: "PostByDate", 
			routeTemplate: "api/Posts/{year}/{month}/{day}", 
			defaults: new { controller = "Posts", month = RouteParameter.Optional, day = RouteParameter.Optional } );
		
		//Works: http://localhost:55778/api/123/employees/12345
		//Doesn't Works: http://localhost:55778/api/abc/employees/12345
		config.Routes.MapHttpRoute(
			name: "DefaultApi",
			routeTemplate: "api/{orgid}/{controller}/{id}",
			defaults: new { id = RouteParameter.Optional },
			constraints: new { orgid = @"\d+" }
		);

		config.Routes.MapHttpRoute( 
			name: "PostByDate", 
			routeTemplate: "api/Posts/{year}/{month}/{day}", 
			defaults: new { 
				controller = "Posts", month = RouteParameter.Optional, day = RouteParameter.Optional}, 
			constraints: new { 
				month = @"\d{0,2}", day = @"\d{0,2}" } 
				);
				
		//Using a Built-in Constraint
		//Add - using System.Web.Http.Routing.Constraints;
		config.Routes.MapHttpRoute(
			name: "ChromeRoute",
			routeTemplate: "api/today/{action}",
			defaults: new { controller = "today" },
			constraints: new {
				useragent = new UserAgentConstraint("Chrome"),
				action = new RegexRouteConstraint("daynumber|othermethod")
			}
		);		
		
		//api/Posts/Category/10
		config.Routes.MapHttpRoute( 
			name: "PostsCustomAction",
			routeTemplate: "api/{controller}/{action}/{id}", 
			defaults: new { id = RouteParameter.Optional } );
		

		config.Routes.MapHttpRoute(
            name: "DefaultApi",
            routeTemplate: "api/{controller}/{id}",
            defaults: new { id = RouteParameter.Optional },
            constraints: null,
            handler: new CustomHttpControllerDispatcher(config)
        );

		//Defining a Route with Data Tokens
		config.Routes.Add(
			"CustomHandler",
			config.Routes.CreateRoute(
			routeTemplate: "api/{controller}/{action}",
			defaults: null,
			constraints: null,
			dataTokens: new Dictionary<string, object> {
			{ "response", "Tomorrow" }
			},
			handler: new CustomRouteHandler())
		);
	
        config.Routes.MapHttpRoute("product-delete", "products/{productId}",
            new { controller = "Products", action = "DeleteProduct", logging = true },
            new { httpMethod = new HttpMethodConstraint("DELETE") });
    }
}
```

### Route Registration in ASP.NET Web API with ASP.NET Hosting
```cs
protected void Application_Start(object sender, EventArgs e) {
	var config = GlobalConfiguration.Configuration;
	var routes = config.Routes;
	
	routes.MapHttpRoute(
		"DefaultHttpRoute",
		"api/{controller}/{id}",
		new { id = RouteParameter.Optional }
		);
	
	//Sample 2: Sample Route Registration	
	GlobalConfiguration.Configuration.Routes.MapHttpRoute(
		"DefaultHttpRoute",
		"api/{controller}/{id}",
		new { id = RouteParameter.Optional }
		);	
		
	//Having Multiple Web API Routes	
	var routes1 = GlobalConfiguration.Configuration.Routes;
		routes.MapHttpRoute(
		"DefaultHttpRoute",
		"api/{controller}/{id}",
		new { id = RouteParameter.Optional }
		);
		
	routes1.MapHttpRoute(
		"VehicleHttpRoute",
		"api/{vehicletype}/{controller}",
		defaults: new { },
		constraints: new { controller = "^vehicles$" }
		);
}

```

### Define Direct Routes
```cs
public class TeamsController : ApiController
{
	[Route("api/teams/{id}")]
	public Team GetTeam(int id)
	{
		//omitted for brevity
	}
	
	[Route("api/teams")]
	public IEnumerable<Team> GetTeams()
	{
		//omitted for brevity
	}
	[Route("api/teams/{teamId}/players")]
	public IEnumerable<Player> GetPlayers(int teamId)
	{
		//omitted for brevity
	}
}

Add this in the config.
config.MapHttpAttributeRoutes();

//Route Prefix
[RoutePrefix("api/teams")]
public class TeamsController : ApiController
{
	[Route("{id}")]
	public Team GetTeam(int id)
	{
	//omitted for brevity
	}
}
```

### Set Default Route Values
```cs
//centralized
config.Routes.MapHttpRoute(
name: "DefaultApi",
routeTemplate: "{controller}/{id}",
defaults: new { id = 100 }
);

//attribute routing
[Route("items/{id:int=100}")]
public HttpResponseMessage Get(int id) {}

//inline
public HttpResponseMessage Get(int id = 100) {}

myapi.com/items/
myapi.com/items/100
```

### Set Optional Route Values

```cs
Usage of Optional Parameters with Attribute Routing
[Route("orders/{skip?},{take?}")]
public HttpResponseMessage GetFiltered(int? skip = null, int? take = null)
{
	var query = orders.AsQueryable();
	if (skip.HasValue)
	{
		query = query.Skip(skip.Value);
	}
	if (take.HasValue)
	{
		query = query.Take(take.Value);
	}
	return Request.CreateResponse(HttpStatusCode.OK, query);
}


Usage of Optional Parameters with Centralized Routing
config.Routes.MapHttpRoute(
name: "OrdersFilter",
routeTemplate: "orders/{skip},{take}}",
defaults: new {skip = RouteParameter.Optional, take = RouteParameter.Optional}
);
```

### Set Route Constraints
```cs
config.Routes.MapHttpRoute(
	name: "DefaultApi",
	routeTemplate: "orders/{text}",
	constraints: new { text = new AlphaRouteConstraint() },
	defaults: null
	);

config.Routes.MapHttpRoute(
	name: "DefaultApi",
	routeTemplate: "size/{id}",
	constraints: new { httpMethod = new HttpMethodConstraint(HttpMethod.Get) },
	defaults: null
	);	
```
	
### Define Remote Procedure Call Style Routes	
```cs
config.Routes.MapHttpRoute(
	name: "LatestOrder",
	routeTemplate: "api/orders/getlatestorder"}",
	defaults: new { controller = "Orders", action = "GetLatestOrder" }
	);

config.Routes.MapHttpRoute(
	name: "Orders",
	routeTemplate: "api/orders/{action}/{id}",
	defaults: new { controller = "Orders", id = RouteParameter.Optional }
	);

config.Routes.MapHttpRoute(
	name: "DefaultApi",
	routeTemplate: "api/{controller}/{action}/{id}",
	defaults: new { id = RouteParameter.Optional }
	);

the client now has to call your HTTP endpoints in the following matter:
• myapi.com/api/orders/getall
• myapi.com/api/orders/getbyid/1


//the controller is OrdersController
[Route("orders/getbyid/{id}")]
public HttpResponseMessage Get(int id)
{
	//omitted for brevity
}

[Route("orders/getall")]
public HttpResponsesMessage GetAll()
{
	//omitted for brevity
}

[RoutePrefix("direct")]
[Route("items/{action}")]
public class ItemsController : ApiController
{
	//omitted for brevity
}
```

### Create Catch-all Routes
```cs
config.Routes.MapHttpRoute(
	name: "DefaultApi",
	routeTemplate: "{*params}"
	);

public class ProxyController : ApiController
{
	[Route("{*params}")]
	public HttpResponseMessage Get(string params)
	{
		//omitted for brevity
	}
}

GET myapi.com/1
• GET myapi.com/hello
• GET myapi.com/www.google.com
• GET myapi.com/monday/filip/192.5

Catch-all ASP.NET Web API Routes—But Only for Requests for proxy/*
config.Routes.MapHttpRoute(
	name: "DefaultApi",
	routeTemplate: "proxy/{*params}"
	);

public class ProxyController : ApiController
{
	[Route("proxy/{*params}")]
	public HttpResponseMessage Get(string params)
	{
		//omitted for brevity
	}
}
```

### Prevent Controller Methods from Inadvertently Becoming Web API Endpoints
```cs
//not an action
[NonAction]
public string GetCustomer()
{
	//omitted for brevity
}
```

### Localize Routes
```cs
public class Startup
{
public void Configuration(IAppBuilder appBuilder)
{
	var config = new HttpConfiguration();
	config.MapHttpAttributeRoutes(new LocalizedDirectRouteProvider());	//Custom Implementation
	LocalizedRouteAttribute.Routes.Add("order", new Dictionary<string, string>
	{
		{ "de-CH", "auftrag" },
		{ "pl-PL", "zamowienie" }
	});
	LocalizedRouteAttribute.Routes.Add("orderById", new Dictionary<string, string>
	{
		{ "de-CH", "auftrag/{id:int}" },
		{ "pl-PL", "zamowienie/{id:int}" }
	});
	appBuilder.UseWebApi(config);
	}
}


public class OrdersController : ApiController
{
	[LocalizedRoute("order", Name = "order")]
	public HttpResponseMessage Get()
	{
		//omitted for brevity
	}
	[LocalizedRoute("order/{id:int}", Name = "orderById")]
	public HttpResponseMessage GetById(int id)
	{
		//omitted for brevity
	}
}

• myapi.com/order (English route)
• myapi.com/auftrag (German route)
• myapi.com/zamowienie (Polish route)
• myapi.com/order/{id} (English route)
• myapi.com/auftrag/{id} (German route)
• myapi.com/zamowienie/{id} (Polish route)
```

### Generate a Link to the Route
```cs
var routeLink = Url.Link("GetTeamById", new {id = team.Id});
```

## Controllers


### Controller Sample

public class CarsController : ApiController {
	private readonly CarsContext _carsCtx = new CarsContext();
	
	//NonActionAttribute
	[NonAction]
	public string[] GetCars() {
		return new string[] {
		"Car 1",
		"Car 2",
		"Car 3"
		};
	}

	//Get Action
	public IEnumerable<Car> Get() {
		var cars = _carsCtx.All;
		
		HttpResponseMessage response =
		Request.CreateResponse<string[]>(HttpStatusCode.OK, cars);
		response.Headers.Add("X-Foo", "Bar");
		return response;
	}
	
	//Get Action
	public Car GetCar(int id) {
		var carTuple = _carsCtx.GetSingle(id);

		if (!carTuple.Item1) {
			var response = 	Request.CreateResponse(HttpStatusCode.NotFound);
			throw new HttpResponseException(response);
		}
		return carTuple.Item2;
	}


	//Post Action
	public HttpResponseMessage PostCar(Car car) {
		var createdCar = _carsCtx.Add(car);
		var response = Request.CreateResponse(HttpStatusCode.Created, createdCar);
		response.Headers.Location = new Uri(Url.Link("DefaultHttpRoute", new {	id = createdCar.Id }));
		return response;
	}
	
	//Put Action
	public Car PutCar(int id, Car car) {
		car.Id = id;
		if (!_carsCtx.TryUpdate(car)) {
			return new HttpResponseMessage(HttpStatusCode.NotFound);
		}
		return car;
	}
	
	//Delete Action Method
	public HttpResponseMessage DeleteCar(int id) {
		if (!_carsCtx.TryRemove(id)) {
			return new HttpResponseMessage(HttpStatusCode.NotFound);
		}
		return Request.CreateResponse(HttpStatusCode.OK);
	}
}


```cs
//Defining a Common Prefix
[RoutePrefix("api/today")]
public class TodayController : ApiController {
}

//Applying the Route Attribute to the Controller
[Route("{action=DayOfWeek}")]
public class TodayController : ApiController {
}

//Consolidating the Direct Routes
[Route("{action=DayOfWeek}/{day:range(0, 6)}")]
public class TodayController : ApiController {
}

//Using a Custom Route Attribute
[UserAgentConstraintRoute("{action=DayOfWeek}/{day:specval(2)}")]
public class TodayController : ApiController {
}

//Applying the CustomControllerConfigAttribute
[CustomControllerConfig]
public class CustomController : ApiController {
}
```



### A Sample Controller Action That Throws HttpResponseException
```cs
public class CarsController : ApiController {
	
	public string[] GetCars() {
		try {
			int left = 10,
			right = 0;
			var result = left / right;
		}
		catch (DivideByZeroException ex) {
			var faultedResponse = Request.CreateResponse(HttpStatusCode.InternalServerError, new HttpError(ex, includeErrorDetail: true));
			
			throw new HttpResponseException(faultedResponse);
		}
			return new[] {
			"Car 1",
			"Car 2",
			"Car 3"
			};
	}

}

```


### Retrieval of Employees by Department
```cs
//http://localhost:55778/api/employees?department=2
public IEnumerable<Employee> GetByDepartment(int department)
{
	int[] validDepartments = {1, 2, 3, 5, 8, 13};
	if (!validDepartments.Any(d => d == department))
	{
		var response = new HttpResponseMessage()
		{
			StatusCode = (HttpStatusCode)422, // Unprocessable Entity
			ReasonPhrase = "Invalid Department"
		};
		throw new HttpResponseException(response);
	}
	return list.Where(e => e.Department == department);
}
```



### It is possible to apply multiple conditions based on parameters. 
```cs
http://localhost:port/api/employees?department=2&lastname=Smith


Listing 1-21. Retrieving an Employee by Applying Two Conditions
public IEnumerable<Employee> Get([FromUri]Filter filter)
{
	return list.Where(e => e.Department == filter.Department &&
	e.LastName == filter.LastName);
}

//Create a class named Filter, under the Models folder.
public class Filter
{
	public int Department { get; set; }
	public string LastName { get; set; }
}
```


### Creating a Resource with a Server-Generated Identifier
```cs
//Creating an Employee using HTTP POST
public HttpResponseMessage Post(Employee employee)
{
	int maxId = list.Max(e => e.Id);
	employee.Id = maxId + 1;
	list.Add(employee);
	
	var response = Request.CreateResponse<Employee>(HttpStatusCode.Created, employee);
	
	string uri = Url.Link("DefaultApi", new { id = employee.Id });
	response.Headers.Location = new Uri(uri);
	
	return response;
}

//Output: Response Status Code and Headers
HTTP/1.1 201 Created
Date: Mon, 26 Mar 2013 07:35:07 GMT
Location: http://localhost:55778/api/employees/12348
Content-Type: application/json; charset=utf-8
```


### Creating a Resource with a Client-Supplied Identifier

//A resource such as an employee can be created by an HTTP PUT to the URI http://localhost:port/api/ employees/12348, 
//where the employee with an ID of 12348 does not exist until this PUT request is processed.
//In this case, the request body contains the JSON/XML representation of the resource being added, which is the new employee.

```cs
Creating an Employee using HTTP PUT
public HttpResponseMessage Put(int id, Employee employee)
{
	if (!list.Any(e => e.Id == id))
	{
		list.Add(employee);
		var response = Request.CreateResponse<Employee>(HttpStatusCode.Created, employee);
		
		string uri = Url.Link("DefaultApi", new { id = employee.Id });
		response.Headers.Location = new Uri(uri);
		return response;
	}
	return Request.CreateResponse(HttpStatusCode.NoContent);
}
```

### Overwriting a Resource
//A resource can be overwritten using HTTP PUT. This operation is generally considered the same as updating the resource, but there is a difference.
```cs
public HttpResponseMessage Put(int id, Employee employee)
{
	int index = list.ToList().FindIndex(e => e.Id == id);
	if (index >= 0)
	{
		list[index] = employee; // overwrite the existing resource
		return Request.CreateResponse(HttpStatusCode.NoContent);
	}
	else
	{
		list.Add(employee);
		var response = Request.CreateResponse<Employee>
		(HttpStatusCode.Created, employee);
		string uri = Url.Link("DefaultApi", new { id = employee.Id });
		response.Headers.Location = new Uri(uri);
		return response;
	}
}
```

### Updating a Resource
//A resource such as an employee in our example can be updated by an HTTP POST to the URI
//http://server/api/employees/12345, where the employee with an ID of 12345 already exists in the system.
```cs
public HttpResponseMessage Post(int id, Employee employee)
{
	int index = list.ToList().FindIndex(e => e.Id == id);
	if (index >= 0)
	{
		list[index] = employee;
		return Request.CreateResponse(HttpStatusCode.NoContent);
	}
	return Request.CreateResponse(HttpStatusCode.NotFound);
}
```

### Route
```cs
[RoutePrefixAttribute("api/employeeTasks")]
public class TasksController : ApiController
{
	[Route("{id:int:max(100)}")]
	public string GetTaskWithAMaxIdOf100(int id)
	{
		return "In the GetTaskWithAMaxIdOf100(int id) method, id = " + id;
	}
	
	[Route("{id:int:min(101)}")]
	[HttpGet]
	public string FindTaskWithAMinIdOf101(int id)
	{
		return "In the FindTaskWithAMinIdOf101(int id) method, id = " + id;
	}
{
```

## Actions
```cs
public class RsvpController : ApiController {
	[HttpGet]
	public IEnumerable<GuestResponse> Attendees() {
		return Repository.Responses.Where(x => x.WillAttend == true);
	}
	
	[HttpPost]
	public void Add(GuestResponse response) {
		if (ModelState.IsValid) {
		Repository.Add(response);
		}
	}
	
	//Binding Request Data As an Array
	[HttpGet]
	[HttpPost]
	public string SumNumbers([ModelBinder] int[] numbers) {
		return numbers.Sum().ToString();
	}
	
	//Binding Request Data As a Strongly Typed Collection
	[HttpGet]
	[HttpPost]
	public string SumNumbers([ModelBinder] List<int> numbers) {
		return numbers.Sum().ToString();
	}
	
	//Adding an Action Method
	[HttpGet]
	[Route("api/products/noop")]
	public IHttpActionResult NoOp() {
		return Ok();
	}
	
	//Using a StatusCodeResult
	public IHttpActionResult Delete(int id) {
		repo.DeleteProduct(id);
		return StatusCode(HttpStatusCode.NoContent);
	}
	
	//Using the ResponseMessage Method
	public IHttpActionResult Delete(int id) {
		repo.DeleteProduct(id);
		return ResponseMessage(new HttpResponseMessage(HttpStatusCode.NoContent));
	}
	
	//Using a Custom Action Method
	public IHttpActionResult Delete(int id) {
		repo.DeleteProduct(id);
		return new MyNoContentResult();
	}
	
	//Defining Direct Routes
	[HttpGet]
	[Route("api/today/dayofweek")]
	public string DayOfWeek() {
		return DateTime.Now.ToString("dddd");
	}

	//Defining Direct Routes
	[HttpGet]
	[Route("api/today/dayofweek/{day}")]
	public string DayOfWeek(int day) {
		return Enum.GetValues(typeof(DayOfWeek)).GetValue(day).ToString();
	}

	//To prevent the prefix from being applied
	[HttpGet]
	[Route("~/getdaynumber")]
	public int DayNumber() {
		return DateTime.Now.Day;
	}

	//Defining an Optional Segment
	[HttpGet]
	[Route("dayofweek/{day?}")]
	public string DayOfWeek(int day = -1) {	//set a default value on the action method parameter
		if (day != -1) {
			return Enum.GetValues(typeof(DayOfWeek)).GetValue(day).ToString();
		} else {
			return DateTime.Now.ToString("dddd");
		}
	}

	//Handling an Optional Segment
	[HttpGet]
	[Route("dayofweek/{day?}")]
	public IHttpActionResult DayOfWeek(int day = -1) {
		if (RequestContext.RouteData.Values.ContainsKey("day")) {
			return day != -1 	? Ok(Enum.GetValues(typeof(DayOfWeek)).GetValue(day).ToString()) 	: (IHttpActionResult)BadRequest("Value Out of Range");
		} else {
			return Ok(DateTime.Now.ToString("dddd"));
		}
	}

	//Defining a Default Segment Value
	[Route("dayofweek/{day=-1}")]
	public string DayOfWeek(int day) {
		if (day != -1) {
			return Enum.GetValues(typeof(DayOfWeek)).GetValue(day).ToString();
		} else {
			return DateTime.Now.ToString("dddd");
		}
	}

	//Applying a Constraint to a Direct Route
	[HttpGet]
	[Route("dayofweek/{day:int=-1}")]
	public string DayOfWeek(int day) {
		if (day != -1) {
			return Enum.GetValues(typeof(DayOfWeek)).GetValue(day).ToString();
		} else {
			return DateTime.Now.ToString("dddd");
		}
	}

	[HttpGet]
	[Route("dayofweek")]
	public string DayOfWeek() {
		return DateTime.Now.ToString("dddd");
	}

	[HttpGet]
	[Route("dayofweek/{day:range(0, 6)}")]
	public string DayOfWeek(int day) {
		return Enum.GetValues(typeof(DayOfWeek)).GetValue(day).ToString();
	}
	
	[AcceptVerbs("GET")]
	public Employee RetrieveEmployeeById(int id)
	{
		return list.First(e => e.Id == id);
	}

	//Applying the Order Property to the Route Attribute
	[HttpGet]
	[Route("~/getdaynumber", Order=1)]
	public int DayNumber() {
		return DateTime.Now.Day;
	}

	//Specifying HTTP Verbs
	[AcceptVerbs("GET", "HEAD")]
	public string DayOfWeek() {
		return DateTime.Now.ToString("dddd");
	}
	
	[CustomException]
	public Product Get(int id) {
		return products[id];
		//return products.Where(x => x.ProductID == id).FirstOrDefault();
	}
	
}		
```

## Securing the Service
```cs
//Applying Authorization in the ProductsController.cs File
[Authorize(Roles = "Administrators")]
public async Task DeleteProduct(int id) {
	await Repository.DeleteProductAsync(id);
}
```


### The Authorization Filter
```cs

[Route("", Name = "AddTaskRoute")]
[HttpPost]
[Authorize(Roles = Constants.RoleNames.Manager)]
public IHttpActionResult AddTask(HttpRequestMessage requestMessage, NewTask newTask)
{
	var task = _addTaskMaintenanceProcessor.AddTask(newTask);
	var result = new TaskCreatedActionResult(requestMessage, task);
	return result;
}
```

### A Message Handler to Support HTTP Basic Authentication
```cs

//IBasicSecurityService.cs
public interface IBasicSecurityService
{
	bool SetPrincipal(string username, string password);
}

//BasicSecurityService.cs
public class BasicSecurityService : IBasicSecurityService
{
	public virtual IPrincipal GetPrincipal(User user)
	{
		var identity = new GenericIdentity(user.Username, Constants.SchemeTypes.Basic);
		identity.AddClaim(new Claim(ClaimTypes.GivenName, user.Firstname));
		identity.AddClaim(new Claim(ClaimTypes.Surname, user.Lastname));
		var username = user.Username.ToLowerInvariant();
		
		switch (username)
		{
		case "bhogg":
			identity.AddClaim(new Claim(ClaimTypes.Role, Constants.RoleNames.Manager));
			identity.AddClaim(new Claim(ClaimTypes.Role, Constants.RoleNames.SeniorWorker));
			identity.AddClaim(new Claim(ClaimTypes.Role, Constants.RoleNames.JuniorWorker));
			break;
		case "jbob":
			identity.AddClaim(new Claim(ClaimTypes.Role, Constants.RoleNames.SeniorWorker));
			identity.AddClaim(new Claim(ClaimTypes.Role, Constants.RoleNames.JuniorWorker));
			break;
		case "jdoe":
			identity.AddClaim(new Claim(ClaimTypes.Role, Constants.RoleNames.JuniorWorker));
			break;
		default:
			return null;
		}
		return new ClaimsPrincipal(identity);
	}
}
```

### Auditing
```cs
public class UserAuditAttribute : ActionFilterAttribute
{
	private readonly ILog _log;
	private readonly IUserSession _userSession;
	public UserAuditAttribute()
	: this(WebContainerManager.Get<ILogManager>(), WebContainerManager.Get<IUserSession>())
	{
	}
	public UserAuditAttribute(ILogManager logManager, IUserSession userSession)
	{
		_userSession = userSession;
		_log = logManager.GetLog(typeof (UserAuditAttribute));
	}
	public override bool AllowMultiple
	{
		get { return false; }
	}
	
	public override Task OnActionExecutingAsync(HttpActionContext actionContext,
	CancellationToken cancellationToken)
	{
		_log.Debug("Starting execution...");
		var userName = _userSession.Username;
		return Task.Run(() => AuditCurrentUser(userName), cancellationToken);
	}
	
	public void AuditCurrentUser(string username)
	{
		// Simulate long auditing process
		_log.InfoFormat("Action being executed by user={0}", username);
		Thread.Sleep(3000);
	}
	public override void OnActionExecuted(HttpActionExecutedContext actionExecutedContext)
	{
		_log.InfoFormat("Action executed by user={0}", _userSession.Username);
	}
}
```


```cs
[HttpPost]
[UserAudit]
[Route("tasks/{taskId:long}/reactivations", Name = "ReactivateTaskRoute")]
public Task ReactivateTask(long taskId)
{
	var task = _reactivateTaskWorkflowProcessor.ReactivateTask(taskId);
	return task;
}
```

## Understanding Parameter and Model Binding

```cs
[HttpGet]
[HttpPost]
public int SumNumbers(int first, int second) {
	return first + second;
}

//Using a Model Class - Refer: Numbers.cs
[HttpGet]
[HttpPost]
public int SumNumbers(Numbers calc) {
	return calc.First + calc.Second;
}

//Adding an Action Method Parameter - refer: Operation.cs
[HttpGet]
[HttpPost]
public int SumNumbers(Numbers calc, Operation op) {
	int result = op.Add ? calc.First + calc.Second : calc.First - calc.Second;
	return op.Double ? result * 2 : result;
}

//Getting Values for a Complex Type from the Request URL
[HttpGet]
[HttpPost]
public int SumNumbers([FromUri] Numbers calc, [FromUri] Operation op) {
	int result = op.Add ? calc.First + calc.Second : calc.First - calc.Second;
	return op.Double ? result * 2 : result;
}

//Using the FromBody Attribute
[HttpGet]
[HttpPost]
public int SumNumbers([FromBody] int number) {
	return number * 2;
}


//Defining a Binding Rule in the WebApiConfig.cs File
config.ParameterBindingRules.Insert(0, typeof(Numbers), x => x.BindWithAttribute(new FromUriAttribute()));


//Numbers.cs
public class Numbers {
	public int First { get; set; }
	public int Second { get; set; }
}

//Operation.cs
public class Operation {
	public bool Add { get; set; }
	public bool Double { get; set; }
}
```

## Message Handlers

### Registering the Message Handlers
```cs
public static class WebApiConfig
{
	public static void Register(HttpConfiguration config)
	{
		config.MessageHandlers.Add(new MyImportantHandler());
		config.MessageHandlers.Add(new MyNotSoImportantHandler());
	}
}
```


### Registering the Per-Route Handlers
```cs
public static class WebApiConfig
{
	public static void Register(HttpConfiguration config)
	{
		var handler = new MyImportantHandler()
		{
			InnerHandler = new MyNotSoImportantHandler()
			{
				InnerHandler = new HttpControllerDispatcher(config)
			}
		};
		config.Routes.MapHttpRoute(
			name: "premiumApi",
			routeTemplate: "premium/{controller}/{id}",
			defaults: new { id = RouteParameter.Optional },
			constraints: null,
			handler: handler
			);

	}
}
```

### Creating a Controller Selector for Versioning
```cs
using System.Web.Http.Dispatcher;
public class MyControllerSelector : DefaultHttpControllerSelector
{
	public MyControllerSelector(HttpConfiguration configuration) : base(configuration) {}
	public override string GetControllerName(HttpRequestMessage request)
	{
		string controllerName = base.GetControllerName(request);
		
		// Having controllers like EmployeesV2Controller or EmployeesV3Controller is
		// our internal business. A client must not make a request directly like /api/employeesv2.
		int version;
		int length = controllerName.Length;
		if (Int32.TryParse(controllerName.Substring(length - 1, 1), out version))
		{
			if (controllerName.Substring(length - 2, 1).Equals("V", StringComparison.OrdinalIgnoreCase))
			{
				string message = "No HTTP resource was found that matches the request URI {0}";
				throw new HttpResponseException(
				request.CreateErrorResponse(
				HttpStatusCode.NotFound,
				String.Format(message, request.RequestUri)));
			}
		}

		
		// If client requests a specific version through the request header, we entertain it
		if (request.Headers.Contains("X-Version"))
		{
			string headerValue = request.Headers.GetValues("X-Version").First();
			if (!String.IsNullOrEmpty(headerValue) &&
			Int32.TryParse(headerValue, out version))
			{
				controllerName = String.Format("{0}v{1}", controllerName, version);
				HttpControllerDescriptor descriptor = null;
				if (!this.GetControllerMapping().TryGetValue(controllerName, out descriptor))
				{
					string message = "No HTTP resource was found that matches the request URI {0} and version {1}";
					throw new HttpResponseException(
					request.CreateErrorResponse(
					HttpStatusCode.NotFound,
					String.Format(message, request.RequestUri, version)));
				}
			}
		}

		return controllerName;
	}
}

http://localhost:39188/api/employeesv2/1.
```

### HttpMessageHandler Abstract Base Class Implementation
```cs
namespace System.Net.Http
{
	public abstract class HttpMessageHandler : IDisposable
	{
		protected HttpMessageHandler()
		{
			if (Logging.On)
			Logging.Enter(Logging.Http, (object) this, ".ctor", (string) null);
			
			if (!Logging.On)
			return;
			
			Logging.Exit(Logging.Http, (object) this, ".ctor", (string) null);
		}
}
```

### Adding a Custom Response Header
```cs
public class XPoweredByHeaderHandler : DelegatingHandler
{
	const string XPOWEREDBYHEADER = "X-Powered-By";
	const string XPOWEREDBYVALUE = "ASP.NET Web API";
	
	protected override Task<HttpResponseMessage> SendAsync(
		HttpRequestMessage request, CancellationToken cancellationToken)
	{
		return base.SendAsync(request, cancellationToken).ContinueWith(
			(task) =>
			{
				HttpResponseMessage response = task.Result;
				response.Headers.Add(XPOWEREDBYHEADER, XPOWEREDBYVALUE);
				return response;
			}
		);
	}
}

//Registration of Two Custom Message Handlers in Global.asax.cs

public class WebApiApplication : System.Web.HttpApplication
{
	protected void Application_Start()
	{
		RouteConfig.RegisterRoutes(RouteTable.Routes);
		var config = GlobalConfiguration.Configuration;
		config.MessageHandlers.Add(new XHttpMethodOverrideHandler());
		config.MessageHandlers.Add(new XPoweredByHeaderHandler());
	}
}
```

### Per-Route Message Handlers - API Key Message Handler Implementation
```cs
public class ApiKeyProtectionMessageHandler : DelegatingHandler {
	protected override Task<HttpResponseMessage> SendAsync(HttpRequestMessage request,
	CancellationToken cancellationToken) {
		IEnumerable<string> values;
		request.Headers.TryGetValues("apikey", out values);
		
		if (null != values && values.Count() == 1) {
			return base.SendAsync(request, cancellationToken);
		}
		
		var tcs = new TaskCompletionSource<HttpResponseMessage>();
		tcs.SetResult(new HttpResponseMessage(HttpStatusCode.Unauthorized) {
			ReasonPhrase = "API Key required."
		});
		return tcs.Task;
	}
}

routes.MapHttpRoute(
	name: "Secret Api",
	routeTemplate: "secretapi/{controller}/{id}",
	defaults: new {id = RouteParameter.Optional},
	constraints: null,
	handler: new ApiKeyProtectionMessageHandler() {
	InnerHandler =
	new HttpControllerDispatcher(GlobalConfiguration.Configuration)
});
```

## Media Type Formatters
//Product.cs
//Creating a CSV Media Formatter
```cs
public class Product
{
	public int Id { get; set; }
	public string Name { get; set; }
	public string Category { get; set; }
	public decimal Price { get; set; }
}
```


//ProductCsvFormatter.cs
```cs
public class ProductCsvFormatter : BufferedMediaTypeFormatter
{
	public ProductCsvFormatter()
	{
		// Add the supported media type.
		SupportedMediaTypes.Add(new MediaTypeHeaderValue("text/csv"));
		
		//Another example
		SupportedMediaTypes.Add(new MediaTypeHeaderValue("application/x.product"));
		
		//Supporting a Specific Encoding
		SupportedEncodings.Add(new UTF8Encoding(encoderShouldEmitUTF8Identifier: false));
		SupportedEncodings.Add(Encoding.GetEncoding("iso-8859-1"));
		
		//Using a MediaTypeMapping
		MediaTypeMappings.Add(new ProductMediaMapping());
	}
	
	public override bool CanWriteType(System.Type type)
	{
		if (type == typeof(Product))
		{
			return true;
		}
		else
		{
			Type enumerableType = typeof(IEnumerable<Product>);
			return enumerableType.IsAssignableFrom(type);
		}
	}

	public override bool CanReadType(Type type)
	{
		return false;
	}

	public override void WriteToStream(Type type, object value, Stream writeStream, HttpContent content)
	{
		using (var writer = new StreamWriter(writeStream))
		{
			var products = value as IEnumerable<Product>;
			if (products != null)
			{
				foreach (var product in products)
				{
					WriteItem(product, writer);
				}
			}
			else
			{
				var singleProduct = value as Product;
				if (singleProduct == null)
				{
					throw new InvalidOperationException("Cannot serialize type");
				}
				WriteItem(singleProduct, writer);
			}
		}
	}

	//Setting the HTTP Response Headers
	public override void SetDefaultContentHeaders(Type type, 	HttpContentHeaders headers, MediaTypeHeaderValue mediaType) {
		base.SetDefaultContentHeaders(type, headers, mediaType);
			headers.Add("X-ModelType", 	type == typeof(IEnumerable<Product>) ? "IEnumerable<Product>" : "Product");
			headers.Add("X-MediaType", mediaType.MediaType);
	}

	// Helper methods for serializing Products to CSV format. 
	private void WriteItem(Product product, StreamWriter writer)
	{
		writer.WriteLine("{0},{1},{2},{3}", Escape(product.Id),
			Escape(product.Name), Escape(product.Category), Escape(product.Price));
	}

	static char[] _specialChars = new char[] { ',', '\n', '\r', '"' };

	private string Escape(object o)
	{
		if (o == null)
		{
			return "";
		}
		string field = o.ToString();
		if (field.IndexOfAny(_specialChars) != -1)
		{
			// Delimit the entire field with quotes and replace embedded quotes with "".
			return String.Format("\"{0}\"", field.Replace("\"", "\"\""));
		}
		else return field;
	}
}


```

```cs
//Creating a Media Type Mapping
//ProductMediaMapping.cs
public class ProductMediaMapping : MediaTypeMapping {
	public ProductMediaMapping() : base("application/x.product") {
	}
	
	public override double TryMatchMediaType(HttpRequestMessage request) {
		IEnumerable<string> values;
		return request.Headers.TryGetValues("X-UseProductFormat", out values) && values.Where(x => x == "true").Count() > 0 ? 1 : 0;
	}
}
```

### Changing the Order of the Media Type Formatters
```cs
public static class WebApiConfig {
	public static void Register(HttpConfiguration config) {
		MediaTypeFormatter xmlFormatter = config.Formatters.XmlFormatter;
		config.Formatters.Remove(xmlFormatter);
		config.Formatters.Insert(0, xmlFormatter);
	}
}
```



### Disabling the Match-on-Type Feature
```cs
public static class WebApiConfig {
	public static void Register(HttpConfiguration config) {
		config.Services.Replace(typeof(IContentNegotiator),	new DefaultContentNegotiator(true));
	}
}
```

### Indenting the JSON Data
```cs
public static class WebApiConfig {
	public static void Register(HttpConfiguration config) {
		JsonMediaTypeFormatter jsonFormatter = config.Formatters.JsonFormatter;
		jsonFormatter.Indent = true;
		
		//Enabling the Microsoft Date Format
		jsonFormatter.SerializerSettings.DateFormatHandling = DateFormatHandling.MicrosoftDateFormat;
		
		//Enabling HTML Character Escaping
		jsonFormatter.SerializerSettings.StringEscapeHandling = StringEscapeHandling.EscapeHtml;
		
		//Ignoring Default Values
		jsonFormatter.SerializerSettings.DefaultValueHandling = DefaultValueHandling.Ignore;
	}
}
```

### Registering a New Formatter
```cs
protected void Application_Start(object sender, EventArgs e) {

	//Registering a New Formatter in ASP.NET Web API Configuration
	var config = GlobalConfiguration.Configuration;
	config.Formatters.Add(new PlainTextFormatter());
	
	///Adding a New Formatter at a Specific Position of the MediaTypeFormatterCollection
	config.Formatters.Insert(0, new JsonpMediaTypeFormatter());
	
	//Removing a Formatter
	config.Formatters.Remove(config.Formatters.JsonFormatter);	
	
}
```

### Media Type Mappings
• UriPathExtensionMapping
• QueryStringMapping
• RequestHeaderMapping
	http://localhost:40553/car/1?format=jsonp&callback=jsonp1311664395075


```cs
//Registering a QueryStringMapping Instead of a UriPathExtensionMapping
public JsonpMediaTypeFormatter() { 
	SupportedMediaTypes.Add(DefaultMediaType);
	SupportedMediaTypes.Add(new MediaTypeHeaderValue("text/javascript"));
	MediaTypeMappings.Add(new QueryStringMapping("format", "jsonp", DefaultMediaType));
}

//RequestHeaderMapping
public class Global : HttpApplication {
	protected void Application_Start(object sender, EventArgs e) {
		var config = GlobalConfiguration.Configuration;
		
		config.Formatters.JsonFormatter.MediaTypeMappings.Add(
		new RequestHeaderMapping(
		"Referer",
		"http://localhost:1501/",
		StringComparison.InvariantCultureIgnoreCase,
		false,
		"text/xml"));
		
		
	}
}
```

### Requesting a Content Type through the Query String
```cs
// GET http://localhost:55778/api/employees/12345?frmt=json HTTP/1.1
// GET http://localhost:55778/api/employees/12345?frmt=xml HTTP HTTP/1.1

public static class WebApiConfig
{
	public static void Register(HttpConfiguration config)
	{

		config.Formatters.JsonFormatter.MediaTypeMappings.Add(
			new QueryStringMapping("frmt", "json",
			new MediaTypeHeaderValue("application/json")));

		config.Formatters.XmlFormatter.MediaTypeMappings.Add(
			new QueryStringMapping("frmt", "xml",
			new MediaTypeHeaderValue("application/xml")));
		foreach (var formatter in config.Formatters)
		{
			Trace.WriteLine(formatter.GetType().Name);
			Trace.WriteLine("\tCanReadType: " + formatter.CanReadType(typeof(Employee)));
			Trace.WriteLine("\tCanWriteType: " + formatter.CanWriteType(typeof(Employee)));
			Trace.WriteLine("\tBase: " + formatter.GetType().BaseType.Name);
			Trace.WriteLine("\tMedia Types: " + String.Join(", ", formatter.SupportedMediaTypes));
		}	
	}
}
```

### Requesting a Content Type through the Header 
```cs
config.Formatters.JsonFormatter
	.MediaTypeMappings.Add(
		new RequestHeaderMapping("X-Media", "json",
			StringComparison.OrdinalIgnoreCase, false,
				new MediaTypeHeaderValue("application/json")));
```


## Model Binding
```cs
//Registering the Media Type Formatter & Mapping Methods
//WebApiConfig.cs
//Registering a Media Type Formatter
public static class WebApiConfig {

	//Registering the Media Type Formatter
	public static void Register(HttpConfiguration config) {
		config.Formatters.Add(new ProductFormatter());
	}
	
	//Using Media Type Formatter Mapping Methods in the WebApiConfig.cs File
	MediaTypeFormatter prodFormatter = new ProductFormatter();
	prodFormatter.AddQueryStringMapping("format", "product", "application/x.product");
	prodFormatter.AddRequestHeaderMapping("X-UseProductFormat", "true", StringComparison.InvariantCultureIgnoreCase, false, "application/x.product");
	prodFormatter.AddUriPathExtensionMapping("custom", "application/x.product");
	config.Formatters.Add(prodFormatter);

}
```

### GET Request URI Having Two QueryString Parameters
//http://localhost:1051/api/values/?param1=1& param2=2

public class ValuesController : ApiController {
	public int Get() {
		var param1 = Request.RequestUri.ParseQueryString().Get("param1");
		var param2 = Request.RequestUri.ParseQueryString().Get("param2");
		
		if (!string.IsNullOrEmpty(param1) && !String.IsNullOrEmpty(param2)) {
			return Convert.ToInt32(param1) + Convert.ToInt32(param2);
		}
		throw new HttpResponseException(HttpStatusCode.BadRequest);
	}
}


### SearchController to Perform a Search for Persons’ Names
//http://localhost:1051/api/search/?text=Bill&maxresults=2
public class Search {
	public string Text { get; set; }
	public int MaxResults { get; set; }
}


public IEnumerable<string> Get([FromUri] Search search) {
	return _persons
	.Where(w => w.Contains(search.Text))
	.Take(search.MaxResults);
}

## Input Validation
### Data Annotation Validation Attributes

```cs
using System.ComponentModel.DataAnnotations;

namespace PartyInvites.Models {
    public class GuestResponse {
        [HttpBindNever]
        public int Id { get; set; }
		
        [Required]
        public string Name { get; set; }

        public decimal Price { get; set; }

        [Required]
        public bool? WillAttend { get; set; }
		
		[Required(AllowEmptyStrings = true)]
		public string Make { get; set; }

		[Required]
		[DataMember(IsRequired = true)]
		public int Year { get; set; }

		[Required]
		[StringLength(maximumLength: 20, ErrorMessage = "For {0} field, the maximum allowed length is {1}.")]
		public string Make { get; set; }

		[Required]
		[StringLength(maximumLength: 20, MinimumLength = 5)]
		public string Model { get; set; }

		[Required]
		[StringLength(maximumLength: 20, MinimumLength = 5, ErrorMessageResourceName = "StringLengthAttribute_ValidationErrorIncludingMinimum",
		ErrorMessageResourceType = typeof(ValidationErrors))]
		public string Model { get; set; }

		[Required]
        [Range(1, 100000)]

		[Range(type: typeof(DateTime), minimum: "2010-01-01", maximum: "9999-12-31")]
		public DateTime PurchasedOn { get; set; }

		[RegularExpression("([^\\s]+(\\.(?i)(jpg|png|gif|bmp))$)")]
		public string ImageName { get; set; }

		[EmailAddress]
		public string EmailAddress { get; set; }

		[MinLength(1)]
		[MaxLength(4)]
		public string[] Tags { get; set; }
    }
}
```

```cs

[ValidateModel]
public IHttpActionResult AddTask(HttpRequestMessage requestMessage, GuestResponse gr)
{
    var task = _processor.GuestResponse(gr);
    return result;
}

//registered at the controller level to handle the validation errors and return an informative response to the client
[InvalidModelStateFilter]
public class CarsController : ApiController {
}

```

```cs
protected void Application_Start(object sender, EventArgs e) {
	var config = GlobalConfiguration.Configuration;
	
	//Removing InvalidModelValidatorProvider from the ModelValidatorProvider List
	config.Services.RemoveAll( 
		typeof(ModelValidatorProvider), 
			validator => validator is InvalidModelValidatorProvider);
	
	
	//Removing All Validator Providers Except for DataAnnotationsModelValidatorProvider
	config.Services.RemoveAll(
		typeof(ModelValidatorProvider),
	validator => !(validator is DataAnnotationsModelValidatorProvider));
	
	// Suppressing the IRequiredMemberSelector for all formatters
	foreach (var formatter in config.Formatters) {
		formatter.RequiredMemberSelector = new SuppressedRequiredMemberSelector();
	}
}

```





### Creating Custom Validation Attributes

```cs

[AttributeUsage(AttributeTargets.Property)]
public class GreaterThanAttribute : ValidationAttribute {

	public string OtherProperty { get; private set; }

	public override bool RequiresValidationContext {
		get {
			return true;
		}
	}
	
	public GreaterThanAttribute(string otherProperty) : 
		base(errorMessage: "The {0} field must be greater than the {1} field.") {
		
		if (string.IsNullOrEmpty(otherProperty)) {
			throw new ArgumentNullException("otherProperty");
		}
		OtherProperty = otherProperty;
	}
	
	public override string FormatErrorMessage(string name) {
		return string.Format(
			CultureInfo.CurrentCulture,
			base.ErrorMessageString,
			name,
			OtherProperty);
	}
	
	protected override ValidationResult IsValid(
	object value, ValidationContext validationContext) {
		// Implementation comes here
	}
}



[GreaterThan("SalesStartsAt")]
public DateTime SalesEndsAt { get; set; }

```

### IValidatableObject Custom Validation
```cs


public class Car : IValidatableObject {
	public int Id { get; set; }
	[Required]
	public string Make { get; set; }
	
	public int Year { get; set; }
	
	public float Price { get; set; }
	public IEnumerable<ValidationResult> Validate(
		ValidationContext validationContext) {
	
		if (Year < 2010 && Price > 250000F) {
			yield return new ValidationResult(
				"The Price cannot be above 250000 if the Year value is lower than 2010.", 	new string[] { "Price" });
		}
		
		yield return ValidationResult.Success;
	}
}

```

### Blacklisting Members
```cs
public class Employee
{
	public int Id { get; set; }
	public string FirstName { get; set; }
	public string LastName { get; set; }

	[JsonIgnore] // Ignored only by Json.NET
	public string Title { get; set; }

	[IgnoreDataMember] // Ignored by both Json.NET and DCS
	public string Department { get; set; }
}
```

### Whitelisting Members
```cs
[DataContract]
public class Employee
{
	[DataMember]
	public int Id { get; set; }
	
	public string FirstName { get; set; } // Does not get serialized
	
	[DataMember]
	public string LastName { get; set; }
	
	[DataMember]
	public decimal Compensation
	{
		// Serialized with json.NET but fails with an exception in case of 	80
		// DataContractSerializer, since set method is absent
		get
		{
			return 5000.00M;
		}
	}
}
```

### Controlling Member Names
```cs
//The Employee Class with Member Names Customized for Serialization
public class Employee
{
	[JsonProperty(PropertyName="Identifier")]
	public int Id { get; set; }
	
	public string FirstName { get; set; }
	
	[DataMember(Name="FamilyName")] // No effect unless DataContract used
	public string LastName { get; set; }
}
```


config.Formatters.JsonFormatter.SerializerSettings.Formatting = Formatting.Indented;
config.Formatters.JsonFormatter.SerializerSettings.ContractResolver = new CamelCasePropertyNamesContractResolver();

### Returning Only a Subset of Members
```cs

public HttpResponseMessage Get()
{
	//Id, FirstName
	var values = list.Select(e => new
	{
		Identifier = e.Id, LastName, Compensation, Department
		Name = e.FirstName + " " + e.LastName
	});
	var response = new HttpResponseMessage(HttpStatusCode.OK)
	{
		Content = new ObjectContent(values.GetType(),	values,
			Configuration.Formatters.JsonFormatter)
	};
	return response;
}
```


## Dependency Resolution
```cs
// a tax calculator implementing ITaxCalculator
// using constructor injection
public class TaxCalculator : ITaxCalculator
{
	private readonly ITaxConfiguration _configuration;
	public TaxCalculator(ITaxConfiguration configuration)
	{
		_configuration = configuration;
	}
	// ... rest of the implementation
}

### Validation Using Data Annotations
```cs
public void Post(Employee employee)
{
	if (ModelState.IsValid)
	{
		// Just be happy and do nothing
	}
	else
	{
		var errors = ModelState.Where(e => e.Value.Errors.Count > 0)
		.Select(e => new
		{
			Name = e.Key,
			Message = e.Value.Errors.First().ErrorMessage}).ToList();
		}
	}	
}	
```

### Removal of InvalidModelValidatorProvider
```cs
public static class WebApiConfig
{
	public static void Register(HttpConfiguration config)
	{
		config.Services.RemoveAll(typeof(ModelValidatorProvider),v => v is InvalidModelValidatorProvider);
	}
}
```

### Handling Validation Errors
```cs
//Action filters in the ASP.NET Web API pipeline
public class ValidationErrorHandlerFilterAttribute : ActionFilterAttribute
{
	public override void OnActionExecuting(HttpActionContext actionContext)
	{
		if (!actionContext.ModelState.IsValid)
		{
			actionContext.Response = actionContext.Request.CreateErrorResponse(
				HttpStatusCode.BadRequest, actionContext.ModelState);
		}
	}
}

//configure it as a global filter in the Register method of WebApiConfig in the App_Start folder
config.Filters.Add(new ValidationErrorHandlerFilterAttribute());
```

### Extending an Out-of-the-Box Validation Attribute
```cs
//The MemberRangeAttribute Class
public class MemberRangeAttribute : RangeAttribute
{
	public MemberRangeAttribute(int minimum, int maximum) : base(minimum, maximum) { }
	public override bool IsValid(object value)
	{
		if (value is ICollection)
		{
			var items = (ICollection)value;
			return items.Cast<int>().All(i => IsValid(i));
		}
		else
			return base.IsValid(value);
		}
	}
}
```

### Creating Your Own Validation Attribute
```cs
public class Employee
{
	[Range(10000, 99999)]
	public int Id { get; set; }

	[LimitChecker("AnnualIncome", 75)]
	public decimal Contribution401K { get; set; }
}


public class LimitCheckerAttribute : ValidationAttribute
{
	public LimitCheckerAttribute(string baseProperty, double percentage)
	{
		this.BaseProperty = baseProperty;
		this.Percentage = percentage;
		this.ErrorMessage = "{0} cannot exceed {1}% of {2}";
	}
	
	public string BaseProperty { get; set; }
	public double Percentage { get; set; }
	
	public override string FormatErrorMessage(string name)
	{
		return string.Format(ErrorMessageString, name, this.Percentage, BaseProperty);
	}
	
	protected override ValidationResult IsValid(object value, ValidationContext validationContext)
	{
		decimal amount = (decimal)value;
		var propertyInfo = validationContext
		.ObjectType
		.GetProperty(this.BaseProperty);
		
		if (propertyInfo != null)
		{
			decimal baseAmount = (decimal)propertyInfo.GetValue(
			validationContext.ObjectInstance, null);
			decimal maxLimit = baseAmount * (decimal)this.Percentage / 100;
			if(amount <= maxLimit)
				return ValidationResult.Success;
			}
		return new ValidationResult(FormatErrorMessage(validationContext.DisplayName));
	}
}
```

### Implementing the IValidatableObject Interface
```cs
```


// registering ITaxCalculator in AutoFac
var builder = new ContainerBuilder();
builder.RegisterType<TaxCalculator>().As<ITaxCalculator>();
var container = builder.Build(); // 2-stage DI exclusive to AutoFac


Service Locator
// Service Locator pattern in AutoFac
var taxCalculator = container.Resolve<ITaxCalculator>();
```
## Testing

```cs
[TestClass]
public class EmployeesControllerTest
{
	[TestMethod]
	public void MustReturnEmployeeForGetUsingAValidId()
	{
		// Arrange
		// Act
		// Assert
	}
}


[TestClass]
public class EmployeesControllerTest
{
	[TestMethod]
	public void MustReturnEmployeeForGetUsingAValidId()
	{
		// Arrange
		int id = 12345;
		var employee = new Employee()
		{
		Id = id, FirstName = "John", LastName = "Human"
		};
		
		IRepository<Employee> repository = MockRepository
		.GenerateMock<IRepository<Employee>>();
		repository.Stub(x => x.Find(id)).Return(employee);
		IUnitOfWork uow = MockRepository.GenerateMock<IUnitOfWork>();
		Mapper.CreateMap<Employee, EmployeeDto>();
		var controller = new EmployeesController(uow, repository, Mapper.Engine);
		controller.EnsureNotNull();
		
		// Act
		// Assert
	}
}


public void MustReturnEmployeeForGetUsingAValidId()
{
	// Arrange
	// Code from the previous steps
	// Act
	HttpResponseMessage response = controller.Get(id);
	
	// Assert
	Assert.IsNotNull(response);
	Assert.IsNotNull(response.Content);
	Assert.IsInstanceOfType(response.Content, typeof(ObjectContent<EmployeeDto>));
	Assert.AreEqual(HttpStatusCode.OK, response.StatusCode);
	var content = (response.Content as ObjectContent<EmployeeDto>);
	var result = content.Value as EmployeeDto;
	Assert.AreEqual(employee.Id, result.Id);
	Assert.AreEqual(employee.FirstName, result.FirstName);
	Assert.AreEqual(employee.LastName, result.LastName);
}

[TestMethod]
public void MustReturn201AndLinkForPost()
{
	// Arrange
	int id = 12345;
	var employeeDto = new EmployeeDto() { Id = id, FirstName = "John", LastName = "Human" };
	string requestUri = "http://localhost:8086/api/employees/";
	Uri uriForNewEmployee = new Uri(new Uri(requestUri), id.ToString());
	IRepository<Employee> repository = MockRepository.GenerateMock<IRepository<Employee>>();
	repository.Expect(x => x.Insert(null)).IgnoreArguments().Repeat.Once();
	IUnitOfWork uow = MockRepository.GenerateMock<IUnitOfWork>();
	uow.Expect(x => x.Save()).Return(1).Repeat.Once();
	Mapper.CreateMap<EmployeeDto, Employee>();
	var controller = new EmployeesController(uow, repository, Mapper.Engine);
	controller.SetRequest("employees", HttpMethod.Post, requestUri);
	
	// Act
	HttpResponseMessage response = controller.Post(employeeDto);
	
	// Assert
	repository.VerifyAllExpectations();
	uow.VerifyAllExpectations();
	Assert.AreEqual(HttpStatusCode.Created, response.StatusCode);
	Assert.AreEqual(uriForNewEmployee, response.Headers.Location);
}
```
### Testing Actions Not Dependent on the Controller
```cs
[Fact]
public void GetAll_should_return_all_from_OrderService()
{
	// arrange
	var orders = new Order[0];
	var mockOrderService = new Mock<IOrderService>();
	mockOrderService.Setup(x => x.GetAll())
	.Returns(orders);
	var orderController = new OrderController(mockOrderService.Object);
	// act
	var result = orderController.Get();
	// assert
	Assert.Equal(orders, result);
}
```

### Testing Getting an Existing Order Without Preparing the Request Context (Causes Exception)
```cs
[Fact]
public void Get_should_return_OK_if_order_exists()
{
	// arrange
	const int OrderId = 123;
	var order = new Order()
	{
		Id = OrderId
	};
	var mockOrderService = new Mock<IOrderService>();
	mockOrderService.Setup(x => x.Exists(It.IsAny<int>()))
	.Returns(true);
	mockOrderService.Setup(x => x.Get(It.IsAny<int>()))
	.Returns(order);
	
	var orderController = new OrderController(mockOrderService.Object);
	// act
	var result = orderController.Get(new HttpRequestMessage(), OrderId);
	// assert
	Assert.Equal(HttpStatusCode.OK, result.StatusCode);
}
```

### Testing Getting a Nonexisting Order
```cs
[Fact]
public void Get_should_return_NotFound_if_order_DoesNotExistS()
{
	// arrange
	const int OrderId = 123;
	var mockOrderService = new Mock<IOrderService>();
	mockOrderService.Setup(x => x.Exists(It.IsAny<int>()))
	.Returns(false);
	var orderController = new OrderController(mockOrderService.Object);
	var request = new HttpRequestMessage();
	request.Properties[HttpPropertyKeys.HttpConfigurationKey] = new HttpConfiguration();
	// act
	var result = orderController.Get(request, OrderId);
	// assert
	Assert.Equal(HttpStatusCode.NotFound, result.StatusCode);
}
```

### Testing HTTP Status Code for a Valid Order Without Preparing Controller Contex
```cs
[Fact]
public void Post_should_return_Created_if_order_good()
{
	// arrange
	const int OrderId = 123;
	var order = new Order(new OrderItem[]
		{
			new OrderItem()
				{
					Name = "Name",
					Quantity = 1
				}
			})
		{
			Id = OrderId
		};
		
	var mockOrderService = new Mock<IOrderService>();
	mockOrderService.Setup(x => x.Exists(It.IsAny<int>()))
	.Returns(false);
	
	var orderController = new OrderController(mockOrderService.Object);
	var request = new HttpRequestMessage();
	
	request.Properties[HttpPropertyKeys.HttpConfigurationKey] = new HttpConfiguration();
	// act
	var result = orderController.Post(request, order);
	// assert
	Assert.Equal(HttpStatusCode.Created, result.StatusCode);
}
```

### Testing HTTP Status Code for a Valid Order Without Preparing Controller Context
```cs
[Fact]
public void Post_should_return_Created_if_order_good()
{
	// arrange
	const int OrderId = 123;
	var order = new Order(new OrderItem[]
			{
				new OrderItem()
					{
						Name = "Name",
						Quantity = 1
					}
				})
		{
			Id = OrderId
		};
		
	var mockOrderService = new Mock<IOrderService>();
	mockOrderService.Setup(x => x.Exists(It.IsAny<int>()))
	.Returns(false);
	var orderController = new OrderController(mockOrderService.Object);
	var request = new HttpRequestMessage(HttpMethod.Post, "http://localhost:2345/api/Order/");
	var config = new HttpConfiguration();
	request.Properties[HttpPropertyKeys.HttpConfigurationKey] = config;
	orderController.Request = request;
	orderController.Configuration = config;
	config.Routes.MapHttpRoute("DefaultApi", "api/{controller}/{id}", _
	new {id = RouteParameter.Optional});
	var route = config.Routes["DefaultApi"];
	var httpRouteData = new HttpRouteData(route, new HttpRouteValueDictionary( _
	new {controller = "Order" }));
	orderController.Request.Properties[HttpPropertyKeys.HttpRouteDataKey] = httpRouteData;
	// act
	var result = orderController.Post(request, order);
	// assert
	Assert.Equal(HttpStatusCode.Created, result.StatusCode);
}
```

### Using the Data Builder’s Fluent API to Set Up the Controller Context
```cs
[Fact]
public void Post_should_return_Created_if_order_good_fluentApi()
{
	// arrange
	const int OrderId = 123;
	var order = new Order(new OrderItem[]
			{
				new OrderItem()
					{
						Name = "Name",
						Quantity = 1
					}
				})
		{
		Id = OrderId
		};
	var mockOrderService = new Mock<IOrderService>();
	mockOrderService.Setup(x => x.Exists(It.IsAny<int>()))
	.Returns(false);

	var orderController = ControllerContextSetup
	.Of(() => new OrderController(mockOrderService.Object))
	.WithDefaultConfig()
	.WithDefaultRoute()
	.Requesting("http://localhost:2345/api/Order/")
	.WithRouteData(new {controller="Order"})
	.Build<OrderController>();
	
	// act
	var result = orderController.Post(orderController.Request, order);
	// assert
	Assert.Equal(HttpStatusCode.Created, result.StatusCode);
}
```


### Data-Driven Cases for Testing Routing
```cs
[Theory]
[InlineData("http://localhost:12345/foo/route", "GET", false, null, null)]
[InlineData("http://localhost:12345/api/order/", "GET", true, "order", null)]
[InlineData("http://localhost:12345/api/order/123", "GET", true, "order", "123")]

public void DefaultRoute_Returns_Correct_RouteData(
string url, string method, bool shouldfound, string controller, string id)
{
	// arrange
	var config = new HttpConfiguration();
	WebApiConfig.Register(config);
	var request = new HttpRequestMessage(new HttpMethod(method), url);
	
	// act
	var routeData = config.Routes.GetRouteData(request);
	
	// assert
	Assert.Equal(shouldfound, routeData!=null);
	if (shouldfound)
	{
		Assert.Equal(controller, routeData.Values["controller"]);
		Assert.Equal(id == null ? (object) RouteParameter.Optional : (object)id, routeData.	Values["id"]);
	}
}
```

### Testing Controller and Action Selection
```cs
//Data-Driven Cases for Checking Controller and Action Selection
[Theory]
[InlineData("http://localhost:12345/api/order/123", "GET", typeof(OrderController), "Get")]
[InlineData("http://localhost:12345/api/order", "POST", typeof(OrderController), "Post")]
[InlineData("http://localhost:12345/api/order/123", "PUT", typeof(OrderController), "Put")]
[InlineData("http://localhost:12345/api/order", "GET", typeof(OrderController), "Get")]
[InlineData("http://localhost:12345/api/order/123/OrderItem", "GET", typeof(OrderItemController),
"GetItems")]
public void Ensure_Correct_Controller_and_Action_Selected(
string url,
string method,
Type controllerType,
string actionName)
{
	// arrange
	var config = new HttpConfiguration();
	WebApiConfig.Register(config);
	var actionSelector = config.Services.GetActionSelector();
	var controllerSelector = config.Services.GetHttpControllerSelector();
	var request = new HttpRequestMessage(new HttpMethod(method), url);
	var routeData = config.Routes.GetRouteData(request);
	request.Properties[HttpPropertyKeys.HttpRouteDataKey] = routeData;
	request.Properties[HttpPropertyKeys.HttpConfigurationKey] = config;
	
	// act
	var controllerDescriptor = controllerSelector.SelectController(request);
	var context = new HttpControllerContext(config, routeData, request)
	{
		ControllerDescriptor = controllerDescriptor
	};
	
	var actionDescriptor = actionSelector.SelectAction(context);
	// assert
	Assert.Equal(controllerType, controllerDescriptor.ControllerType);
	Assert.Equal(actionName, actionDescriptor.ActionName);
}
```

### Testing Filters
```cs
//ValidateModelStateAttribute Filter
[AttributeUsage( AttributeTargets.Class | AttributeTargets.Method,
AllowMultiple = false, Inherited = true)]
public class ValidateModelStateAttribute : ActionFilterAttribute {
	public override void OnActionExecuting(
		HttpActionContext actionContext) {
		
	if (!actionContext.ModelState.IsValid) {
		actionContext.Response =
		actionContext.Request.CreateErrorResponse(
			HttpStatusCode.BadRequest,
			actionContext.ModelState);
		}
	}
}

//Testing ValidateModelStateAttribute Filter

[Fact]
public void Should_Return_BadRequest_If_ModelState_Invalid()
{
	// arrange
	var filter = new ValidateModelStateAttribute();
	var context = new HttpActionContext(
		new HttpControllerContext(new HttpConfiguration(),
			new HttpRouteData(new HttpRoute("SomePattern")),
			new HttpRequestMessage()),
			new ReflectedHttpActionDescriptor());
	
	context.ModelState.AddModelError("foo", "some error");
	
	// act
	filter.OnActionExecuting(context);
	
	// assert
	Assert.NotNull(context.Response);
	Assert.Equal(HttpStatusCode.BadRequest, context.Response.StatusCode);
}
```

### Integration Testing
```cs
//Writing Multiple Assertions in SubSpec

[Specification]
public void GetAll_should_return_all_from_OrderService_Subspec()
{
	var orders = default(Order[]);
	var mockOrderService = default(Mock<IOrderService>);
	var orderController = default(OrderController);
	var result = default(IEnumerable<Order>);
	
	"Given order service contains no orders"
		.Context(() =>
			{
				orders = new Order[0];
				mockOrderService = new Mock<IOrderService>();
				orderController = new OrderController(mockOrderService.Object);
				mockOrderService.Setup(x => x.GetAll())
					.Returns(orders);
			});
	
	"When I ask for all orders from orderController"
		.Do(() =>
			{
				result = orderController.Get();
			});
	
	"Then it must not be null"
		.Observation(() =>
			{
				Assert.NotNull(result);
			});
	"And it should contain no order"
		.Observation(() =>
			{
				Assert.Empty(result);
			});
}
```
## Optimization and Performance
## Hosting
### Self-Hosting ASP.NET Web API

```cs
//http://localhost:8086/api/employees/1

using System;
using System.Web.Http.SelfHost;
using Robusta.TalentManager.WebApi.Core.Configuration;
class Program
{
	static void Main(string[] args)
	{
		var configuration = new HttpSelfHostConfiguration("http://localhost:8086");
		WebApiConfig.Register(configuration);
		DtoMapperConfig.CreateMaps();
		IocConfig.RegisterDependencyResolver(configuration);
		using (HttpSelfHostServer server = new HttpSelfHostServer(configuration))
		{
			server.OpenAsync().Wait();
			Console.WriteLine("Press Enter to terminate the server...");
			Console.ReadLine();
		}
	}
}
```

### In-Memory Hosting ASP.NET Web API
```cs
[Authorize]
public HttpResponseMessage Get(int id)
{
	var employee = repository.Find(id);
	if (employee == null)
	{
		var response = Request.CreateResponse(HttpStatusCode.NotFound, "Employee not found");
		throw new HttpResponseException(response);
	}
	
	return Request.CreateResponse<EmployeeDto>(
	HttpStatusCode.OK,
	mapper.Map<Employee, EmployeeDto>(employee));
}
```


## Filters
### SayHelloAttribute
```cs
//Registering a Global Filter in the WebApiConfig.cs File
public static class WebApiConfig {
	public static void Register(HttpConfiguration config) {
		config.Filters.Add(new SayHelloAttribute { Message = "Global Filter" });
	}
}

//SayHelloAttribute
using System.Web.Http.Filters;

namespace Dispatch.Infrastructure {
	public class SayHelloAttribute : ActionFilterAttribute {
		public string Message { get; set; }
		
		public override Task OnActionExecutingAsync(HttpActionContext actionContext, CancellationToken cancellationToken) {
			Debug.WriteLine("SayHello: {0}", (object)Message ?? "Hello");
			return Task.FromResult<object>(null);
		}
	}
}


### Appling the Authorization Filter
namespace Dispatch.Controllers {
	[Time]
	public class ProductsController : ApiController {

		[CustomAuthentication]
		[CustomAuthorization("admins")]
		public Product Get(int id) {
			return products.Where(x => x.ProductID == id).FirstOrDefault();
		}
	}
}	
	
	
### Creating an Exception Filter
public class CustomExceptionAttribute : Attribute, IExceptionFilter {
	public Task ExecuteExceptionFilterAsync(HttpActionExecutedContext actionExecutedContext, CancellationToken cancellationToken) {
		if (actionExecutedContext.Exception != null && actionExecutedContext.Exception is ArgumentOutOfRangeException) {
			actionExecutedContext.Response = actionExecutedContext.Request.CreateErrorResponse( HttpStatusCode.BadRequest, "No data item");
		}
	
		return Task.FromResult<object>(null);
	}

	public bool AllowMultiple {
		get { return true; }
	}
}
```

### AuthorizeAttribute
```cs
GlobalConfiguration.Configuration.Filters.Add( new AuthorizeAttribute());

public class AuthController : ApiController {
	//Lines omitted for brevity
	[AllowAnonymous]
	public HttpResponseMessage Post(User user) {
		//Lines omitted for brevity
	}
}
```



### SecondaryLoggerAttribute Implementation
```cs
public class SecondaryLoggerAttribute : ActionFilterAttribute {
	private const string _loggerName = "SecondaryLogger";
	
	public override void OnActionExecuting(
		HttpActionContext actionContext) {
		
		var controllerCtx = actionContext.ControllerContext;
		
		LoggerUtil.WriteLog(
		_loggerName,
		"OnActionExecuting",
		controllerCtx.ControllerDescriptor.ControllerName,
		actionContext.ActionDescriptor.ActionName
		);
	}
	
	public override void OnActionExecuted(
		HttpActionExecutedContext actionExecutedContext) {
		
		var actionCtx = actionExecutedContext.ActionContext;
		
		var controllerCtx = actionCtx.ControllerContext;
		LoggerUtil.WriteLog(
		_loggerName,
		"OnActionExecuted",
		controllerCtx.ControllerDescriptor.ControllerName,
		actionCtx.ActionDescriptor.ActionName
		);
	}
}

[Logger]
public class CarsController : ApiController {
	[SecondaryLogger]
	public string[] GetCars() {
		return new string[] {
		"Car 1",
		"Car 2",
		"Car 3",
		"Car 4"
		};
	}
}
```

### logging functionality inside every controller action by passing 
```cs
//a relevant parameter to the private log method
namespace Overview.Filters {
	[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method)]
	public class LoggerAttribute : Attribute, IActionFilter {
		public Task<HttpResponseMessage> ExecuteActionFilterAsync(
		HttpActionContext actionContext,
		CancellationToken cancellationToken,
		Func<Task<HttpResponseMessage>> continuation) {
		
		var controllerCtx = actionContext.ControllerContext;
		Trace.TraceInformation(
			"Controller {0}, Action {1} is running...",
			controllerCtx.ControllerDescriptor.ControllerName,
			actionContext.ActionDescriptor.ActionName
		);
		
		//the way of saying everything is OK
		return continuation();
		}
		
		public bool AllowMultiple {
			get {
				return false;
			}
		}
	}
}

//Registering LoggerAttribute as a Global Filter
protected void Application_Start(object sender, EventArgs e) {
	GlobalConfiguration.Configuration.Filters.Add(new LoggerAttribute());
}

```


## Error Handling
```cs
//Applying the HttpResponseException
[LogErrors]
public Product Get(int id) {
	Product product = products.Where(x => x.ProductID == id).FirstOrDefault();
		if (product == null) {
			throw new HttpResponseException(HttpStatusCode.BadRequest);
		}
	return product;
}


//Using an Implementation of the IHttpActionResult Interface
[LogErrors]
public IHttpActionResult Get(int id) {
	Product product = products.Where(x => x.ProductID == id).FirstOrDefault();
		if (product == null) {
			return BadRequest("No such data object");
		}
	return Ok(product);
}


//Creating an Error Response
[LogErrors]
public HttpResponseMessage Get(int id) {
	Product product = products.Where(x => x.ProductID == id).FirstOrDefault();
	if (product == null) {
		return Request.CreateErrorResponse(HttpStatusCode.BadRequest, new HttpError {
			Message = "No such data item",
			MessageDetail = string.Format("No item ID {0} was found", id)
		});
	}
	return Request.CreateResponse(product);
}


//Adding Extra Error Information
[LogErrors]
public HttpResponseMessage Get(int id) {
	Product product = products.Where(x => x.ProductID == id).FirstOrDefault();
	if (product == null) {
		HttpError error = new HttpError();
		error.Message = "No such data item";
		error.Add("RequestID", id);
		error.Add("AvailbleIDs", products.Select(x => x.ProductID));
		return Request.CreateErrorResponse(HttpStatusCode.BadRequest, error);
	}
	return Request.CreateResponse(product);
}

//Adding Model State Data to the Error
public HttpResponseMessage Post(Product product) {
	if (!ModelState.IsValid) {
		HttpError error = new HttpError(ModelState, false);
		error.Message = "Cannot Add Product";
		error.Add("AvailbleIDs", products.Select(x => x.ProductID));
		return Request.CreateErrorResponse(HttpStatusCode.BadRequest, error);
	}
	product.ProductID = products.Count + 1;
	products.Add(product);

	return Request.CreateResponse(product);
}


public static class WebApiConfig {
public static void Register(HttpConfiguration config) {
	//Setting the Exception Detail Policy
	config.IncludeErrorDetailPolicy = IncludeErrorDetailPolicy.Never;
	
	//Registering a Global Exception Handler
	config.Services.Replace(typeof(IExceptionHandler), new CustomExceptionHandler());
	
	//Registering a Custom Global Exception Logger
	config.Services.Add(typeof(IExceptionLogger), new CustomExceptionLogger());
}


//Throwing Exceptions
[LogErrors]
public Product Get(int id) {
	Product product = products.Where(x => x.ProductID == id).FirstOrDefault();
	if (product == null) {
		throw new ArgumentOutOfRangeException("id");
	}
		return product;
}
```
## Tracing and Logging
## API Documentation

Web API Architecture And Dependency Injection Best Practices
http://www.c-sharpcorner.com/article/web-api-architecture-and-dependency-injection-best-practices/

## Useful URL
* [HTTP Message Lifecycle](http://www.asp.net/media/4071077/aspnet-web-api-poster.pdf)
* [Intro to Application Pools in IIS](http://geekswithblogs.net/JeremyMorgan/archive/2016/07/09/introduction-to-application-pools-in-iis.aspx)
* [Securing ASP.NET Web API](http://code.tutsplus.com/tutorials/securing-aspnet-web-api--cms-26012)
