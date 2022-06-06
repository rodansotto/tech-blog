---
title: "Ways to Extend The ASP.NET MVC 5 Framework"
date: "2017-11-03"
categories: 
  - "asp-net-mvc"
---

![]({{ site.baseurl }}/assets/images/mvcbloglogo.png)



ASP.NET MVC 5 Framework does not limit you to the capabilities it provide out of the box.  It is an extensible framework which emphasizes on convention over configuration or coding by convention, and below are some ways you can extend it.

- [Action Results](http://www.c-sharpcorner.com/UploadFile/db2972/custom-action-result-sample-in-mvc-day-36/)
    - Action results are returned by the controller (e.g. _return View()_).
    - They are responsible for writing response to a request.
    - They are executed internally by MVC to write out the response.
    - You can create a custom action result by inheriting from _ActionResult_ and overriding _ExecuteResult()_, or by extending an existing action result (e.g. _FileResult_).
- [Action Filters](https://docs.microsoft.com/en-us/aspnet/mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters)
    - Action filters execute before and after a controller action method.
    - You can create a custom action filter by implementing _ActionFilter_'s _OnActionExecuting()_ and _OnActionExecuted()_ methods.
    - They can be applied at the method, controller, or global scope.
- [Helper Methods](http://www.c-sharpcorner.com/article/custom-html-helper-in-Asp-Net-mvc/)
    - Two types: inline Razor helpers (_@helper_) and HTML helpers (_@Html.*_).
    - They reduce code duplication but if it involves complex logic consider using partial view / child action method.
    - You can create your own HTML helper by creating an extension method to _HTMLHelper_.
- [View Engines](http://marisks.net/2017/02/03/razor-view-engine-for-feature-folders/)
    - When controller returns a view, the MVC executes the action result and in the process uses a view engine to find a view and returns a _ViewEngineResult_ whose _Render()_ method is called.
    - A custom view engine can be used to extend view selection functionality such as to implement swappable UI themes (e.g. Wordpress themes).
    - You create a custom view engine by extending the _RazorViewEngine_ and in the constructor setting the search location format properties to use the theme directories that you want the view engine to search for for the currently active theme.
    - You register the custom view engine in _Application_Start()_ calling _ViewEngines.Engines.Insert()_, inserting it as the first engine to be evaluated.  You can leave the _RazorViewEngine_ there if you want a fallback.  Note that MVC supports multiple view engines.
- [Exception Filters](http://www.tutorialsteacher.com/mvc/filters-in-asp.net-mvc)
    - Exception filters catch errors that occur inside the scope of action method execution (including inside action filters and action results) and thus provide more contextual framework information.
    - The default exception filter in MVC is the _HandleErrorAttribute_.
    - You can create a custom exception filter by implementing the _IExceptionFilter_'s _OnException()_.
    - They can be applied at the method, controller, or global scope.
    - The _ExceptionHandled_ flag is useful when using multiple exception filters: checking to make sure exception was not handled by previous exception filter before continuing.
    - _Application_Error()_ should still be implemented as a fallback.
- [Server-Side Validations](http://prideparrot.com/blog/archive/2012/4/model_validation_in_asp_net_mvc)
    - Two ways: via data attributes (e.g. _Required_, _Range_, etc.) and implementation of _IValidatableObject_'s _Validate()_ in the model class, the former being reusable while the latter providing easy cross property validation.
    - The model binder that binds the request data to the model classes (or the action method parameters) checks the data attributes first then the _Validate()_ and populates the controller's _ModelState_ property which you can check if any errors occurred in the model binding process (e.g. _ModelState.IsValid_).
    - You can create a custom data attribute by inheriting from _ValidationAttribute_ and overriding _IsValid()_ and setting the _ErrorMessage_ in the constructor.
    - You can implement the _IValidatableObject_'s _Validate()_ in the model class and return _List_ containing any error messages.
- [Model Binders](http://www.dotnetcurry.com/aspnet-mvc/1261/custom-model-binder-aspnet-mvc)
    - A model binder implements the _IModelBinder_'s _BindModel()_.  The binder model is returned by a model binder provider that implements _IModelBinderProvider_'s _GetBinder_().  The model binding process searches through a list of model binder providers asking them if they can provide a model binder for the data it is trying to bind.
    - You can create a custom model binder by implementing _IModelBinder_'s _BindModel_() and adding any error messages to the controller's _ModelState_.  Then you create a custom model binder provider by implementing _IModelBinderProvider_'s _GetBinder_() to return the custom model binder you just created.  You register your custom model binder provider in _Application_Start_() by calling _ModelBinderProviders.BinderProviders.Insert()_.
- [Value Providers](http://www.c-sharpcorner.com/UploadFile/97fc7a/smart-working-with-custom-value-providers-in-Asp-Net-mvc/)
    - A model binder employs value providers to provide it data from different sources such as posted form data, query string, route data, etc. that it can use to populate the action method parameters.
    - Possible uses of a custom value provider is to provide HTTP header data or settings from configuration file or database.
    - You create a custom value provider by implementing _IValueProvider_'s two methods: _ContainsPrefix()_ to return true if the passed in property name matches any data the custom value provider provides and _GetValue()_ to return the value itself.  Then you create a custom value provider factory by inheriting from _ValueProviderFactory_ and overriding _GetValueProvider()_ to return the custom value provider you just created.  You register your custom value provider factory in _Application_Start()_ by calling _ValueProviderFactories.Factories.Insert()_.
- [Authentication Filters](http://www.dotnetfunda.com/articles/show/2935/creating-custom-authentication-filter-in-aspnet-mvc) and Authorization Filters
    - Authentication filters implement _IAuthenticationFilter_'s two methods: _OnAuthentication_() to authenticate a request and _OnAuthenticationChallenge_() that runs when authentication fails and right after action method execution.
    - Authorization filters implement _IAuthorizationFilter_'s _OnAuthorization()_.
    - These filters return a non-null context results if authentication/authorization fails.
    - Note that MVC supports Forms and Windows authentication by default and does not support Basic authentication.  One use of a custom authentication filter is to provide Basic authentication.
    - You create a custom authentication filter by implementing _IAuthenticationFilter_.  For custom authorization filter, consider inheriting from _AuthorizeAttribute_ instead.
- Action Name Selectors and [Action Method Selectors](http://www.tutorialsteacher.com/articles/define-custom-action-selector-in-mvc)
    - Action name selectors (e.g. _\[ActionName("xxxxx")\]_) and action method selectors (e.g. _\[HttpGet\]_ and _\[HttpPost\]_) influence the decision process of selecting which action method to handle the request by the action invoker.
    - You can create a custom action name selector by inheriting from _ActionNameSelectorAttribute_ and overriding _IsValidName()_.
    - You can create a custom action method selector by inheriting from _ActionMethodSelectorAttribute_ and overriding _IsValidForRequest()_.

 

**Additional References:**

- [ASP.NET MVC 5 Application Lifecycle Diagram](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application) - this will give you an idea how MVC 5 works
- [A look inside MVC](http://beletsky.net/blog/categories/insidemvc/) - a deep dive inside MVC (older version), but still worth taking a look
- [MVC 5 Source Code](https://github.com/aspnet/AspNetWebStack) - if you're up to it why not pull the source code from GitHub

 

**BONUS:** Found this good article worth looking too: [10 ways to extend your Razor views in ASP.​NET core - the complete overview](http://asp.net-hacker.rocks/2016/02/18/extending-razor-views.html).
