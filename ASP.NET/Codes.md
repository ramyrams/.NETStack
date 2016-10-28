
# ASP.NET

## TOC
* [ASP.NET - Directives](#aspnet---directives)
* [ASP.NET Configuration]()
* [Controllers](controllers)
* [Views](views)
* [Models](models)
* [Forms and HTML Helpers](forms-and-html-elpers)
* [Data Annotations and Validation](data-annotations-and-validation)
* [Routing](routing)
* [Ajax](ajax)
* [Dependency Injection](dependency-injection)
* [Extending MVC](extending-mvc)
* [Unit Testing](unit-testing)
* [Modules](modules)
* [Handlers](handlers)
* [Detecting Device Capabilities](detecting-device-capabilities)
* [Tracing](tracing)
* [Configuration](configuration)
* [State Data](state-data)
* [Caching Data](caching data)
* [Caching Content](caching-content)
* [ASP.NET Identity](asp.net-identity)


# ASP.NET - Directives
* @Application 	
* @Assembly 		
* @Control 		
* @Implements 		
* @Import 			
* @Master 			
* @MasterType 		
* @OutputCache 	
* @Page 			
* @PreviousPageType
* @Reference  		
* @Register 		

```asp.net
<%@ Application Language="C#" %>

<%@ Assembly Name="MyAssembly"%>
<%@ Assembly src="MYAssembly.cs">

<%@ Control Language="C#" EnableViewState="false" Explicit="True" CodeFile="WebUserControl.ascx.cs" Inherits="WebUserControl" %>

<%@ Implements Interface="System.Web.UI.IValidator"%>

<%@ Import Namespace="System.Data"%>
<%@ Import Namespace="Peter.Toybox" %>

<%@ Master Language="C#" AutoEventWIreup="false" CodeFile="MasterPage1.master.cs" Inherits="MasterPage"%>

<%@ MasterType VirtualPath="/MasterPage1.master"%>

<%@ OutputCache Duration ="180" VaryByParam="None"%>
<%@ OutputCache Duration="10" VaryByParam="location;count" %>

<%@ Page Language="C#" Explicit="true" AutoEventWIreup="false" buffer="true" runat="server" CodeFile="Default.aspx.cs" Trace="true" Inherits="_Default"%>


<%@ PreviousPageType VirtualPath="~/SourcePage.aspx"%>
<%@ Reference  Page ="somepage.aspx" VirtualPath="~/MyControl.ascx"%>

<%@ Register TagPrefix="MayTag Namespace="MyName.MyNameSpace" Assembly="MyAssembly"%>
<%@ Register TagPrefix="OurTag" Tagname="Header" Src="header.ascx"%>
<%@ Register  tagprefix="custom" namespace="Mycompany.namespace" assembly="Mycompany.namespace.control, Version=1.2.3.4,        PublicKeyToken=12345678abcdefgh, Culture=neutral"  %>

```




# ASP.NET Configuration
```cs
ConfigurationSettings.AppSettings("Emailto");
```

```xml

<configuration>
	<system.web>
		<browserCaps provider="Samples.CustomProvider, Samples" />
	</system.web>

	<appSettings>
		<add key="Emailto" value="me@microsoft.com" />
		<add key="cssFile" value="CSS/text.css" />
	</appSettings>
	
	<appSettings file="myfile.config" />

</configuration>

<connectionStrings>
	<add name="NWind" connectionString="SERVER=...;DATABASE=...;UID=...;PWD=...;" providerName="System.Data.SqlClient" />
</connectionStrings>

<authentication mode="None"/>
<authentication mode="Windows"/>

<authentication mode="Forms">
  <forms name="Form" loginUrl="index.asp" />
</authentication>

<authentication mode="Passport">
  <passport redirectUrl="internal" />
</authentication>


<authorization>
	<allow users="comma-separated list of users" roles="comma-separated list of roles" 	verbs="comma-separated list of verbs" />
	<deny users="comma-separated list of users" roles="comma-separated list of roles" 	verbs="comma-separated list of verbs" />
</authorization>

<identity impersonate="false" userName="domain\username" password="password" />


<customErrors defaultRedirect="Errors/appGenericError.aspx" mode="On">
  <error statusCode="403" redirect="/accesdenied.html" />
  <error statusCode="404" redirect="/pagenotfound.html" />
  <error statusCode="500" redirect="Errors/internal.aspx" />
</customErrors>


<error statusCode="403" redirect="/accesdenied.html" />
<error statusCode="404" redirect="/pagenotfound.html" />

<globalization requestEncoding="utf-8" responseEncoding="utf-8" />

<httpRuntime appRequestQueueLimit="50" executionTimeout="300" />

<trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" locaOnly="true" />

<sessionState mode="Off" 
     cookieless="true" 
     timeout="100" 
     stateConnectionString="tcpip=server:port" 
     sqlConnectionString="sql connection string"
     stateNetworkTimeout="number of seconds"/>

<cache disableMemoryCollection = "false" disableExpiration = "false" privateBytesLimit = "0" percentagePhysicalMemoryUsedLimit = "89" privateBytesPollTime = "00:02:00" />

<outputCache defaultProvider="AspNetInternalProvider" enableOutputCache = "true" enableKernelCacheForVaryByStar = "false" enableFragmentCache = "true"
sendCacheControlHeader = "true" omitVaryStar = "false">
</outputCache>

<outputCacheSettings>
	<outputCacheProfiles>
		<add name="ServerOnly" 	duration="60" 	varyByCustom="browser" />
	</outputCacheProfiles>
</outputCacheSettings>

<sqlCacheDependency enabled="true" pollTime="1000">
	<databases>
		<add name="Northwind" connectionStringName="LocalNWind" />
	</databases>
</sqlCacheDependency>

<deployment retail="true" />

<healthMonitoring enabled="true|false" heartbeatInterval="HH:MM:SS">
	<bufferModes>...</bufferModes>
	<providers>...</providers>
	<eventMappings>...</eventMappings>
	<profiles>...</profiles>
	<rules>...</rules>
</healthMonitoring>

<hostingEnvironment idleTimeout="HH:MM:SS" shadowCopyBinAssemblies="true|false" shutdownTimeout="number" urlMetadataSlidingExpiration="HH:MM:SS" />

<httpCookies domain="string" httpOnlyCookies="true|false" requireSSL="true|false" />

<identity impersonate="true" />

<machineKey validationKey="AutoGenerate,IsolateApps" decryptionKey="AutoGenerate,IsolateApps" validation="HMACSHA256" decryption="Auto" />

<membership>
	<providers>
		<add name="MyProvider" type="Samples.MyMembershipProvider" 		connectionStringName="MyConnString" 		enablePasswordRetrieval="false" 		enablePasswordReset="true"
		requiresQuestionAndAnswer="true" passwordFormat="Hashed" />
		...
	</providers>
</membership>

<pages>
	<controls>...</controls>
	<namespaces>...</namespaces>
	<tagMapping>...</tagMapping>
	<ignoreDeviceFilters>...</ignoreDeviceFilters>
</pages>


<pages>
	<tagMapping>
		<add tagType="System.Web.UI.WebControls.TextBox" mappedTagType=	"Samples.MyTextBox" />
	</tagMapping>
</pages>


<ignoreDeviceFilters>
	<filter add="sys" />	
</ignoreDeviceFilters>

<processModel autoConfig="true"/>


<profile>
	<properties>
		<add name="BackColor" type="string" />
		<add name="ForeColor" type="string" />
	</properties>
</profile>


<roleManager
	cacheRolesInCookie="true|false"
	cookieName="name"
	cookiePath="/"
	cookieProtection="All|Encryption|Validation|None"
	cookieRequireSSL="true|false "
	cookieSlidingExpiration="true|false "
	cookieTimeout="number of minutes"
	createPersistentCookie="true|false"
	defaultProvider="provider name"
	domain="cookie domain">
	enabled="true|false"
	maxCachedResults="maximum number of role names cached"
	<providers>...</providers>
</roleManager>


<securityPolicy>
	<trustLevel name="Full" policyFile="internal" />
	<trustLevel name="High" policyFile="web_hightrust.config" />
	<trustLevel name="Medium" policyFile="web_mediumtrust.config" />
	<trustLevel name="Low" policyFile="web_lowtrust.config" />
	<trustLevel name="Minimal" policyFile="web_minimaltrust.config" />
</securityPolicy>


<sitemap enabled="true|false" defaultProvider="provider name">
	<providers>...</providers>
</siteMap>

<trust level="Full" originUrl="" />

<location allowOverride="false">
	<system.web>
		<trust level="Medium" originUrl="" />
	</system.web>
</location>


<urlMappings enabled="true">
	<add url="~/main.aspx" mappedUrl="~/default.aspx?tab=main" />
</urlMappings>

<webControls clientScriptsLocation="/aspnet_client/{0}/{1}/" />


```


```cs
using System.Collections.Generic;
namespace SimpleApp.Models {
	public enum Color {
		Red, Green, Yellow, Purple
	};
	
	class Votes {
		private static Dictionary<Color, int> votes = new Dictionary<Color, int>();
		
		public static void RecordVote(Color color) {
			votes[color] = votes.ContainsKey(color) ? votes[color] + 1 : 1;
		}
		
		public static void ChangeVote(Color newColor, Color oldColor) {
			if (votes.ContainsKey(oldColor)) {
				votes[oldColor]--;
			}	
			RecordVote(newColor);
		}
		
		public static int GetVotes(Color color) {
			return votes.ContainsKey(color) ? votes[color] : 0;
		}
	}
}
```

```cs
namespace SimpleApp.Controllers {
	public class HomeController : Controller {
		public ActionResult Index() {
			return View();
		}
		
		[HttpPost]
		public ActionResult Index(Color color) {
			Color? oldColor = Session["color"] as Color?;
			if (oldColor != null) {
				Votes.ChangeVote(color, (Color)oldColor);
			} else {
				Votes.RecordVote(color);
			}
			ViewBag.SelectedColor = Session["color"] = color;
			return View();
		}
	}
}
```

```aspx
@using SimpleApp.Models
@{ Layout = null; }
<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width" />
<title>Vote</title>
</head>
<body>
@if (ViewBag.SelectedColor == null) {
<h4>Vote for your favorite color</h4>
} else {
<h4>Change your vote from @ViewBag.SelectedColor</h4>
}
@using (Html.BeginForm()) {
@Html.DropDownList("color",
new SelectList(Enum.GetValues(typeof(Color))), "Choose a Color")
<div>
<button type="submit">Vote</button>
</div>
}
<div>
<h5>Results</h5>
<table>
<tr><th>Color</th><th>Votes</th></tr>
@foreach (Color c in Enum.GetValues(typeof(Color))) {
<tr><td>@c</td><td>@Votes.GetVotes(c)</td></tr>
}
</table>
</div>
</body>
</html>
```


## 
```cs

```


### The Contents of the Global.asax.cs File
```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;
using System.Web.Routing;
namespace SimpleApp {
	public class MvcApplication : System.Web.HttpApplication {
		protected void Application_Start() {
			AreaRegistration.RegisterAllAreas();
			RouteConfig.RegisterRoutes(RouteTable.Routes);
		}
	}
}
```



### Breaking the Debugger in the Global.asax.cs File
```cs

namespace SimpleApp {
	public class MvcApplication : System.Web.HttpApplication {
		protected void Application_Start() {
			AreaRegistration.RegisterAllAreas();
			RouteConfig.RegisterRoutes(RouteTable.Routes);
			System.Diagnostics.Debugger.Break();
		}
		
		protected void Application_End() {
			System.Diagnostics.Debugger.Break();
		}
	}
}

```

### Handling Request life-Cycle Events in the Global.asax.cs File
```cs
namespace SimpleApp {
	public class MvcApplication : System.Web.HttpApplication {
		protected void Application_Start() {
			AreaRegistration.RegisterAllAreas();
			RouteConfig.RegisterRoutes(RouteTable.Routes);
		}
		
		protected void Application_BeginRequest() {
			RecordEvent("BeginRequest");
		}
		
		protected void Application_AuthenticateRequest() {
			RecordEvent("AuthenticateRequest");
		}
		
		protected void Application_PostAuthenticateRequest() {
			RecordEvent("PostAuthenticateRequest");
		}
		
		private void RecordEvent(string name) {
			List<string> eventList = Application["events"] as List<string>;
			if (eventList == null) {
				Application["events"] = eventList = new List<string>();
			}
			eventList.Add(name);
		}
	}
}
```


### Displaying the Event Information
```cs
public class HomeController : Controller {
	public ActionResult Index() {
		return View(HttpContext.Application["events"]);
	}
}
```

```aspx
<div class="panel panel-primary">
	<h5 class="panel-heading">Events</h5>
	<table class="table table-condensed table-striped">
		@foreach (string eventName in Model) {
		<tr><td>@eventName</td></tr>
	}
	</table>
</div>
```

### Using C# Events in the Global.asax.cs File
```cs
namespace SimpleApp {
	public class MvcApplication : System.Web.HttpApplication {
	
		public MvcApplication() {
			PostAcquireRequestState += (src, args) => CreateTimeStamp();
		}
		
		protected void Application_Start() {
			AreaRegistration.RegisterAllAreas();
			RouteConfig.RegisterRoutes(RouteTable.Routes);
			CreateTimeStamp();
		}
		
		private void CreateTimeStamp() {
			string stamp = Context.Timestamp.ToLongTimeString();
			if (Session != null) {
				Session["request_timestamp"] = stamp;
			} else {
				Application["app_timestamp"] = stamp;
			}
		}
	}
}
```


```cs
namespace SimpleApp.Controllers {
	public class HomeController : Controller {
		public ActionResult Index() {
			return View(GetTimeStamps());
		}

		private List<string> GetTimeStamps() {
			return new List<string> {
				string.Format("App timestamp: {0}",
					HttpContext.Application["app_timestamp"]),
				string.Format("Request timestamp: {0}", Session["request_timestamp"]),
			};
		}
```

## Module

### ASP.NET Modules		
#### Contents of the TimerModule.cs File
```cs
namespace SimpleApp.Infrastructure {
	public class TimerModule : IHttpModule {
	
		private Stopwatch timer;
	
		//Setting Up the Event Handlers
		public void Init(HttpApplication app) {
			app.BeginRequest += HandleEvent;
			app.EndRequest += HandleEvent;
		}
		
		//Handling the BeginRequest & EndRequest Event
		private void HandleEvent(object src, EventArgs args) {
			HttpContext ctx = HttpContext.Current;
			
			if (ctx.CurrentNotification == RequestNotification.BeginRequest) {
				timer = Stopwatch.StartNew();
			} else {
				ctx.Response.Write(string.Format(
					"<div class='alert alert-success'>Elapsed: {0:F5} seconds</div>",
					((float) timer.ElapsedTicks) / Stopwatch.Frequency));
			}
		}
		
		public void Dispose() {
		// do nothing - no resources to release
		}
	}
}
```		
		
#### Registering a Module	
```xml	
//Registering a Module in the Web.config File
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<system.webServer>
	<modules>
		<add name="Timer" type="SimpleApp.Infrastructure.TimerModule"/>
	</modules>
	</system.webServer>
</configuration>
```

### Creating Self-registering Modules


#### Creating the Module
```cs
namespace CommonModules {
	public class InfoModule : IHttpModule {
	
		public void Init(HttpApplication app) {
			app.EndRequest += (src, args) => {
				HttpContext ctx = HttpContext.Current;
					ctx.Response.Write(string.Format(
						"<div class='alert alert-success'>URL: {0} Status: {1}</div>",
						ctx.Request.RawUrl, ctx.Response.StatusCode));
			};
		}
		public void Dispose() {
			// do nothing - no resources to release
		}
	}
}


#### Creating the Registration Class
```cs
using System.Web;
[assembly: PreApplicationStartMethod(typeof(CommonModules.ModuleRegistration),"RegisterModule")]
namespace CommonModules {
	public class ModuleRegistration {
		public static void RegisterModule() {
			HttpApplication.RegisterModule(typeof(CommonModules.InfoModule));
		}
	}
}
```

### Using Module Events
#### Defining the Module Event

### Understanding the Built-in Modules

## Handler
```cs
//DayOfWeekHandler.cs
namespace SimpleApp.Infrastructure {
	public class DayOfWeekHandler: IHttpHandler {
		public void ProcessRequest(HttpContext context) {
		
			string day = DateTime.Now.DayOfWeek.ToString();
			
			if (context.Request.CurrentExecutionFilePathExtension == ".json") {
				context.Response.ContentType = "application/json";
				context.Response.Write(string.Format("{{\"day\": \"{0}\"}}", day));
			} else {
				context.Response.ContentType = "text/html";
				context.Response.Write(string.Format("<span>It is: {0}</span>", day));
			}
		}
		
		public bool IsReusable {
			get { return false; }
		}
	}
}
```

### Registering a Handler Using URL Routing
```cs
//Setting Up a Route for a Custom Handler in the RouteConfig.cs File
namespace SimpleApp {
	public class RouteConfig {
		public static void RegisterRoutes(RouteCollection routes) {
			routes.IgnoreRoute("{resource}.axd/{*pathInfo}");
			
			routes.Add(new Route("handler/{*path}",
			new CustomRouteHandler {HandlerType = typeof(DayOfWeekHandler)}));
			
			routes.MapRoute(
				name: "Default",
				url: "{controller}/{action}/{id}",
				defaults: new { controller = "Home", action = "Index",
				id = UrlParameter.Optional }
				);
			}
		}
		
	class CustomRouteHandler : IRouteHandler {
		public Type HandlerType { get; set; }
		
		public IHttpHandler GetHttpHandler(RequestContext requestContext) {
			return (IHttpHandler)Activator.CreateInstance(HandlerType);
		}
	}
}
```

### Registering a Handler Using the Configuration File
```cs
//Registering a Handler in the Web.config File
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<system.webServer>
	<handlers>
		<add name="DayJSON" path="/handler/*.json" verb="GET" type="SimpleApp.Infrastructure.DayOfWeekHandler"/>
		<add name="DayHTML" path="/handler/day.html" verb="*" type="SimpleApp.Infrastructure.DayOfWeekHandler"/>
	</handlers>
	</system.webServer>
</configuration>
```

### Ignoring Requests for the Custom handler in the RouteConfig.cs File
```cs
namespace SimpleApp {
	public class RouteConfig {
		public static void RegisterRoutes(RouteCollection routes) {
			routes.IgnoreRoute("{resource}.axd/{*pathInfo}");
			
			//routes.Add(new Route("handler/{*path}",
			// new CustomRouteHandler {HandlerType = typeof(DayOfWeekHandler)}));
			
			routes.IgnoreRoute("handler/{*path}");
			routes.MapRoute(
				name: "Default",
				url: "{controller}/{action}/{id}",
				defaults: new { controller = "Home", action = "Index",
				id = UrlParameter.Optional }
				);
			}
		}
		
		class CustomRouteHandler : IRouteHandler {
			public Type HandlerType { get; set; }
		
			public IHttpHandler GetHttpHandler(RequestContext requestContext) {
				return (IHttpHandler)Activator.CreateInstance(HandlerType);
			}
		}
}
```

### Creating Asynchronous Handlers

```cs
//The Contents of the SiteLengthHandler.cs File
using System.Net.Http;
using System.Threading.Tasks;
using System.Web;
namespace SimpleApp.Infrastructure {
	public class SiteLengthHandler : HttpTaskAsyncHandler {
		public override async Task ProcessRequestAsync(HttpContext context) {
			string data = await new HttpClient().GetStringAsync("http://www.apress.com");
			context.Response.ContentType = "text/html";
			context.Response.Write(string.Format("<span>Length: {0}</span>", data.Length));
		}
	}
}
```

```xml
//Registering the Asynchronous Handler in the Web.config File
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<system.webServer>
		<handlers>
			<add name="SiteLength" path="/handler/site" verb="*" type="SimpleApp.Infrastructure.SiteLengthHandler"/>
		</handlers>
	</system.webServer>
</configuration>
```

### Creating Modules That Provide Services to Handlers

```cs
Contents of the DayModule.cs File
using System;
using System.Web;
namespace SimpleApp.Infrastructure {
	public class DayModule : IHttpModule {
		public void Init(HttpApplication app) {
			app.BeginRequest += (src, args) => {
				app.Context.Items["DayModule_Time"] = DateTime.Now;
			};
		}
		public void Dispose() {
			// nothing to do
		}
	}
}
```

```xml
//Registering the Module in the Web.config File
<?xml version="1.0" encoding="utf-8"?>
	<configuration>
	<system.webServer>
		<modules>
			<add name="DayPrep" type="SimpleApp.Infrastructure.DayModule"/>
		</modules>
	</system.webServer>
</configuration>
```

### Consuming the Items Data
```cs
namespace SimpleApp.Infrastructure {
	public class DayOfWeekHandler : IHttpHandler {
		public void ProcessRequest(HttpContext context) {
		
			if (context.Items.Contains("DayModule_Time")
				&& (context.Items["DayModule_Time"] is DateTime)) {
					string day = ((DateTime)context.Items["DayModule_Time"]).DayOfWeek.ToString();
		
				if (context.Request.CurrentExecutionFilePathExtension == ".json") {
					context.Response.ContentType = "application/json";
					context.Response.Write(string.Format("{{\"day\": \"{0}\"}}", day));
				} else {
					context.Response.ContentType = "text/html";
					context.Response.Write(string.Format("<span>It is: {0}</span>",	day));
				}
			} else {
				context.Response.ContentType = "text/html";
				context.Response.Write("No Module Data Available");
			}
		}
		
		public bool IsReusable {
			get { return false; }
		}
	}
}
```

### Custom Handler Factories



### Detecting Device Capabilities

#### The Contents of the Browser.cshtml File

```aspx
//The ASP.NET browser capabilities properties for the iPhone
@model IEnumerable<Tuple<string, string>>
@{
Layout = null;
}
<!DOCTYPE html>
<html>
<head>
	<meta name="viewport" content="width=device-width" />
	<title>Device Capabilities</title>
	<link href="~/Content/bootstrap.min.css" rel="stylesheet" />
	<link href="~/Content/bootstrap-theme.min.css" rel="stylesheet" />
</head>
<body class="container">
	<div class="panel panel-primary">
		<div class="panel-heading">Capabilities</div>
		<table class="table table-striped table-bordered">
			<tr><th>Property</th><th>Value</th></tr>
			<tr><td>Browser</td><td>@Request.Browser.Browser</td></tr>
			<tr><td>IsMobileDevice</td><td>@Request.Browser.IsMobileDevice</td></tr>
		<tr>
			<td>MobileDeviceManufacturer</td>
			<td>@Request.Browser.MobileDeviceManufacturer</td>
		</tr>
		<tr>
			<td>MobileDeviceModel</td>
			<td>@Request.Browser.MobileDeviceModel</td>
		</tr>
		<tr>
			<td>ScreenPixelsHeight</td>
			<td>@Request.Browser.ScreenPixelsHeight</td>
		</tr>
		<tr>
			<td>ScreenPixelsWidth</td>
			<td>@Request.Browser.ScreenPixelsWidth</td>
		</tr>
		<tr><td>Version</td><td>@Request.Browser.Version</td></tr>
		</table>
	</div>
</body>
</html>
```

#### Creating a Capability Provider

```cs
//The Contents of the KindleCapabilities.cs File
using System.Web;
using System.Web.Configuration;
namespace Mobile.Infrastructure {
	public class KindleCapabilities : HttpCapabilitiesProvider {
		public override HttpBrowserCapabilities
			GetBrowserCapabilities(HttpRequest request) {

			HttpCapabilitiesDefaultProvider defaults =
				new HttpCapabilitiesDefaultProvider();
				
			HttpBrowserCapabilities caps = defaults.GetBrowserCapabilities(request);
			
			if (request.UserAgent.Contains("Kindle Fire")) {
				caps.Capabilities["Browser"] = "Silk";
				caps.Capabilities["IsMobileDevice"] = "true";
				caps.Capabilities["MobileDeviceManufacturer"] = "Amazon";
				caps.Capabilities["MobileDeviceModel"] = "Kindle Fire";
				if (request.UserAgent.Contains("Kindle Fire HD")) 
				{
					caps.Capabilities["MobileDeviceModel"] = "Kindle Fire HD";
				}
			}
			return caps;
		}
	}
}
```

```cs
//Registering the Capabilities Provider in the Global.asax.cs File
using System.Web.Configuration;
using System.Web.Mvc;
using System.Web.Routing;
using Mobile.Infrastructure;
namespace Mobile {
	public class MvcApplication : System.Web.HttpApplication {
		protected void Application_Start() {
			AreaRegistration.RegisterAllAreas();
			RouteConfig.RegisterRoutes(RouteTable.Routes);
			HttpCapabilitiesBase.BrowserCapabilitiesProvider = new KindleCapabilities();
		}
	}

}
```

## Tracing Requests

### Responding to the Logging Events
```cs
//The Contents of the LogModule.cs File
namespace Mobile.Infrastructure {
	public class LogModule : IHttpModule {
		private static int sharedCounter = 0;
		private int requestCounter;
		
		private static object lockObject = new object();
		private Exception requestException = null;
		
		public void Init(HttpApplication app) {
				app.BeginRequest += (src, args) => {
					requestCounter = ++sharedCounter;
			};
			
			app.Error += (src, args) => {
				requestException = HttpContext.Current.Error;
			};
			
			app.LogRequest += (src, args) => WriteLogMessage(HttpContext.Current);
		}
		
		private void WriteLogMessage(HttpContext ctx) {
			StringWriter sr = new StringWriter();
			sr.WriteLine("--------------");
			sr.WriteLine("Request: {0} for {1}", requestCounter, ctx.Request.RawUrl);
			
			if (ctx.Handler != null) {
				sr.WriteLine("Handler: {0}", ctx.Handler.GetType());
			}
			
			sr.WriteLine("Status Code: {0}, Message: {1}", ctx.Response.StatusCode,
			ctx.Response.StatusDescription);
			sr.WriteLine("Elapsed Time: {0} ms",
			DateTime.Now.Subtract(ctx.Timestamp).Milliseconds);
			
			if (requestException != null) {
				sr.WriteLine("Error: {0}", requestException.GetType());
			}
			
			lock (lockObject) {
			Debug.Write(sr.ToString());
			}
		}
		
		public void Dispose() {
		// do nothing
		}
	}
}
```

```xml
//Registering the Module in the Web.config File
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<system.webServer>
		<modules>
			<add name="Log" type="Mobile.Infrastructure.LogModule"/>
		</modules>
	</system.webServer>
</configuration>
```

### Enabling Request Tracing
```xml
//Enabling Request Tracing in the Web.config File
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<system.web>
		<trace enabled="true" requestLimit="50" />
	</system.web>
</configuration>
```

### Adding Custom Trace Messages
```cs
//Using Request Tracing in the LogModule.cs File
namespace Mobile.Infrastructure {
	public class LogModule : IHttpModule {
		private const string traceCategory = "LogModule";
		
		public void Init(HttpApplication app) {
			app.BeginRequest += (src, args) => {
				HttpContext.Current.Trace.Write(traceCategory, "BeginRequest");
			};
			
			app.EndRequest += (src, args) => {
				HttpContext.Current.Trace.Write(traceCategory, "EndRequest");
			};
		
			app.PostMapRequestHandler += (src, args) => {
				HttpContext.Current.Trace.Write(traceCategory,
				string.Format("Handler: {0}",
				HttpContext.Current.Handler));
			};
			
			app.Error += (src, args) => {
				HttpContext.Current.Trace.Warn(traceCategory, string.Format("Error: {0}",
				HttpContext.Current.Error.GetType().Name));
			};
		}
		
		public void Dispose() {
		// do nothing
		}
	}
}
```

```cs
//Adding Tracing in the HomeController.cs File
using System.Web.Mvc;
using Mobile.Models;
namespace Mobile.Controllers {
	public class HomeController : Controller {
		private Programmer[] progs = {
			new Programmer("Alice", "Smith", "Lead Developer", "Paris", "France", "C#"),
			new Programmer("Joe", "Dunston", "Developer", "London", "UK", "Java"),
			new Programmer("Peter", "Jones", "Developer", "Chicago", "USA", "C#"),
			new Programmer("Murray", "Woods", "Jnr Developer", "Boston", "USA", "C#")
		};
		
		public ActionResult Index() {
			HttpContext.Trace.Write("HomeController", "Index Method Started");
			HttpContext.Trace.Write("HomeController",
			string.Format("There are {0} programmers", progs.Length));
			ActionResult result = View(progs);
			HttpContext.Trace.Write("HomeController", "Index Method Completed");
			return result;
		}
		
		public ActionResult Browser() {
			return View();
		}
	}
}
```

```aspx
//Adding Trace Statements to the Programmers.cshtml File
@using Mobile.Models
@model Programmer[]
<table class="table table-striped">
	<tr>
		<th>First Name</th>
		<th class="hidden-xs">Last Name</th>
		<th class="hidden-xs">Title</th>
		<th>City</th>
		<th class="hidden-xs">Country</th>
		<th>Language</th>
	</tr>
	@foreach (Programmer prog in Model) {
		Context.Trace.Write("Programmers View",
			string.Format("Processing {0} {1}",
			prog.FirstName, prog.LastName));
	<tr>
		<td>@prog.FirstName</td>
		<td class="hidden-xs">@prog.LastName</td>
		<td class="hidden-xs">@prog.Title</td>
		<td>@prog.City</td>
		<td class="hidden-xs">@prog.Country</td>
		<td>@prog.Language</td>
	</tr>
	}
</table>
```

## Configuration

### Using Application Settings
```xml
Defining Application Settings in the Web.config File
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<appSettings>
		<add key="webpages:Version" value="3.0.0.0" />
		<add key="webpages:Enabled" value="false" />
		<add key="ClientValidationEnabled" value="true" />
		<add key="UnobtrusiveJavaScriptEnabled" value="true" />
		<add key="defaultCity" value="New York"/>
		<add key="defaultCountry" value="USA"/>
		<add key="defaultLanguage" value="English"/>
	</appSettings>
</configuration>	
```

### Reading Application Settings
```cs
//Reading Application Settings in the HomeController.cs File

using System.Collections.Generic;
using System.Web.Mvc;
using System.Web.Configuration;
namespace ConfigFiles.Controllers {
	public class HomeController : Controller {
		public ActionResult Index() {
			Dictionary<string, string> configData = new Dictionary<string, string>();
			foreach (string key in WebConfigurationManager.AppSettings) {
				configData.Add(key, WebConfigurationManager.AppSettings[key]);
			}
		return View(configData);
		}
	}
}
```

```cs
//Adding an Action Method in the HomeController.cs File
using System.Collections.Generic;
using System.Web.Mvc;
using System.Web.Configuration;
namespace ConfigFiles.Controllers {
	public class HomeController : Controller {
		public ActionResult Index() {
		
		Dictionary<string, string> configData = new Dictionary<string, string>();
		
		foreach (string key in WebConfigurationManager.AppSettings) {
			configData.Add(key, WebConfigurationManager.AppSettings[key]);
		}
			return View(configData);
		}
		
		public ActionResult DisplaySingle() {
			return View((object)WebConfigurationManager.AppSettings["defaultLanguage"]);
		}
	}
}
```

### Using Connection Strings
```xml
//Adding a Connection String to the Web.config File
<?xml version="1.0" encoding="utf-8"?>
<configuration>

	<connectionStrings>
		<add name="EFDbContext" connectionString="Data Source=(localdb)\v11.0;Initial
			Catalog=SportsStore;Integrated Security=True"
			providerName="System.Data.SqlClient"/>
	</connectionStrings>
</configuration>
```

### Reading Connection Strings

```cs
//Reading a Connection String in the HomeController.cs File
using System.Configuration;
namespace ConfigFiles.Controllers {
	public class HomeController : Controller {
		public ActionResult Index() {
			Dictionary<string, string> configData = new Dictionary<string, string>();
			foreach (ConnectionStringSettings cs in
				WebConfigurationManager.ConnectionStrings) {
				configData.Add(cs.Name, cs.ProviderName + " " + cs.ConnectionString);
			}
			return View(configData);
		}
		
		public ActionResult DisplaySingle() {
			return View((object)WebConfigurationManager
				.ConnectionStrings["EFDbContext"].ConnectionString);
		}
	}
}
```

### Grouping Settings Together
```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<system.web>
		<compilation debug="true" targetFramework="4.5.1" />
		<httpRuntime targetFramework="4.5.1" />
	</system.web>
</configuration>
```

### Creating a Simple Configuration Section

```xml
//Adding a New Configuration Section to the Web.config File

<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<appSettings>
		<add key="defaultCity" value="New York"/>
		<add key="defaultCountry" value="USA"/>
		<add key="defaultLanguage" value="English"/>
	</appSettings>

	<newUserDefaults city="Chicago" country="USA" language="English" regionCode="1"/>

</configuration>
```

### Creating the Configuration Section Handler Class

```cs
The Contents of the NewUserDefaultsSection.cs File
using System.Configuration;
namespace ConfigFiles.Infrastructure {
	public class NewUserDefaultsSection : ConfigurationSection {
	[ConfigurationProperty("city", IsRequired = true)]
		public string City {
			get { return (string)this["city"]; }
			set { this["city"] = value; }
		}
		
		[ConfigurationProperty("country", DefaultValue = "USA")]
		public string Country {
			get { return (string)this["country"]; }
			set { this["country"] = value; }
		}
		
		[ConfigurationProperty("language")]
		public string Language {
			get { return (string)this["language"]; }
			set { this["language"] = value; }
		}
		
		[ConfigurationProperty("regionCode")]
		[IntegerValidator(MaxValue = 5, MinValue = 0)]
		public int Region {
			get { return (int)this["regionCode"]; }
			set { this["regionCode"] = value; }
		}
	}
}
```

### Defining the Section
```xml
Defining a Custom Configuration Section in the Web.config File
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<configSections>
		<section name="newUserDefaults"
		type="ConfigFiles.Infrastructure.NewUserDefaultsSection"/>
	</configSections>
	
	<newUserDefaults city="Chicago" country="USA" language="English" regionCode="1"/>

</configuration>
```

```cs
//Reading Values from a Configuration Section

using System.Collections.Generic;
using System.Web.Mvc;
using System.Web.Configuration;
using System.Configuration;
using ConfigFiles.Infrastructure;
namespace ConfigFiles.Controllers {
public class HomeController : Controller {
	public ActionResult Index() {
	
		Dictionary<string, string> configData = new Dictionary<string, string>();
		
		NewUserDefaultsSection nuDefaults = WebConfigurationManager
		.GetWebApplicationSection("newUserDefaults") as NewUserDefaultsSection;
		
		if (nuDefaults != null) {
			configData.Add("City", nuDefaults.City);
			configData.Add("Country", nuDefaults.Country);
			configData.Add("Language", nuDefaults.Language);
			configData.Add("Region", nuDefaults.Region.ToString());
		};
		
		return View(configData);
		}
		public ActionResult DisplaySingle() {
			return View((object)WebConfigurationManager
				.ConnectionStrings["EFDbContext"].ConnectionString);
		}
	}
}
```

### Creating a Collection Configuration Section
```xml
//Adding a Collection Configuration Section to the Web.config File
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<configSections>
		<section name="newUserDefaults"
			type="ConfigFiles.Infrastructure.NewUserDefaultsSection"/>
	</configSections>
	
	<!-- ...application settings and connection strings omitted for brevity... -->
	<newUserDefaults city="Chicago" country="USA" language="English" regionCode="1"/>
	
	<places default="LON">
		<add code="NYC" city="New York" country="USA" />
		<add code="LON" city="London" country="UK" />
		<add code="PAR" city="Paris" country="France" />
	</places>

</configuration>
```

```cs
//The Contents of the Place.cs File
using System;
using System.Configuration;
namespace ConfigFiles.Infrastructure {
	public class Place : ConfigurationElement {

		[ConfigurationProperty("code", IsRequired = true)]
		public string Code {
			get { return (string)this["code"]; }
			set { this["code"] = value; }
		}
		
		[ConfigurationProperty("city", IsRequired = true)]
		public string City {
			get { return (string)this["city"]; }
			set { this["city"] = value; }
		}
		
		[ConfigurationProperty("country", IsRequired = true)]
		public String Country {
			get { return (string)this["country"]; }
			set { this["country"] = value; }
		}
	}
}
```

```cs
//Reading a Collection Configuration Section in the HomeController.cs File
using System.Collections.Generic;
using System.Web.Mvc;
using System.Web.Configuration;
using System.Configuration;
using ConfigFiles.Infrastructure;
namespace ConfigFiles.Controllers {
	public class HomeController : Controller {
		public ActionResult Index() {
			Dictionary<string, string> configData = new Dictionary<string, string>();
				PlaceSection section = WebConfigurationManager
				.GetWebApplicationSection("places") as PlaceSection;
			foreach (Place place in section.Places) {
				configData.Add(place.Code, string.Format("{0} ({1})",			place.City, place.Country));
			}
			return View(configData);
		}
		
		public ActionResult DisplaySingle() {
			PlaceSection section = WebConfigurationManager
			.GetWebApplicationSection("places") as PlaceSection;
			Place defaultPlace = section.Places[section.Default];
			return View((object)string.Format("The default place is: {0}",	defaultPlace.City));
		}
	}
}
```

### Overriding Configuration Settings

```xml
//Adding a location Element to the Web.config File
<?xml version="1.0" encoding="utf-8"?>
<configuration>
<location path="Home/Index">
<appSettings>
<add key="defaultCity" value="London"/>
<add key="defaultCountry" value="UK"/>
</appSettings>
</location>
</configuration>

```cs
//Reading Application Settings in the HomeController.cs File
namespace ConfigFiles.Controllers {
	public class HomeController : Controller {
		public ActionResult Index() {
			Dictionary<string, string> configData = new Dictionary<string, string>();
			foreach (string key in WebConfigurationManager.AppSettings.AllKeys) {
				configData.Add(key, WebConfigurationManager.AppSettings[key]);
			}
			return View(configData);
		}
		public ActionResult OtherAction() {
			Dictionary<string, string> configData = new Dictionary<string, string>();
			foreach (string key in WebConfigurationManager.AppSettings.AllKeys) {
				configData.Add(key, WebConfigurationManager.AppSettings[key]);
			}
			return View("Index", configData);
		}
	}
}
```

### Using Folder-Level Files
```xml
//The Contents of the Web.config File in the Views/Home Folder
<?xml version="1.0"?>
<configuration>
	<appSettings>
		<add key="defaultCity" value="Paris"/>
		<add key="defaultCountry" value="France"/>
	</appSettings>
</configuration>
```

```cs
//Reading a Folder-Level Configuration in the HomeController.cs File
using System.Collections.Generic;
using System.Configuration;
using System.Web.Configuration;
using System.Web.Mvc;
namespace ConfigFiles.Controllers {
	public class HomeController : Controller {
		public ActionResult Index() {
			Dictionary<string, string> configData = new Dictionary<string, string>();
			foreach (string key in WebConfigurationManager.AppSettings.AllKeys) {
				configData.Add(key, WebConfigurationManager.AppSettings[key]);
			}
			return View(configData);
		}
		
		public ActionResult OtherAction() {
			Dictionary<string, string> configData = new Dictionary<string, string>();
			AppSettingsSection appSettings = WebConfigurationManager.OpenWebConfiguration("~/Views/Home").AppSettings;
			
			foreach (string key in appSettings.Settings.AllKeys) {
				configData.Add(key, appSettings.Settings[key].Value);
			}
			return View("Index", configData);
		}
	}
}
```

### Navigating the ASP.NET Configuration Elements

```cs
//Reading ASP.NET Configuration Elements in the HomeController.cs File
namespace ConfigFiles.Controllers {
	public class HomeController : Controller {
		public ActionResult Index() {
			Dictionary<string, string> configData = new Dictionary<string, string>();
			SystemWebSectionGroup sysWeb = 	(SystemWebSectionGroup)WebConfigurationManager.OpenWebConfiguration("/").GetSectionGroup("system.web");
			configData.Add("debug", sysWeb.Compilation.Debug.ToString());
			configData.Add("targetFramework", sysWeb.Compilation.TargetFramework);
			return View(configData);
		}
	}
}
```

## State Data

```cs
//Gaining Exclusive Access to the Application State Data in the AppStateHelper.cs File
using System;
using System.Web;
using System.Collections.Generic;

namespace StateData.Infrastructure {
	public enum AppStateKeys {
		COUNTER,
		LAST_REQUEST_TIME,
		LAST_REQUEST_URL
	};

		
	public static class AppStateHelper {
		public static object Get(AppStateKeys key, object defaultValue = null) {
			string keyString = Enum.GetName(typeof(AppStateKeys), key);
			if (HttpContext.Current.Application[keyString] == null
				&& defaultValue != null) {
			HttpContext.Current.Application[keyString] = defaultValue;
			}
		return HttpContext.Current.Application[keyString];
	}
	
	public static object Set(AppStateKeys key, object value) {
		return HttpContext.Current.Application[Enum.GetName(typeof(AppStateKeys),key)] = value;
	}
	
	public static IDictionary<AppStateKeys, object>
		GetMultiple(params AppStateKeys[] keys) {
	
		Dictionary<AppStateKeys, object> results = new Dictionary<AppStateKeys, object>();
		HttpApplicationState appState = HttpContext.Current.Application;
		appState.Lock();
	
		foreach (AppStateKeys key in keys) {
			string keyString = Enum.GetName(typeof(AppStateKeys), key);
			results.Add(key, appState[keyString]);
		}
		
		appState.UnLock();
		return results;
	}
	
	public static void SetMultiple(IDictionary<AppStateKeys, object> data) {
		HttpApplicationState appState = HttpContext.Current.Application;
		appState.Lock();
		foreach (AppStateKeys key in data.Keys) {
			string keyString = Enum.GetName(typeof(AppStateKeys), key);
			appState[keyString] = data[key];
		}
			appState.UnLock();
		}
	}
}
```

### Working with Session Data

```cs
//The Contents of the RegistrationController.cs File
using System.Web.Mvc;
namespace StateData.Controllers {
	public class RegistrationController : Controller {
		public ActionResult Index() {
			return View();
		}
		
		[HttpPost]
		public ActionResult ProcessFirstForm(string name) {
			System.Diagnostics.Debug.WriteLine("Name: {0}", (object)name);
			return View("SecondForm");
		}
		
		[HttpPost]
		public ActionResult CompleteForm(string country) {
			System.Diagnostics.Debug.WriteLine("Country: {0}", (object)country);
			// in a real application, this is where the call to create the
			// new user account would be
			ViewBag.Name = "<Unknown>";
			ViewBag.Country = country;
			return View();
		}
	}
}
```

```aspx
//The Contents of the CompleteForm.cshtml File
@{ Layout = null; }
<!DOCTYPE html>
<html>
<head>
	<meta name="viewport" content="width=device-width" />
	<title>Finished</title>
	<link href="~/Content/bootstrap.min.css" rel="stylesheet" />
	<link href="~/Content/bootstrap-theme.min.css" rel="stylesheet" />
	<style>body { padding-top: 10px; }</style>
</head>
<body class="container">
	<div class="panel panel-default">
		<div class="panel-heading">Registration Details</div>
		<table class="table table-striped">
			<tr><th>Name</th><td>@ViewBag.Name</td></tr>
			<tr><th>Country</th><td>@ViewBag.Country</td></tr>
		</table>
	</div>
</body>
</html>
```

### Using Session State Data
```cs
//The Contents of the SessionStateHelper.cs File
using System;
using System.Web;
namespace StateData.Infrastructure {
	public enum SessionStateKeys {
		NAME
	}
	
	public static class SessionStateHelper {
		public static object Get(SessionStateKeys key) {
			string keyString = Enum.GetName(typeof(SessionStateKeys), key);
			return HttpContext.Current.Session[keyString];
		}
		
		public static object Set(SessionStateKeys key, object value) {
			string keyString = Enum.GetName(typeof(SessionStateKeys), key);
			return HttpContext.Current.Session[keyString] = value;
		}
	}
}
```


```cs
Using Session State Data in the RegistrationController.cs File
using System.Web.Mvc;
using StateData.Infrastructure;
namespace StateData.Controllers {
	public class RegistrationController : Controller {

		public ActionResult Index() {
			return View();
		}
		
		[HttpPost]
		public ActionResult ProcessFirstForm(string name) {
			SessionStateHelper.Set(SessionStateKeys.NAME, name);
			return View("SecondForm");
		}
		
		[HttpPost]
		public ActionResult CompleteForm(string country) {
			ViewBag.Name = SessionStateHelper.Get(SessionStateKeys.NAME);
			ViewBag.Country = country;
			return View();
			}
	}
}
```

```cs
//Understanding How Sessions Work
//The Contents of the LifecycleController.cs File
using System.Web;
using System.Web.Mvc;
using StateData.Infrastructure;
namespace StateData.Controllers {
	public class LifecycleController : Controller {
		public ActionResult Index() {
			return View();
		}
		
		[HttpPost]
		public ActionResult Index(bool store = false, bool abandon = false) {
			if (store) {
				SessionStateHelper.Set(SessionStateKeys.NAME, "Adam");
			}
			if (abandon) {
				Session.Abandon();
			}
			return RedirectToAction("Index");
		}
	}
}
```

```cs
//Contents of the Index.cshtml File in the /Views/Lifecycle Folder
@{ Layout = null; }
<!DOCTYPE html>
<html>
<head>
	<meta name="viewport" content="width=device-width" />
	<title>Session Lifecycle</title>
	<link href="~/Content/bootstrap.min.css" rel="stylesheet" />
	<link href="~/Content/bootstrap-theme.min.css" rel="stylesheet" />
	<style> body { padding-top: 10px; } </style>
</head>
<body class="container">
	<div class="panel panel-primary">
		<div class="panel-heading">Session</div>
		<table class="table">
			<tr><th>Session ID</th><td>@Session.SessionID</td></tr>
			<tr><th>Is New?</th><td>@Session.IsNewSession</td></tr>
			<tr><th>State Data Count</th><td>@Session.Count</td></tr>
		</table>
	</div>
	@using(Html.BeginForm()) {
	<div class="checkbox">
		<label>
		@Html.CheckBox("store") Store State Data</label>
	</div>
	
	<div class="checkbox">
		<label>
		@Html.CheckBox("abandon") Abandon Session</label>
	</div>
	<button class="btn btn-primary" type="submit">Submit</button>
	}
</body>
</html>
```

### Configuring Sessions and Session State

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<system.web>
		<sessionState cookieless="UseUri" />
	</system.web>
</configuration>
```

### Using the State Server
```xml
Configuring the State Server in the Web.config File
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<system.web>
		<sessionState cookieless="UseCookies" mode="StateServer" stateConnectionString="tcpip=localhost:42424" />
	</system.web>
</configuration>
```

### Using a SQL Database
```xml
Configuring the Universal Provider for Session Data in the Web.config File
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<connectionStrings>
		<add name="StateDb" providerName="System.Data.SqlClient"
			connectionString="Data Source=(localdb)\v11.0;Initial Catalog=StateDb;	Integrated Security=True" />
	</connectionStrings>

	<sessionState mode="Custom" customProvider="DefaultSessionProvider">
		<providers>
			<add name="DefaultSessionProvider" connectionStringName="StateDb" 	type="System.Web.Providers.DefaultSessionStateProvider,
				System.Web.Providers, Version=2.0.0.0, Culture=neutral,	PublicKeyToken=31bf3856ad364e35" />
		</providers>
	</sessionState>
</system.web>
</configuration>
```

## Caching Data

### Using Basic Caching

```cs
//Using the Cache in the CacheController.cs File
using System.Net.Http;
using System.Threading.Tasks;
using System.Web;
using System.Web.Mvc;
namespace StateData.Controllers {
	public class CacheController : Controller {
		public ActionResult Index() {
			return View((long?)(HttpContext.Cache["pageLength"]));
		}
		
		[HttpPost]
		public async Task<ActionResult> PopulateCache() {
			HttpResponseMessage result 	= await new HttpClient().GetAsync("http://apress.com");
			HttpContext.Cache["pageLength"] = result.Content.Headers.ContentLength;
			return RedirectToAction("Index");
		}
	}
}
```

### Configuring the Cache

```xml
//Configuring the Cache in the Web.config File
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<caching>
		<cache percentagePhysicalMemoryUsedLimit="10" />
	</caching>
</configuration>
```

### Using Absolute Time Expiration
```cs
Expiring Cache Items in the CacheController.cs File
using System;
using System.Net.Http;
using System.Threading.Tasks;
using System.Web;
using System.Web.Mvc;
using System.Web.Caching;
namespace StateData.Controllers {
	public class CacheController : Controller {
		public ActionResult Index() {
		return View((long?)(HttpContext.Cache["pageLength"]));
		}
		
		[HttpPost]
		public async Task<ActionResult> PopulateCache() {
			HttpResponseMessage result 		= await new HttpClient().GetAsync("http://apress.com");
			long? data = result.Content.Headers.ContentLength;

			DateTime expiryTime = DateTime.Now.AddSeconds(30);
			HttpContext.Cache.Insert("pageLength", data, null, expiryTime,
			Cache.NoSlidingExpiration);

			return RedirectToAction("Index");
		}
	}
}
```

### Using Sliding Time Expirations

```cs
//Using a Sliding Expiration in the CacheController.cs File
using System.Web.Caching;

namespace StateData.Controllers {
	public class CacheController : Controller {
		public ActionResult Index() {
			return View((long?)(HttpContext.Cache["pageLength"]));
		}
		
		[HttpPost]
		public async Task<ActionResult> PopulateCache() {
		HttpResponseMessage result 		= await new HttpClient().GetAsync("http://apress.com");
		long? data = result.Content.Headers.ContentLength;
		TimeSpan idleDuration = new TimeSpan(0, 0, 30);
		HttpContext.Cache.Insert("pageLength", data, null, Cache.NoAbsoluteExpiration, idleDuration);
		return RedirectToAction("Index");
		}
	}
}
```

### Creating a File Dependency
```cs
//Creating a File Dependency in the CacheController.cs File
using System.Web.Caching;
namespace StateData.Controllers {
	public class CacheController : Controller {
	
		public ActionResult Index() {
			return View((long?)(HttpContext.Cache["pageLength"]));
		}
		
		[HttpPost]
		public async Task<ActionResult> PopulateCache() {
			HttpResponseMessage result	= await new HttpClient().GetAsync("http://apress.com");
			long? data = result.Content.Headers.ContentLength;
			
			CacheDependency dependency = new CacheDependency(Request.MapPath("~/data.txt"));
			HttpContext.Cache.Insert("pageLength", data, dependency);

			return RedirectToAction("Index");
		}
	}
}
```

### Depending on Another Cached Item
```cs
//Adding a New Action Method to the CacheController.cs File
using System.Web.Caching;

namespace StateData.Controllers {
	public class CacheController : Controller {
		
		public ActionResult Index() {
			return View((long?)(HttpContext.Cache["pageLength"]));
		}
		
		[HttpPost]
		public async Task<ActionResult> PopulateCache() {
			HttpResponseMessage result 	= await new HttpClient().GetAsync("http://apress.com");
			long? data = result.Content.Headers.ContentLength;
			CacheDependency dependency = new
			CacheDependency(Request.MapPath("~/data.txt"));
			HttpContext.Cache.Insert("pageLength", data, dependency);
			DateTime timestamp = DateTime.Now;
			CacheDependency timesStampDependency = new CacheDependency(null, new string[] { "pageLength" });
			HttpContext.Cache.Insert("pageTimestamp", timestamp, timesStampDependency);
			return RedirectToAction("Index");
		}
	}
}
```

### Creating Custom Dependencies

```cs
//The Contents of the SelfExpiringData.cs File

using System.Web.Caching;
namespace StateData.Infrastructure {
	public class SelfExpiringData<T> : CacheDependency {
		private T dataValue;
		private int requestCount = 0;
		private int requestLimit;
		
		public T Value {
			get {
				if (requestCount++ >= requestLimit) {
					NotifyDependencyChanged(this, EventArgs.Empty);
				}
			return dataValue;
			}
		}
		
		public SelfExpiringData(T data, int limit) {
			dataValue = data;
			requestLimit = limit;
		}
	}
}
```

```cs
//Applying the Self-expiring Cache Dependency in the CacheController.cs File

using System.Web.Caching;

using StateData.Infrastructure;
namespace StateData.Controllers {
	public class CacheController : Controller {
		public ActionResult Index() {
			SelfExpiringData<long?> seData = (SelfExpiringData<long?>)HttpContext.Cache["pageLength"];
			return View(seData == null ? null : seData.Value);
		}
		
		[HttpPost]
		public async Task<ActionResult> PopulateCache() {
			HttpResponseMessage result 	= await new HttpClient().GetAsync("http://apress.com");
			long? data = result.Content.Headers.ContentLength;
			SelfExpiringData<long?> seData = new SelfExpiringData<long?>(data, 3);
			HttpContext.Cache.Insert("pageLength", seData, seData);
			return RedirectToAction("Index");
		}
	}
}
```

```cs
//Creating an Aggregate Dependency in the CacheController.cs File

namespace StateData.Controllers {
public class CacheController : Controller {
	public ActionResult Index() {
			SelfExpiringData<long?> seData = (SelfExpiringData<long?>)HttpContext.Cache["pageLength"];
			return View(seData == null ? null : seData.Value);
		}
		
		[HttpPost]
		public async Task<ActionResult> PopulateCache() {
			HttpResponseMessage result	= await new HttpClient().GetAsync("http://apress.com");
			
			long? data = result.Content.Headers.ContentLength;
			SelfExpiringData<long?> seData = new SelfExpiringData<long?>(data, 3);
			CacheDependency fileDep = new CacheDependency(Request.MapPath("~/data.txt"));
			AggregateCacheDependency aggDep = new AggregateCacheDependency();
			
			aggDep.Add(seData, fileDep);
			HttpContext.Cache.Insert("pageLength", seData, aggDep);
			return RedirectToAction("Index");
		}
	}
}
```

```cs
//Receiving Dependency Notifications in the CacheController.cs File
using System;
using System.Net.Http;
using System.Threading.Tasks;
using System.Web;
using System.Web.Caching;
using System.Web.Mvc;
using StateData.Infrastructure;
namespace StateData.Controllers {
	public class CacheController : Controller {
		public ActionResult Index() {
			SelfExpiringData<long?> seData = (SelfExpiringData<long?>)HttpContext.Cache["pageLength"];
			return View(seData == null ? null : seData.Value);
		}
		
		[HttpPost]
		public async Task<ActionResult> PopulateCache() {
			HttpResponseMessage result
			= await new HttpClient().GetAsync("http://apress.com");
			long? data = result.Content.Headers.ContentLength;
			SelfExpiringData<long?> seData = new SelfExpiringData<long?>(data, 3);
			HttpContext.Cache.Insert("pageLength", seData, seData,
			Cache.NoAbsoluteExpiration, Cache.NoSlidingExpiration,
			CacheItemPriority.Normal, HandleNotification);
			return RedirectToAction("Index");
		}
		
		private void HandleNotification(string key, object data,
			CacheItemRemovedReason reason) {
			System.Diagnostics.Debug.WriteLine("Item {0} removed. ({1})",
			key, Enum.GetName(typeof(CacheItemRemovedReason), reason));
		}
	}
}
```

## Caching Content

```cs
//Adding Content Caching to the HomeController.cs File
using ContentCache.Infrastructure;
namespace ContentCache.Controllers {
	public class HomeController : Controller {
		[OutputCache(Duration = 30, Location = OutputCacheLocation.Downstream)]
		public ActionResult Index() {
			Thread.Sleep(1000);
			int counterValue = AppStateHelper.IncrementAndGet(
			AppStateKeys.INDEX_COUNTER);
			Debug.WriteLine(string.Format("INDEX_COUNTER: {0}", counterValue));
			return View(counterValue);
		}
	}
}
```

### Caching at the Server

```cs
using ContentCache.Infrastructure;

namespace ContentCache.Controllers {
	public class HomeController : Controller {
		[OutputCache(Duration = 30, Location = OutputCacheLocation.Server)]
		public ActionResult Index() {
			Thread.Sleep(1000);
			int counterValue = AppStateHelper.IncrementAndGet(
			AppStateKeys.INDEX_COUNTER);
			Debug.WriteLine(string.Format("INDEX_COUNTER: {0}", counterValue));
			return View(counterValue);
		}
	}
}
```


### Varying Caching Using Headers
```cs
//Varying Cached Content Based on Headers in the HomeController.cs File
using System.Diagnostics;
using System.Threading;
using System.Web.Mvc;
using System.Web.UI;
using ContentCache.Infrastructure;
namespace ContentCache.Controllers {
	public class HomeController : Controller {
	[OutputCache(Duration = 30, VaryByHeader="user-agent",
	Location = OutputCacheLocation.Any)]
		public ActionResult Index() {
			Thread.Sleep(1000);
			int counterValue = AppStateHelper.IncrementAndGet(
			AppStateKeys.INDEX_COUNTER);
			Debug.WriteLine(string.Format("INDEX_COUNTER: {0}", counterValue));
			return View(counterValue);
		}
	}
}
```

### Varying Caching Using Form or Query String Data
```cs
//Varying Cached Content Based on User Data in the HomeController.cs File
using System.Diagnostics;
using System.Threading;
using System.Web.Mvc;
using System.Web.UI;
using ContentCache.Infrastructure;
namespace ContentCache.Controllers {
	public class HomeController : Controller {
	[OutputCache(Duration = 30, VaryByHeader="user-agent",
	VaryByParam="name;city", Location = OutputCacheLocation.Any)]
		public ActionResult Index() {
			Thread.Sleep(1000);
			int counterValue = AppStateHelper.IncrementAndGet(
			AppStateKeys.INDEX_COUNTER);
			Debug.WriteLine(string.Format("INDEX_COUNTER: {0}", counterValue));
			return View(counterValue);
		}
	}
}
```

### Using a Custom Cache Variation in the HomeController.cs File
```cs
namespace ContentCache.Controllers {
	public class HomeController : Controller {
	[OutputCache(Duration = 30,
	VaryByHeader="user-agent",
	VaryByParam="name;city",
	VaryByCustom="mobile",
	Location = OutputCacheLocation.Any)]

		public ActionResult Index() {
			Thread.Sleep(1000);
			int counterValue = AppStateHelper.IncrementAndGet(
			AppStateKeys.INDEX_COUNTER);
			Debug.WriteLine(string.Format("INDEX_COUNTER: {0}", counterValue));
			return View(counterValue);
		}
	}
}
```

### Adding a Custom Cache Variation to the Global.asax.cs File
```cs
namespace ContentCache {
	public class MvcApplication : System.Web.HttpApplication {
		protected void Application_Start() {
			AreaRegistration.RegisterAllAreas();
			RouteConfig.RegisterRoutes(RouteTable.Routes);
		}
		
		public override string GetVaryByCustomString(HttpContext ctx, string custom) {
			if (custom == "mobile") {
				return Request.Browser.IsMobileDevice.ToString();
			} else {
				return base.GetVaryByCustomString(ctx, custom);
			}
		}
	}
}
```

### Creating Cache Profiles in the Web.config File
```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<system.web>
		<caching>
			<outputCacheSettings>
				<outputCacheProfiles>
					<add name="cp1" duration="30" location="Any" varyByHeader="user-agent" varyByParam="name;city" varyByCustom="mobile"/>
				</outputCacheProfiles>
			</outputCacheSettings>
		</caching>
	</system.web>
</configuration>
```

### Applying a Cache Profile in the HomeController.cs File
```cs
using ContentCache.Infrastructure;
namespace ContentCache.Controllers {
	public class HomeController : Controller {
	[OutputCache(CacheProfile="cp1")]
		public ActionResult Index() {
			Thread.Sleep(1000);
			int counterValue = AppStateHelper.IncrementAndGet(
			AppStateKeys.INDEX_COUNTER);
			Debug.WriteLine(string.Format("INDEX_COUNTER: {0}", counterValue));
			return View(counterValue);
		}
	}
}
```

### Caching Child Action Output
```cs
//Adding a Child Action to the HomeController.cs File

namespace ContentCache.Controllers {
	public class HomeController : Controller {
	[OutputCache(CacheProfile = "cp1")]
		public ActionResult Index() {
			Thread.Sleep(1000);
			int counterValue = AppStateHelper.IncrementAndGet(
			AppStateKeys.INDEX_COUNTER);
			Debug.WriteLine(string.Format("INDEX_COUNTER: {0}", counterValue));
			return View(counterValue);
		}
		
		[ChildActionOnly]
		[OutputCache(Duration=60)]
		public PartialViewResult GetTime() {
			return PartialView((object)DateTime.Now.ToShortTimeString());
		}
	}
}
```

### Dynamically Setting Cache Policy
```cs
namespace ContentCache.Controllers {
	public class HomeController : Controller {
		public ActionResult Index() {
			if (Request.RawUrl == "/Home/Index") {
				Response.Cache.SetNoServerCaching();
				Response.Cache.SetCacheability(HttpCacheability.NoCache);
			} else {
				Response.Cache.SetExpires(DateTime.Now.AddSeconds(30));
				Response.Cache.SetCacheability(HttpCacheability.Public);
			}
			
			Thread.Sleep(1000);
			
			int counterValue = AppStateHelper.IncrementAndGet(
			AppStateKeys.INDEX_COUNTER);
			Debug.WriteLine(string.Format("INDEX_COUNTER: {0}", counterValue));
			return View(counterValue);
		}
	}
}
```

### Validating Cached Content
```cs
//Using a Cache Validation Callback to the HomeController.cs File
namespace ContentCache.Controllers {
	public class HomeController : Controller {

		public ActionResult Index() {
			Response.Cache.SetExpires(DateTime.Now.AddSeconds(30));
			Response.Cache.SetCacheability(HttpCacheability.Server);
			Response.Cache.AddValidationCallback(CheckCachedItem, Request.UserAgent);
			Thread.Sleep(1000);
			int counterValue = AppStateHelper.IncrementAndGet(
			AppStateKeys.INDEX_COUNTER);
			Debug.WriteLine(string.Format("INDEX_COUNTER: {0}", counterValue));
			return View(counterValue);
		}
		
		[ChildActionOnly]
		[OutputCache(Duration = 60)]
		public PartialViewResult GetTime() {
			return PartialView((object)DateTime.Now.ToShortTimeString());
		}
		
		public void CheckCachedItem(HttpContext ctx, object data, 		ref HttpValidationStatus status) {
			status = data.ToString() == ctx.Request.UserAgent ?	HttpValidationStatus.Valid : HttpValidationStatus.Invalid;
			Debug.WriteLine("Cache Status: " + status);
		}
	}
}
```


## ASP.NET Identity

```cs
//IdentityConfig.cs
using Microsoft.AspNet.Identity;
using Microsoft.Owin;
using Microsoft.Owin.Security.Cookies;
using Owin;
using Users.Infrastructure;
using Microsoft.Owin.Security.Google;

namespace Users {
    public class IdentityConfig {
        public void Configuration(IAppBuilder app) {

            app.CreatePerOwinContext<AppIdentityDbContext>(AppIdentityDbContext.Create);
            app.CreatePerOwinContext<AppUserManager>(AppUserManager.Create);
            app.CreatePerOwinContext<AppRoleManager>(AppRoleManager.Create);

            app.UseCookieAuthentication(new CookieAuthenticationOptions {
                AuthenticationType = DefaultAuthenticationTypes.ApplicationCookie,
                LoginPath = new PathString("/Account/Login"),
            });

            app.UseExternalSignInCookie(DefaultAuthenticationTypes.ExternalCookie);
            app.UseGoogleAuthentication();
        }
    }
}
```

```cs
//AccountController.cs

using System.Threading.Tasks;
using System.Web.Mvc;
using Users.Models;
using Microsoft.Owin.Security;
using System.Security.Claims;
using Microsoft.AspNet.Identity;
using Microsoft.AspNet.Identity.Owin;
using Users.Infrastructure;
using System.Web;

namespace Users.Controllers {

    [Authorize]
    public class AccountController : Controller {

        [AllowAnonymous]
        public ActionResult Login(string returnUrl) {
            if (HttpContext.User.Identity.IsAuthenticated) {
                return View("Error", new string[] { "Access Denied" });
            }
            ViewBag.returnUrl = returnUrl;
            return View();
        }

        [HttpPost]
        [AllowAnonymous]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Login(LoginModel details, string returnUrl) {
            if (ModelState.IsValid) {
                AppUser user = await UserManager.FindAsync(details.Name,
                    details.Password);
                if (user == null) {
                    ModelState.AddModelError("", "Invalid name or password.");
                } else {
                    ClaimsIdentity ident = await UserManager.CreateIdentityAsync(user,
                        DefaultAuthenticationTypes.ApplicationCookie);
                    ident.AddClaims(LocationClaimsProvider.GetClaims(ident));
                    ident.AddClaims(ClaimsRoles.CreateRolesFromClaims(ident));
                    AuthManager.SignOut();
                    AuthManager.SignIn(new AuthenticationProperties {
                        IsPersistent = false
                    }, ident);
                    return Redirect(returnUrl);
                }
            }
            ViewBag.returnUrl = returnUrl;
            return View(details);
        }

        [HttpPost]
        [AllowAnonymous]
        public ActionResult GoogleLogin(string returnUrl) {
            var properties = new AuthenticationProperties {
                RedirectUri = Url.Action("GoogleLoginCallback",
                    new { returnUrl = returnUrl })
            };
            HttpContext.GetOwinContext().Authentication.Challenge(properties, "Google");
            return new HttpUnauthorizedResult();
        }

        [AllowAnonymous]
        public async Task<ActionResult> GoogleLoginCallback(string returnUrl) {
            ExternalLoginInfo loginInfo = await AuthManager.GetExternalLoginInfoAsync();
            AppUser user = await UserManager.FindAsync(loginInfo.Login);
            if (user == null) {
                user = new AppUser {
                    Email = loginInfo.Email,
                    UserName = loginInfo.DefaultUserName,
                    City = Cities.LONDON, Country = Countries.UK
                };
                IdentityResult result = await UserManager.CreateAsync(user);
                if (!result.Succeeded) {
                    return View("Error", result.Errors);
                } else {
                    result = await UserManager.AddLoginAsync(user.Id, loginInfo.Login);
                    if (!result.Succeeded) {
                        return View("Error", result.Errors);
                    }
                }
            }

            ClaimsIdentity ident = await UserManager.CreateIdentityAsync(user,
                DefaultAuthenticationTypes.ApplicationCookie);
            ident.AddClaims(loginInfo.ExternalIdentity.Claims);
            AuthManager.SignIn(new AuthenticationProperties {
                IsPersistent = false
            }, ident);

            return Redirect(returnUrl ?? "/");
        }

        [Authorize]
        public ActionResult Logout() {
            AuthManager.SignOut();
            return RedirectToAction("Index", "Home");
        }

        private IAuthenticationManager AuthManager {
            get {
                return HttpContext.GetOwinContext().Authentication;
            }
        }

        private AppUserManager UserManager {
            get {
                return HttpContext.GetOwinContext().GetUserManager<AppUserManager>();
            }
        }
    }
}
```


```cs
//AdminController.cs
using System.Web;
using System.Web.Mvc;
using Microsoft.AspNet.Identity.Owin;
using Users.Infrastructure;
using Users.Models;
using Microsoft.AspNet.Identity;
using System.Threading.Tasks;

namespace Users.Controllers {

    [Authorize(Roles = "Administrators")]
    public class AdminController : Controller {

        public ActionResult Index() {
            return View(UserManager.Users);
        }

        public ActionResult Create() {
            return View();
        }

        [HttpPost]
        public async Task<ActionResult> Create(CreateModel model) {
            if (ModelState.IsValid) {
                AppUser user = new AppUser { UserName = model.Name, Email = model.Email };
                IdentityResult result = await UserManager.CreateAsync(user,
                    model.Password);
                if (result.Succeeded) {
                    return RedirectToAction("Index");
                } else {
                    AddErrorsFromResult(result);
                }
            }
            return View(model);
        }

        [HttpPost]
        public async Task<ActionResult> Delete(string id) {
            AppUser user = await UserManager.FindByIdAsync(id);
            if (user != null) {
                IdentityResult result = await UserManager.DeleteAsync(user);
                if (result.Succeeded) {
                    return RedirectToAction("Index");
                } else {
                    return View("Error", result.Errors);
                }
            } else {
                return View("Error", new string[] { "User Not Found" });
            }
        }

        public async Task<ActionResult> Edit(string id) {
            AppUser user = await UserManager.FindByIdAsync(id);
            if (user != null) {
                return View(user);
            } else {
                return RedirectToAction("Index");
            }
        }

        [HttpPost]
        public async Task<ActionResult> Edit(string id, string email, string password) {
            AppUser user = await UserManager.FindByIdAsync(id);
            if (user != null) {
                user.Email = email;
                IdentityResult validEmail
                    = await UserManager.UserValidator.ValidateAsync(user);
                if (!validEmail.Succeeded) {
                    AddErrorsFromResult(validEmail);
                }
                IdentityResult validPass = null;
                if (password != string.Empty) {
                    validPass
                        = await UserManager.PasswordValidator.ValidateAsync(password);
                    if (validPass.Succeeded) {
                        user.PasswordHash =
                            UserManager.PasswordHasher.HashPassword(password);
                    } else {
                        AddErrorsFromResult(validPass);
                    }
                }
                if ((validEmail.Succeeded && validPass == null) || (validEmail.Succeeded
                        && password != string.Empty && validPass.Succeeded)) {
                    IdentityResult result = await UserManager.UpdateAsync(user);
                    if (result.Succeeded) {
                        return RedirectToAction("Index");
                    } else {
                        AddErrorsFromResult(result);
                    }
                }
            } else {
                ModelState.AddModelError("", "User Not Found");
            }
            return View(user);
        }

        private void AddErrorsFromResult(IdentityResult result) {
            foreach (string error in result.Errors) {
                ModelState.AddModelError("", error);
            }
        }

        private AppUserManager UserManager {
            get {
                return HttpContext.GetOwinContext().GetUserManager<AppUserManager>();
            }
        }

    }
}
```

```cs
//ClaimsController.cs
using System.Security.Claims;
using System.Web;
using System.Web.Mvc;
using Users.Infrastructure;

namespace Users.Controllers {
    public class ClaimsController : Controller {

        [Authorize]
        public ActionResult Index() {
            ClaimsIdentity ident = HttpContext.User.Identity as ClaimsIdentity;
            if (ident == null) {
                return View("Error", new string[] { "No claims available" });
            } else {
                return View(ident.Claims);
            }
        }

        [ClaimsAccess(Issuer = "RemoteClaims", ClaimType = ClaimTypes.PostalCode,
             Value = "DC 20500")]
        public string OtherAction() {
            return "This is the protected action";
        }
    }
}
```

```cs
//HomeController.cs
using System.Web.Mvc;
using System.Collections.Generic;
using System.Web;
using System.Security.Principal;
using System.Threading.Tasks;
using Users.Infrastructure;
using Microsoft.AspNet.Identity;
using Microsoft.AspNet.Identity.Owin;
using Users.Models;

namespace Users.Controllers {

    public class HomeController : Controller {

        [Authorize]
        public ActionResult Index() {
            return View(GetData("Index"));
        }

        [Authorize(Roles = "Users")]
        public ActionResult OtherAction() {
            return View("Index", GetData("OtherAction"));
        }

        private Dictionary<string, object> GetData(string actionName) {
            Dictionary<string, object> dict
                = new Dictionary<string, object>();
            dict.Add("Action", actionName);
            dict.Add("User", HttpContext.User.Identity.Name);
            dict.Add("Authenticated", HttpContext.User.Identity.IsAuthenticated);
            dict.Add("Auth Type", HttpContext.User.Identity.AuthenticationType);
            dict.Add("In Users Role", HttpContext.User.IsInRole("Users"));
            return dict;
        }

        [Authorize]
        public ActionResult UserProps() {
            return View(CurrentUser);
        }

        [Authorize]
        [HttpPost]
        public async Task<ActionResult> UserProps(Cities city) {
            AppUser user = CurrentUser;
            user.City = city;
            user.SetCountryFromCity(city);
            await UserManager.UpdateAsync(user);
            return View(user);
        }

        private AppUser CurrentUser {
            get {
                return UserManager.FindByName(HttpContext.User.Identity.Name);
            }
        }

        private AppUserManager UserManager {
            get {
                return HttpContext.GetOwinContext().GetUserManager<AppUserManager>();
            }
        }
    }
}
```


```cs
//RoleAdminController.cs
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;
using System.Linq;
using System.Threading.Tasks;
using System.Web;
using System.Web.Mvc;
using Microsoft.AspNet.Identity;
using Microsoft.AspNet.Identity.Owin;
using Users.Infrastructure;
using Users.Models;

namespace Users.Controllers {

    [Authorize(Roles = "Administrators")]
    public class RoleAdminController : Controller {

        public ActionResult Index() {
            return View(RoleManager.Roles);
        }

        public ActionResult Create() {
            return View();
        }

        [HttpPost]
        public async Task<ActionResult> Create([Required]string name) {
            if (ModelState.IsValid) {
                IdentityResult result
                    = await RoleManager.CreateAsync(new AppRole(name));
                if (result.Succeeded) {
                    return RedirectToAction("Index");
                } else {
                    AddErrorsFromResult(result);
                }
            }
            return View(name);
        }

        [HttpPost]
        public async Task<ActionResult> Delete(string id) {
            AppRole role = await RoleManager.FindByIdAsync(id);
            if (role != null) {
                IdentityResult result = await RoleManager.DeleteAsync(role);
                if (result.Succeeded) {
                    return RedirectToAction("Index");
                } else {
                    return View("Error", result.Errors);
                }
            } else {
                return View("Error", new string[] { "Role Not Found" });
            }
        }

        public async Task<ActionResult> Edit(string id) {
            AppRole role = await RoleManager.FindByIdAsync(id);
            string[] memberIDs = role.Users.Select(x => x.UserId).ToArray();
            IEnumerable<AppUser> members
                = UserManager.Users.Where(x => memberIDs.Any(y => y == x.Id));
            IEnumerable<AppUser> nonMembers = UserManager.Users.Except(members);
            return View(new RoleEditModel {
                Role = role,
                Members = members,
                NonMembers = nonMembers
            });
        }

        [HttpPost]
        public async Task<ActionResult> Edit(RoleModificationModel model) {
            IdentityResult result;
            if (ModelState.IsValid) {
                foreach (string userId in model.IdsToAdd ?? new string[] { }) {
                    result = await UserManager.AddToRoleAsync(userId, model.RoleName);
                    if (!result.Succeeded) {
                        return View("Error", result.Errors);
                    }
                }
                foreach (string userId in model.IdsToDelete ?? new string[] { }) {
                    result = await UserManager.RemoveFromRoleAsync(userId,
                        model.RoleName);
                    if (!result.Succeeded) {
                        return View("Error", result.Errors);
                    }
                }
                return RedirectToAction("Index");
            }
            return View("Error", new string[] { "Role Not Found" });
        }

        private void AddErrorsFromResult(IdentityResult result) {
            foreach (string error in result.Errors) {
                ModelState.AddModelError("", error);
            }
        }

        private AppUserManager UserManager {
            get {
                return HttpContext.GetOwinContext().GetUserManager<AppUserManager>();
            }
        }

        private AppRoleManager RoleManager {
            get {
                return HttpContext.GetOwinContext().GetUserManager<AppRoleManager>();
            }
        }
    }
}
```


```cs
//AppIdentityDbContext.cs
namespace Users.Infrastructure {
    public class AppIdentityDbContext : IdentityDbContext<AppUser> {

        public AppIdentityDbContext() : base("IdentityDb") { }

        static AppIdentityDbContext() {
            Database.SetInitializer<AppIdentityDbContext>(new IdentityDbInit());
        }

        public static AppIdentityDbContext Create() {
            return new AppIdentityDbContext();
        }
    }

    public class IdentityDbInit : NullDatabaseInitializer<AppIdentityDbContext> {
    }
}
```

```cs
//AppRoleManager.cs
namespace Users.Infrastructure {

    public class AppRoleManager : RoleManager<AppRole>, IDisposable {

        public AppRoleManager(RoleStore<AppRole> store)
            : base(store) {
        }

        public static AppRoleManager Create(
                IdentityFactoryOptions<AppRoleManager> options,
                IOwinContext context) {
            return new AppRoleManager(new
                RoleStore<AppRole>(context.Get<AppIdentityDbContext>()));
        }
    }
}
```

```cs
//AppUserManager.cs
namespace Users.Infrastructure {
    public class AppUserManager : UserManager<AppUser> {

        public AppUserManager(IUserStore<AppUser> store)
            : base(store) {
        }

        public static AppUserManager Create(
                IdentityFactoryOptions<AppUserManager> options,
                IOwinContext context) {

            AppIdentityDbContext db = context.Get<AppIdentityDbContext>();
            AppUserManager manager = new AppUserManager(new UserStore<AppUser>(db));

            manager.PasswordValidator = new CustomPasswordValidator {
                RequiredLength = 6,
                RequireNonLetterOrDigit = false,
                RequireDigit = false,
                RequireLowercase = true,
                RequireUppercase = true
            };

            //manager.UserValidator = new CustomUserValidator(manager) {
            //    AllowOnlyAlphanumericUserNames = true,
            //    RequireUniqueEmail = true
            //};

            return manager;
        }
    }
}
```

```cs
//ClaimsAccessAttribute.cs
namespace Users.Infrastructure {
    public class ClaimsAccessAttribute : AuthorizeAttribute {

        public string Issuer { get; set; }
        public string ClaimType { get; set; }
        public string Value { get; set; }

        protected override bool AuthorizeCore(HttpContextBase context) {
            return context.User.Identity.IsAuthenticated
                && context.User.Identity is ClaimsIdentity
                && ((ClaimsIdentity)context.User.Identity).HasClaim(x =>
                    x.Issuer == Issuer && x.Type == ClaimType && x.Value == Value
                );
        }
    }
}
```

```cs
//ClaimsRoles.cs
namespace Users.Infrastructure {
    public class ClaimsRoles {

        public static IEnumerable<Claim> CreateRolesFromClaims(ClaimsIdentity user) {
            List<Claim> claims = new List<Claim>();
            if (user.HasClaim(x => x.Type == ClaimTypes.StateOrProvince
                        && x.Issuer == "RemoteClaims" && x.Value == "DC")
                    && user.HasClaim(x => x.Type == ClaimTypes.Role
                        && x.Value == "Employees")) {
                claims.Add(new Claim(ClaimTypes.Role, "DCStaff"));
            }
            return claims;
        }
    }
}
```

```cs
//CustomPasswordValidator.cs
namespace Users.Infrastructure {

    public class CustomPasswordValidator : PasswordValidator {
        public override async Task<IdentityResult> ValidateAsync(string pass) {
            IdentityResult result = await base.ValidateAsync(pass);
            if (pass.Contains("12345")) {
                var errors = result.Errors.ToList();
                errors.Add("Passwords cannot contain numeric sequences");
                result = new IdentityResult(errors);
            }
            return result;
        }
    }
}
```

```cs
//CustomUserValidator.cs
namespace Users.Infrastructure {

    public class CustomUserValidator : UserValidator<AppUser> {

        public CustomUserValidator(AppUserManager mgr)
            : base(mgr) {
        }

        public override async Task<IdentityResult> ValidateAsync(AppUser user) {
            IdentityResult result = await base.ValidateAsync(user);

            if (!user.Email.ToLower().EndsWith("@example.com")) {
                var errors = result.Errors.ToList();
                errors.Add("Only example.com email addresses are allowed");
                result = new IdentityResult(errors);
            }
            return result;
        }
    }
}
```

```cs
//IdentityHelpers.cs
namespace Users.Infrastructure {
    public static class IdentityHelpers {
        public static MvcHtmlString GetUserName(this HtmlHelper html, string id) {
            AppUserManager mgr
                = HttpContext.Current.GetOwinContext().GetUserManager<AppUserManager>();
            return new MvcHtmlString(mgr.FindByIdAsync(id).Result.UserName);
        }

        public static MvcHtmlString ClaimType(this HtmlHelper html, string claimType) {
            FieldInfo[] fields = typeof(ClaimTypes).GetFields();
            foreach (FieldInfo field in fields) {
                if (field.GetValue(null).ToString() == claimType) {
                    return new MvcHtmlString(field.Name);
                }
            }
            return new MvcHtmlString(string.Format("{0}",
                claimType.Split('/', '.').Last()));
        }

    }
}
```

```cs
//LocationClaimsProvider.cs
namespace Users.Infrastructure {

    public static class LocationClaimsProvider {

        public static IEnumerable<Claim> GetClaims(ClaimsIdentity user) {
            List<Claim> claims = new List<Claim>();
            if (user.Name.ToLower() == "alice") {
                claims.Add(CreateClaim(ClaimTypes.PostalCode, "DC 20500"));
                claims.Add(CreateClaim(ClaimTypes.StateOrProvince, "DC"));
            } else {
                claims.Add(CreateClaim(ClaimTypes.PostalCode, "NY 10036"));
                claims.Add(CreateClaim(ClaimTypes.StateOrProvince, "NY"));
            }
            return claims;
        }

        private static Claim CreateClaim(string type, string value) {
            return new Claim(type, value, ClaimValueTypes.String, "RemoteClaims");
        }
    }
}
```


#### Model

```cs
//AppRole.cs

namespace Users.Models {
    public class AppRole : IdentityRole {

        public AppRole() : base() { }

        public AppRole(string name) : base(name) { }
    }
}
```

```cs
//AppUser.cs

namespace Users.Models {

    public enum Cities {
        LONDON, PARIS, CHICAGO
    }

    public enum Countries {
        NONE, UK, FRANCE, USA
    }

    public class AppUser : IdentityUser {
        public Cities City { get; set; }
        public Countries Country { get; set; }

        public void SetCountryFromCity(Cities city) {
            switch (city) {
                case Cities.LONDON:
                    Country = Countries.UK;
                    break;
                case Cities.PARIS:
                    Country = Countries.FRANCE;
                    break;
                case Cities.CHICAGO:
                    Country = Countries.USA;
                    break;
                default:
                    Country = Countries.NONE;
                    break;
            }
        }
    }
}
```

```cs
//UserViewModels.cs

namespace Users.Models {

    public class CreateModel {
        [Required]
        public string Name { get; set; }
        [Required]
        public string Email { get; set; }
        [Required]
        public string Password { get; set; }
    }

    public class LoginModel {
        [Required]
        public string Name { get; set; }
        [Required]
        public string Password { get; set; }
    }

    public class RoleEditModel {
        public AppRole Role { get; set; }
        public IEnumerable<AppUser> Members { get; set; }
        public IEnumerable<AppUser> NonMembers { get; set; }
    }

    public class RoleModificationModel {
        [Required]
        public string RoleName { get; set; }
        public string[] IdsToAdd { get; set; }
        public string[] IdsToDelete { get; set; }
    }

}
```

#### Web.Config

```cs
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <connectionStrings>
    <add name="IdentityDb" providerName="System.Data.SqlClient" connectionString="Data Source=(localdb)\v11.0;Initial Catalog=IdentityDb;Integrated Security=True;Connect Timeout=15;Encrypt=False;TrustServerCertificate=False; MultipleActiveResultSets=True" />
  </connectionStrings>

  <appSettings>
    <add key="owin:AppStartup" value="Users.IdentityConfig" />
  </appSettings>
</configuration>
```


#### View
```aspx
//Login.cshtml
@model Users.Models.LoginModel
@{ ViewBag.Title = "Login";}
<h2>Log In</h2>

@Html.ValidationSummary()

@using (Html.BeginForm()) {
    @Html.AntiForgeryToken();
    <input type="hidden" name="returnUrl" value="@ViewBag.returnUrl" />
    <div class="form-group">
        <label>Name</label>
        @Html.TextBoxFor(x => x.Name, new { @class = "form-control" })
    </div>
    <div class="form-group">
        <label>Password</label>
        @Html.PasswordFor(x => x.Password, new { @class = "form-control" })
    </div>
    <button class="btn btn-primary" type="submit">Log In</button>
}

@using (Html.BeginForm("GoogleLogin", "Account")) {
    <input type="hidden" name="returnUrl" value="@ViewBag.returnUrl" />
    <button class="btn btn-primary" type="submit">Log In via Google</button>
}
```

```aspx
//Create.cshtml
@model Users.Models.CreateModel
@{ ViewBag.Title = "Create User";}
<h2>Create User</h2>
@Html.ValidationSummary(false)
@using (Html.BeginForm()) {
    <div class="form-group">
        <label>Name</label>
        @Html.TextBoxFor(x => x.Name, new { @class = "form-control" })
    </div>
    <div class="form-group">
        <label>Email</label>
        @Html.TextBoxFor(x => x.Email, new { @class = "form-control" })
    </div>
    <div class="form-group">
        <label>Password</label>
        @Html.PasswordFor(x => x.Password, new { @class = "form-control" })
    </div>
    <button type="submit" class="btn btn-primary">Create</button>
    @Html.ActionLink("Cancel", "Index", null, new { @class = "btn btn-default" })
}
```


```aspx
//@model Users.Models.AppUser
@{ ViewBag.Title = "Edit"; }
@Html.ValidationSummary(false)
<h2>Edit User</h2>

<div class="form-group">
    <label>Name</label>
    <p class="form-control-static">@Model.Id</p>
</div>
@using (Html.BeginForm()) {
    @Html.HiddenFor(x => x.Id)
    <div class="form-group">
        <label>Email</label>
        @Html.TextBoxFor(x => x.Email, new { @class = "form-control" })
    </div>
    <div class="form-group">
        <label>Password</label>
        <input name="password" type="password" class="form-control" />
    </div>
    <button type="submit" class="btn btn-primary">Save</button>
    @Html.ActionLink("Cancel", "Index", null, new { @class = "btn btn-default" })
}
```


```aspx
Claims\Index.cshtml
@using System.Security.Claims
@using Users.Infrastructure
@model IEnumerable<Claim>
@{ ViewBag.Title = "Claims"; }

<div class="panel panel-primary">
    <div class="panel-heading">
        Claims
    </div>
    <table class="table table-striped">
        <tr>
            <th>Subject</th>
            <th>Issuer</th>
            <th>Type</th>
            <th>Value</th>
        </tr>
        @foreach (Claim claim in Model.OrderBy(x => x.Type)) {
            <tr>
                <td>@claim.Subject.Name</td>
                <td>@claim.Issuer</td>
                <td>@Html.ClaimType(claim.Type)</td>
                <td>@claim.Value</td>
            </tr>
        }
    </table>
</div>
```

```aspx
Role\edit.cshtml
@using Users.Models
@model RoleEditModel
@{ ViewBag.Title = "Edit Role";}
@Html.ValidationSummary()
@using (Html.BeginForm()) {
    <input type="hidden" name="roleName" value="@Model.Role.Name" />
    <div class="panel panel-primary">
        <div class="panel-heading">Add To @Model.Role.Name</div>
        <table class="table table-striped">
            @if (Model.NonMembers.Count() == 0) {
                <tr><td colspan="2">All Users Are Members</td></tr>
            } else {
                <tr><td>User ID</td><td>Add To Role</td></tr>
                foreach (AppUser user in Model.NonMembers) {
                    <tr>
                        <td>@user.UserName</td>
                        <td>
                            <input type="checkbox" name="IdsToAdd" value="@user.Id">
                        </td>
                    </tr>
                }
            }
        </table>
    </div>
    <div class="panel panel-primary">
        <div class="panel-heading">Remove from @Model.Role.Name</div>
        <table class="table table-striped">
            @if (Model.Members.Count() == 0) {
                <tr><td colspan="2">No Users Are Members</td></tr>
            } else {
                <tr><td>User ID</td><td>Remove From Role</td></tr>
                foreach (AppUser user in Model.Members) {
                    <tr>
                        <td>@user.UserName</td>
                        <td>
                            <input type="checkbox" name="IdsToDelete" value="@user.Id">
                        </td>
                    </tr>
                }
            }
        </table>
    </div>
    <button type="submit" class="btn btn-primary">Save</button>
    @Html.ActionLink("Cancel", "Index", null, new { @class = "btn btn-default" })
}
```

```aspx
Role\Index.cshtml
@using Users.Models
@using Users.Infrastructure
@model IEnumerable<AppRole>
@{ ViewBag.Title = "Roles"; }
<div class="panel panel-primary">
    <div class="panel-heading">Roles</div>
    <table class="table table-striped">
        <tr><th>ID</th><th>Name</th><th>Users</th><th></th></tr>
        @if (Model.Count() == 0) {
            <tr><td colspan="4" class="text-center">No Roles</td></tr>
        } else {
            foreach (AppRole role in Model) {
                <tr>
                    <td>@role.Id</td>
                    <td>@role.Name</td>
                    <td>
                        @if (role.Users == null || role.Users.Count == 0) {
                            @: No Users in Role
                        } else {
                            <p>
                                @string.Join(", ", role.Users.Select(x =>
                                Html.GetUserName(x.UserId)))
                        </p>
                        }
                    </td>
                    <td>
                        @using (Html.BeginForm("Delete", "RoleAdmin",
                            new { id = role.Id })) {
                            @Html.ActionLink("Edit", "Edit", new { id = role.Id },
                                    new { @class = "btn btn-primary btn-xs" })
                            <button class="btn btn-danger btn-xs"
                                    type="submit">
                                Delete
                            </button>
                        }
                    </td>
                </tr>
            }
        }
    </table>
</div>
@Html.ActionLink("Create", "Create", null, new { @class = "btn btn-primary" })
```

