---
title: "Don't confuse DIP, IoC, and DI together.  They are all different but related."
date: "2017-11-07"
categories: 
  - "design-patterns"
---

![]({{ site.baseurl }}/assets/images/dpbloglogo.png)**DIP** (or _Dependency Inversion Principle_)

 is one of the principles of SOLID.  **SOLID** stands for:

- _**S**ingle responsibility_ - a class should only have one responsibility
- _**O**pen / closed principle_ - a class should be open for extension but closed for modification
- _**L**iskov substitution principle_ - a class should be replaceable without altering the functionality of the whole
- _**I**nterface segregation principle_ - better to have more specific interfaces than a general purpose one
- _**D**ependency inversion principle_ - a higher-level class should never depend on a lower-level class, instead higher-level class should define an abstraction that lower-level class should depend on

**IoC** (or _Inversion of Control_) is a paradigm that adheres to the dependency inversion principle by inverting the control to avoid dependencies.  Most inversions can be generalized into these three types of control:

- _Control over interface_ - consumer class should have control over the interface and provider classes should depend on that interface
- _Control over flow_ - a "don't call us, we'll call you" paradigm
- _Control over creation_ - where creating objects is done outside of the class they are being used in

**DI** (or _Dependency Injection_) is one way of inverting control over creation (other ways being the factory method and the service locator).  It moves the creation and binding of a dependency outside of the class that depends on it.  [Common types of dependency injection](https://en.wikipedia.org/wiki/Dependency_injection#Three_types_of_dependency_injection):

- _Constructor injection_
- _Setter injection_
- _Interface injection_

 

**Additional Resources:**

- [S.O.L.I.D. Software Development, One Step at a Time](http://www.codemag.com/Article/1001061)
- [Developer's Guide to Dependency Injection Using Unity](https://msdn.microsoft.com/en-us/library/dn223671(v=pandp.30).aspx)
- [Dependency Injection in ASP.NET MVC 4 and WebAPI using Unity](http://netmvc.blogspot.ca/2012/04/dependency-injection-in-aspnet-mvc-4.html)
