---
layout: post
title: "Demystifying .NET Core apps, a quick walkthrough (.NET 6)"
date: "2022-10-23"
categories: net
---

![]({{ site.baseurl }}/assets/images/netcoreapps.png)

This is just an overview of what makes **.NET Core** apps work with links pointing to a much more in-depth coverage of these concepts.  There are several types of **.NET Core** apps but this only covers the common ones, or at least those I have worked with.  Hopefully this will give you a much better understanding of the scope involved in developing **.NET Core** apps.  Let's go straight to it then.


## .NET Generic Host

[.NET Core](https://learn.microsoft.com/en-us/dotnet/core/introduction) apps uses this **.NET Generic Host** to handle the apps' resources such as:
* [Dependency Injection (DI)](https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection)
* [Logging](https://learn.microsoft.com/en-us/dotnet/core/extensions/logging?tabs=command-line)
* [Configuration](https://learn.microsoft.com/en-us/dotnet/core/extensions/configuration)
* App shutdown

They are 2 versions of this host and are created by these 2 builders:
* [HostBuilder](https://learn.microsoft.com/en-us/dotnet/core/extensions/generic-host)
* [WebApplicationBuilder](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-6.0)

**.NET Core** apps such as the [Worker Services](https://learn.microsoft.com/en-us/dotnet/core/extensions/workers) and even [Console apps](https://learn.microsoft.com/en-us/dotnet/core/tutorials/with-visual-studio-code?pivots=dotnet-6-0) use the `HostBuilder` version while [ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-6.0) apps such as [Web APIs](https://learn.microsoft.com/en-us/aspnet/core/web-api/?view=aspnetcore-6.0) and [MVC apps](https://learn.microsoft.com/en-us/aspnet/core/mvc/overview?view=aspnetcore-6.0) use the `WebApplicationBuilder` version.

Historically, this host was originally developed for **ASP.NET Core** apps but was extended for use with other types of **.NET Core** apps.

Let's look at the different **.NET Core** apps generated from templates provided in the [Visual Studio 2022 Community Edition](https://visualstudio.microsoft.com/vs/community/) and see what type of host they use and how it is used in it's basic setup.


## Console App

Here is the generated code from the `Console App` template with the usual startup code or entry point for any **.NET Core** app found in `Program.cs` file.

```c#
/* Program.cs */

// See https://aka.ms/new-console-template for more information
Console.WriteLine("Hello, World!");
```

It does not actually contain code that uses a host.  You will have to add it yourself which is not that difficult once you looked at the generated `Worker Service` code later on.

What you will notice in the code is the missing `Main` method.  This is the new form in [.NET 6](https://learn.microsoft.com/en-us/dotnet/core/whats-new/dotnet-6).  See [.NET 6 C# console app template generates top-level statements](https://learn.microsoft.com/en-us/dotnet/core/tutorials/top-level-templates) for more information on this.


## Worker Service

Here is the generated code from the `Worker Service` template:

```c#
/* Program.cs */

using WorkerService1;

IHost host = Host.CreateDefaultBuilder(args)
    .ConfigureServices(services =>
    {
        services.AddHostedService<Worker>();
    })
    .Build();

await host.RunAsync();
```

```c#
/* Worker.cs */

namespace WorkerService1
{
    public class Worker : BackgroundService
    {
        private readonly ILogger<Worker> _logger;

        public Worker(ILogger<Worker> logger)
        {
            _logger = logger;
        }

        protected override async Task ExecuteAsync(CancellationToken stoppingToken)
        {
            while (!stoppingToken.IsCancellationRequested)
            {
                _logger.LogInformation("Worker running at: {time}", DateTimeOffset.Now);
                await Task.Delay(1000, stoppingToken);
            }
        }
    }
}
```

In the `Program.cs` file,
1. the [Host.CreateDefaultBuilder()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.hosting.host.createdefaultbuilder?view=dotnet-plat-ext-6.0) returns an instance of the [HostBuilder](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.hosting.hostbuilder?view=dotnet-plat-ext-6.0) class.
2. From this host you can then add services to the (dependency injection) container via [ConfigureServices()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.hosting.hostbuilder.configureservices?view=dotnet-plat-ext-6.0#microsoft-extensions-hosting-hostbuilder-configureservices(system-action((microsoft-extensions-hosting-hostbuildercontext-microsoft-extensions-dependencyinjection-iservicecollection)))).
3. Then you register your own [implementation of an IHostedService](https://learn.microsoft.com/en-us/dotnet/core/extensions/timer-service?source=recommendations) which in this case is the `Worker` in the `Worker.cs` file via [AddHostedService\<T\>()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionhostedserviceextensions.addhostedservice?view=dotnet-plat-ext-6.0#microsoft-extensions-dependencyinjection-servicecollectionhostedserviceextensions-addhostedservice-1(microsoft-extensions-dependencyinjection-iservicecollection)).
4. Then you [Build()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.hosting.hostbuilder.build?view=dotnet-plat-ext-6.0#microsoft-extensions-hosting-hostbuilder-build) your host.
5. And lastly, call [Run()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.run?view=dotnet-plat-ext-6.0#microsoft-extensions-hosting-hostingabstractionshostextensions-run(microsoft-extensions-hosting-ihost)) or [RunAsync()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.runasync?view=dotnet-plat-ext-6.0#microsoft-extensions-hosting-hostingabstractionshostextensions-runasync(microsoft-extensions-hosting-ihost-system-threading-cancellationtoken)) on the host to run all registered hosted services, because you can have multiple hosted services running and not just one.

The `Worker.cs` file, on the otherhand, contains the `Worker` class which inherits from [BackgroundService](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.hosting.backgroundservice?view=dotnet-plat-ext-6.0) which is an implementation of an [IHostedService](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.hosting.ihostedservice?view=dotnet-plat-ext-6.0).

Note that in the constructor method of the `Worker` class, `Worker()`, is passed, or shall we say is where an [ILogger\<T\>](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.logging.ilogger-1?view=dotnet-plat-ext-6.0) implementation is injected.  This is an example of how **.NET Generic Host** provides dependency injection for services such as the basic logging provided by **.NET Core**.

Next the function [ExecuteAsync()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.hosting.backgroundservice.executeasync?view=dotnet-plat-ext-6.0) is called when the hosted service starts.  It accepts a [CancellationToken](https://learn.microsoft.com/en-us/dotnet/api/system.threading.cancellationtoken?view=net-6.0&viewFallbackFrom=dotnet-plat-ext-6.0) which means this long running operation should be cancellable.


## ASP.NET Core Web API

Here is the generated code from the `ASP.NET Core Web API` template:

```c#
/* Program.cs */

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.

builder.Services.AddControllers();
// Learn more about configuring Swagger/OpenAPI at https://aka.ms/aspnetcore/swashbuckle
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

```c#
/* WeatherForecastController.cs */

using Microsoft.AspNetCore.Mvc;

namespace ControllerWebAPI1.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class WeatherForecastController : ControllerBase
    {
        private static readonly string[] Summaries = new[]
        {
            "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
        };

        private readonly ILogger<WeatherForecastController> _logger;

        public WeatherForecastController(ILogger<WeatherForecastController> logger)
        {
            _logger = logger;
        }

        [HttpGet(Name = "GetWeatherForecast")]
        public IEnumerable<WeatherForecast> Get()
        {
            return Enumerable.Range(1, 5).Select(index => new WeatherForecast
            {
                Date = DateTime.Now.AddDays(index),
                TemperatureC = Random.Shared.Next(-20, 55),
                Summary = Summaries[Random.Shared.Next(Summaries.Length)]
            })
            .ToArray();
        }
    }
}
```

In the `Program.cs` file of an **ASP.NET Core** app such as **Web API** app,
1. the [WebApplication.CreateBuilder()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.webapplication.createbuilder?view=aspnetcore-6.0) is called to create an instance of the [WebApplicationBuilder](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.webapplicationbuilder?view=aspnetcore-6.0) class.
2. Then the following services are added into it's DI container, the [WebApplicationBuilder.Services](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.webapplicationbuilder.services?view=aspnetcore-6.0):
    1. Adds MVC services for controllers via [AddControllers()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addcontrollers?view=aspnetcore-6.0#microsoft-extensions-dependencyinjection-mvcservicecollectionextensions-addcontrollers(microsoft-extensions-dependencyinjection-iservicecollection))
    2. Configures [ApiExplorer](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.apiexplorer?view=aspnetcore-6.0) using [Endpoint's Metadata](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.endpoint.metadata?view=aspnetcore-6.0#microsoft-aspnetcore-http-endpoint-metadata) via [AddEndpointsApiExplorer()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.endpointmetadataapiexplorerservicecollectionextensions.addendpointsapiexplorer?view=aspnetcore-6.0)
    3. Adds the [Swagger](https://learn.microsoft.com/en-us/aspnet/core/tutorials/web-api-help-pages-using-swagger?view=aspnetcore-6.0) generator via `AddSwaggerGen()`.  See [Get started with Swashbuckle and ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/tutorials/getting-started-with-swashbuckle?view=aspnetcore-6.0&tabs=visual-studio).
3. Then you [Build()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.webapplicationbuilder.build?view=aspnetcore-6.0#microsoft-aspnetcore-builder-webapplicationbuilder-build) the host, the [WebApplication](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.webapplication?view=aspnetcore-6.0).
4. Next you configure the HTTP request pipeline or the middleware with the following calls:
    1. Register the Swagger middleware via `UseSwagger()`
    2. Register the SwaggerUI middleware via `UseSwaggerUI()`
    3. Adds middleware for redirecting HTTP requests to HTTPS vi [UseHttpsRedirection()](https://learn.microsoft.com/en-us/aspnet/core/security/enforcing-ssl?view=aspnetcore-6.0&tabs=visual-studio)
    4. Enables authorization capabilities via [UseAuthorization()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authorizationappbuilderextensions.useauthorization?view=aspnetcore-6.0)
    5. Adds endpoints to controller actions via [MapControllers()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.controllerendpointroutebuilderextensions.mapcontrollers?view=aspnetcore-6.0)
<br/>
See [ASP.NET Core Middleware](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-6.0) for more information of what middleware is and what other built-in middleware components came with **ASP.NET Core**.  Briefly, they replace the HTTP handlers and modules in previous **ASP.NET** versions and come with [Use](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.useextensions.use?view=aspnetcore-6.0), [Map](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.mapextensions.map?view=aspnetcore-6.0), or [Run](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.runextensions.run?view=aspnetcore-6.0) extension methods.
<br/>
5. And lastly, runs the application via [Run()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.webapplication.run?view=aspnetcore-6.0) which blocks the calling thread until host shutdown


## The Old Startup.cs
You will notice that all the configuration and setup is done in the `Program.cs` file.  Before **.NET 6**, it used to be in 2 files: `Program.cs` and `Startup.cs` and it looks something like this:

```c#
/* Program.cs */

public class Program
{
	public static void Main(string[] args)
	{
		CreateWebHostBuilder(args).Build().Run();
	}
	   
	public static IWebHostBuilder CreateWebHostBuilder(string[] args)
	{
		IConfiguration config = Configuration.CreateConfigurationContainer();

		return WebHost.CreateDefaultBuilder(args)
			.UseConfiguration(config)
			.ConfigureLogging(logging =>
			{
				logging.ClearProviders();
				logging.AddConsole();
			})
			.UseStartup<Startup>();
	}
}
```

```c#
/* Startup.cs */

public class Startup
{
	public Startup(IConfiguration configuration)
	{
		Configuration = configuration;
	}

	public IConfiguration Configuration { get; }

	// This method gets called by the runtime. Use this method to add services to the container.
	public void ConfigureServices(IServiceCollection services)
	{
		services.AddMvc()
			.SetCompatibilityVersion(CompatibilityVersion.Version_2_1);
		// etc.
	}

	// This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
	public void Configure(IApplicationBuilder app, IHostingEnvironment env)
	{
		if (env.IsDevelopment())
		{
			app.UseDeveloperExceptionPage();
		}
		else
		{
			app.UseHsts();
		}

		app.UseHttpsRedirection();
		app.UseMvc();
	}
}
```

You have the `Program.cs` file where you create the host and call [UseStartup\<TStartup\>()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup?view=aspnetcore-6.0) to use a separate file containing the startup code.

In the `Startup.cs` file, you implement the following 2 methods that are called by the runtime:
* **ConfigureServices(IServiceCollection)** - to add services to the container
* **Configure(IApplicationBuilder app, IHostingEnvironment env)** - to configure the HTTP request pipeline

As you can see there is more boilerplate code you need to add compared to the new minimal hosting model in **.NET 6**.


## Minimal API

**Minimal API** is a new type of **.NET Core** application in **.NET 6**.  You can generate the code from the same `ASP.NET Core Web API` template but unselecting the checkbox besides `Use controllers (uncheck to use minimal APIs)`.  Below is the generated code:

```c#
/* Program.cs */

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
// Learn more about configuring Swagger/OpenAPI at https://aka.ms/aspnetcore/swashbuckle
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();

var summaries = new[]
{
    "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
};

app.MapGet("/weatherforecast", () =>
{
    var forecast = Enumerable.Range(1, 5).Select(index =>
        new WeatherForecast
        (
            DateTime.Now.AddDays(index),
            Random.Shared.Next(-20, 55),
            summaries[Random.Shared.Next(summaries.Length)]
        ))
        .ToArray();
    return forecast;
})
.WithName("GetWeatherForecast");

app.Run();

internal record WeatherForecast(DateTime Date, int TemperatureC, string? Summary)
{
    public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);
}
```

So it does not have controller code like in the regular **Web API** but it makes a call to [MapGet()](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.endpointroutebuilderextensions.mapget?view=aspnetcore-6.0).  I won't go over too much on this but feel free to look at [Minimal APIs overview](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/minimal-apis?view=aspnetcore-6.0) for more information.  Also [Routing basics](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-6.0#routing-basics) in **ASP.NET Core**.


## ASP.NET Core Empty

And just to show you how many lines of code is required to get yourself a bare minimum, no content **ASP.NET Core** web application up and running, you can use the `ASP.NET Core Empty` template to generate this code for you:

```c#
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () => "Hello World!");

app.Run();
```


## Adding Host to a Console App

As previously mentioned, you need to add the **.NET Generic Host** to the console app because the generated code does not expose it.  You will need to add a NuGet package for [Microsoft.Hosting.Extensions](https://www.nuget.org/packages/Microsoft.Extensions.Hosting) before you can use the host.  See this video showing you how to do this.

<iframe width="100%" height="315" src="https://www.youtube.com/embed/I6SzqpoQ-Gw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br/>
And below is the code to use host in a console app after adding the NuGet package:

```c#
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;

var host = Host.CreateDefaultBuilder(args).Build();

// See https://aka.ms/new-console-template for more information
Console.WriteLine("Hello, World!");

var logger = host.Services.GetRequiredService<ILogger<Program>>();
logger.LogInformation("Host created.");

await host.RunAsync();
```

And as an added bonus, it also shows you how to get the host's default logger service to log messages.


## What's Next
There's still a lot more to cover but this is only part 1.  In the next part or so, I like to get more into .NET Generic Host's features such as dependency injection, logging, and configuration; some of the framework provided sevices; some of ASP.NET Core's built-in HTTP middleware like authentication and authorization; and how to create a custom HTTP middleware.


## Additional References
* [.NET documentation](https://learn.microsoft.com/en-us/dotnet/)
* [.NET Fundamentals](https://learn.microsoft.com/en-us/dotnet/fundamentals/)
* [ASP.NET documentation](https://learn.microsoft.com/en-us/aspnet/core/?view=aspnetcore-6.0)
