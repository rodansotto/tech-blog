---
layout: post
title: "Ways Developer Can Secure An ASP.NET Application (Redux 2022)"
date: "2022-12-13"
categories: asp-net
---


![]({{ site.baseurl }}/assets/images/secureaspnetlogo.png)


Updating my post back in 2015 [here](/tech-blog/2015/11/02/ways-developer-can-secure-an-asp-net-application-part-1.html) for year 2022.


## Cross-Site Scripting (XSS)

- According to [OWASP's definition of XSS](https://owasp.org/www-community/attacks/xss/), XSS is a type of injection that occurs when a web application uses input from a user within the output it generates without validating or encoding it

- To avoid XSS in ASP.NET, use [Razor's expression syntax](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/razor?view=aspnetcore-7.0#expression-encoding) with the `@` symbol preceeding variable names, e.g. `@InputString`, as this will escape HTML characters in the input string by default

    For example the following code:

    ```
    @("<span>Hello World</span>")
    ```

    will render the following HTML:
    
    ```
    &lt;span&gt;Hello World&lt;/span&gt;
    ```

- Use the [HttpUtility.HtmlEncode()](https://learn.microsoft.com/en-us/dotnet/api/system.web.httputility.htmlencode?view=net-7.0) function inside your Razor code:

    ```
    <%= HttpUtility.HtmlEncode(UserInput) %>
    ```

- Avoid using [HtmlHelper.Raw()](https://learn.microsoft.com/en-us/dotnet/api/system.web.mvc.htmlhelper.raw?view=aspnet-mvc-5.2), unless you validate and sanitize the input string variable


## Same Origin Policy and Cross Origin Resource Sharing (CORS)

- According to [MDN's definition of same origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy#:~:text=The%20same%2Dorigin%20policy%20is,documents%2C%20reducing%20possible%20attack%20vectors.), same origin policy restricts how a document or script loaded by one origin can interact with a resource from another origin

- 2 URLs have different origin if any of the following is different:
    - protocol (`http` vs `https`)
    - domain (`https://my-site.com` vs `https://www.my-site.com`)
    - port (`:443` vs `:5000`)

<p></p>
- CORS on the other hand, according to [OWASP's definition of CORS](https://owasp.org/www-community/attacks/CORS_OriginHeaderScrutiny), allows a web application to expose resources to all or restricted domain and allows a web client to make AJAX request for resource on other domain than its source domain

- The process involves the browser sending the [Origin](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Origin) HTTP request header (with origin URL as its value) for cross domain request to the server.  The server then sending the [Access-Control-Allow-Origin](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Access-Control-Allow-Origin) HTTP response header (with origin URL as its value) to allow CORS.  Then lastly the browser checking if URL in `Access-Control-Allow-Origin` header matches the origin URL.

- To enable CORS per endpoint in ASP.NET:
	- Use [[EnableCors]](https://learn.microsoft.com/en-us/aspnet/core/security/cors?view=aspnetcore-7.0#attr) attribute at the controller level
	- And call [CorsHttpConfigurationExtensions.EnableCors()](https://learn.microsoft.com/en-us/aspnet/web-api/overview/security/enabling-cross-origin-requests-in-web-api#enable-cors) on startup/configuration

<p></p>
- You can enable CORS in `web.config` using [\<customHeaders\>](https://learn.microsoft.com/en-us/iis/configuration/system.webserver/httpprotocol/customheaders/) but this will apply for all requests:

    ```xml    
	<system.webServer>
        <httpProtocol>
            <customHeaders>
                <add name="Access-Control-Allow-Origin" value="https://..." />
            </customHeaders>
        </httpProtocol>
    </system.webServer>
    ```


## SQL Injection

- Avoid concatenating user input to SQL query statements

- Use parameterized query or prepared statements

    In your SQL query use [SQL variables](https://learn.microsoft.com/en-us/sql/t-sql/language-elements/variables-transact-sql?view=sql-server-ver16):

    ```sql
	SELECT * FROM product WHERE id = @id
    ```

    And in your ASP.NET code, use [SQL command parameters](https://learn.microsoft.com/en-us/dotnet/api/system.data.sqlclient.sqlcommand.parameters?view=dotnet-plat-ext-7.0):

    ```c#
	command.Parameters.AddWithValue("@id", id);
    ```

- Additionally validate user input

- Avoid execution of raw SQL even in Entity Framework 6 (EF6) - EF6 calls such as as [Database.SqlQuery()](https://learn.microsoft.com/en-us/dotnet/api/system.data.entity.database.sqlquery?view=entity-framework-6.2.0) and [Database.ExecuteSqlCommand()](https://learn.microsoft.com/en-us/dotnet/api/system.data.entity.database.executesqlcommand?view=entity-framework-6.2.0)

- For Entity Framework Core (EF Core), see [Passing parameters in EF Core](https://learn.microsoft.com/en-us/ef/core/querying/sql-queries#passing-parameters)

- Also, avoid returning [IQueryable](https://learn.microsoft.com/en-us/dotnet/api/system.linq.iqueryable?view=net-7.0) in EF and instead call [ToList()](https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.tolist?view=net-7.0) before returning results


## Cross-Site Request Forgery (CSRF)

- According to [OWASP's definition of CSRF](https://owasp.org/www-community/attacks/csrf), CSRF forces an end user to execute unwanted actions on a web application in which they are currently authenticated.

- An example of CSRF is luring a user to visit the attacker's site where the attacker is able to send an authenticated HTTP request to the server being attacked that the user has previously logged in

- To prevent CSRF in ASP.NET, antiforgery tokens are used and they work because the malicious page cannot read the user's tokens, due to same-origin policies

    Use [HtmlHelper.AntiForgeryToken()](https://learn.microsoft.com/en-us/dotnet/api/system.web.mvc.htmlhelper.antiforgerytoken?view=aspnet-mvc-5.2) to add antiforgery token to a `<form>` element:

    ```c#
	@using (Html.BeginForm("DeleteProduct", "Admin")) {
		@Html.AntiForgeryToken()
        ...
	}
    ```

    And add the [[ValidateAntiForgeryToken]](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.validateantiforgerytokenattribute?view=aspnetcore-7.0) attribute to the controller action:

	```c#
	[HttpPost]
	[ValidateAntiForgeryToken]
	public ActionResult DeleteProduct(...)
    {
        ...
    }
    ```

- For ASP.NET Core, see [Prevent Cross-Site Request Forgery (XSRF/CSRF) attacks in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/security/anti-request-forgery?view=aspnetcore-7.0)


## Web.config

- ASP.NET or specifically IIS by default forbids downloading the `web.config` file via HTTP as this is configured in it's config under [\<system.web\>/\<httpHandlers\>](https://learn.microsoft.com/en-us/previous-versions/dotnet/netframework-4.0/bya7fh0a(v=vs.100)):

    ```xml
    <system.web>
        <httpHandlers>
            <add verb="*" path="*.config" type="System.Web.HttpForbiddenHandler" />
        </httpHandlers>
    </system.web>
    ```

- But still it should not contain sensitive information as this `web.config` file can be stored in the project's source control repository

- You can store your app settings and connections strings in an external file which you can refer to in your `web.config` (see [\<appSettings\> file](https://learn.microsoft.com/en-us/dotnet/framework/configure-apps/file-schema/appsettings/appsettings-element-for-configuration#attribute) attribute and [\<connectionStrings\> configSource](https://learn.microsoft.com/en-us/dotnet/framework/data/adonet/connection-strings-and-configuration-files)  attribute):

```xml
    <appSettings file="secrets.appSettings.config">
        ...
    </appSettings>
```

```xml
    <connectionStrings configSource="secrets.connectionStrings.config">
    </connectionStrings>
```

- Encrypt sections of your `web.config` file (see [Encrypting and Decrypting Configuration Sections](https://learn.microsoft.com/en-us/previous-versions/aspnet/zhhddkxy(v=vs.100)))

- If you are using a cloud provider, use the [Key Vault in Azure](https://learn.microsoft.com/en-us/azure/key-vault/general/basic-concepts) or [Secrets Manager in AWS](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) to store sensitive information


## Password Hashing

- You can use [Rfc2898DeriveBytes](https://learn.microsoft.com/en-us/dotnet/api/system.security.cryptography.rfc2898derivebytes?view=net-7.0) to hash password

- Or use [ASP.NET Core Identity PasswordHasher](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.identity.passwordhasher-1?view=aspnetcore-7.0) (see [Exploring the ASP.NET Core Identity PasswordHasher](https://andrewlock.net/exploring-the-asp-net-core-identity-passwordhasher/))


## Cookies

- Secure cookies in ASP.NET code (see [HttpCookie Class](https://learn.microsoft.com/en-us/dotnet/api/system.web.httpcookie?view=netframework-4.8)) by setting the following properties:
    - [Secure](https://owasp.org/www-community/controls/SecureCookieAttribute) - set to `true` to only transmit cookie using SSL, that is over HTTPS
    - [HttpOnly](https://owasp.org/www-community/HttpOnly) - set to `true` to prevent client-side script from accessing the cookie
    - [SameSite](https://owasp.org/www-community/SameSite) - set to `strict` to prevent cookie from being sent in all cross-site browsing contexts or set to `lax` for a more balanced approach between security and usability

    <p></p>
    ```c#
    cookie = new HttpCookie("NewCookie");
    cookie.Secure = true;
    cookie.HttpOnly = true;
    cookie.SameSite = SameSiteMode.Strict // or SameSiteMode.Lax
    ```


## Sessions

- Secure sessions by setting properties in `web.config` under `<system.web>/<sessionState>` (see [SessionStateSection Class](https://learn.microsoft.com/en-us/dotnet/api/system.web.configuration.sessionstatesection?view=netframework-4.8)) and `<system.web>/<httpCookies>` (see [HttpCookiesSection Class](https://learn.microsoft.com/en-us/dotnet/api/system.web.configuration.httpcookiessection?view=netframework-4.8)):

    ```xml
	<system.web>
		<sessionState
			cookieless="false"
			regenerateExpiredSessionId="false"
			timeout="20"
		/>
		<httpCookies
			httpOnlyCookies="true"
			requireSSL="true"
			sameSite="Strict"
		/>
	</system.web>
    ```

- Setting `<sessionState> cookieless` attribute to `false` will prevent encoding the session ID in the URL which is prone to a security attack and instead use a cookie to store the session ID

- Setting `<sessionState> regenerateExpiredSessionId` attribute to `false` will prevent using the same session ID value when expired

- Setting a `<sessionState> timeout` is recommended to prevent a session running too long which make it more vulnerable to security attack


## Enforce HTTPS

- Enforce HTTPS in ASP.NET code by redirecting after checking [HttpRequest.IsSecureConnection](https://learn.microsoft.com/en-us/dotnet/api/system.web.httprequest.issecureconnection?view=netframework-4.8):

    ```c#
   if (!HttpContext.Current.Request.IsSecureConnection)
   {
        Response.Redirect("https://" + Request.ServerVariables["HTTP_HOST"] + HttpContext.Current.Request.RawUrl);
   }    
    ```

- You can add a rewrite rule in `web.config`:

    ```xml
    <system.webServer>
        <rewrite>
            <rules>
                <rule name="HTTP to HTTPS redirect" stopProcessing="true"> 
                    <match url="(.*)" /> 
                    <conditions> 
                        <add input="{HTTPS}" pattern="off" ignoreCase="true" />
                    </conditions> 
                    <action type="Redirect" redirectType="Permanent" url="https://{HTTP_HOST}/{R:1}" />
                </rule> 
            </rules>
        </rewrite>
    </system.webServer>
    ```

- Or you can add the HTTP [Strict-Transport-Security (HSTS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security) header to the response

- For ASP.NET Core, see [Enforce HTTPS in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/security/enforcing-ssl?view=aspnetcore-7.0&tabs=visual-studio) for information on `UseHttpsRedirection()` and `UseHsts()`


## Error handling

- Having a custom error page allows you to tailor your error messages from displaying too much information or from displaying sensitive information that can lead to a security attack

- In ASP.NET, you can add custom error handler in `Global.asax` file under `Application_Error()`:

    ```c#
    protected void Application_Error(object sender, EventArgs e)
    {
        Exception exception = Server.GetLastError();
        System.Diagnostics.Debug.WriteLine(exception);
        Response.Redirect("/Home/Error");
    }  
    ```

- You can configure custom error messages/pages in `web.config`

    For example you can add this to your `web.config` file:

    ```xml
	<customErrors mode="On">
		<error statusCode="404" redirect="~/Home/MyCustomErrorPage" />
	</customErrors>
    ```

	Then in your `HomeController` code, you would have this method defined:

    ```c#
	public ActionResult MyCustomErrorPage(...)
    {
        ...
    }
    ```

    And of course the corresponding view file `MyCustomErrorPage.cshtml` should have been created as well


## OWASP Links
- [OWASP Top 10 2021](https://owasp.org/Top10/)
- [OWASP Top 10 2017](https://owasp.org/www-project-top-ten/2017/)
