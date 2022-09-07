---
title: "Design Patterns: Strategy, Observer, and Decorator"
date: "2013-11-06"
categories: 
  - "design-patterns"
---

Here and in the next posts, I will talk about design patterns, it’s definition, the guiding design principles they embody, and their C# examples.  But before you dive into design patterns, here is a refresher on [four OO basics](https://rodansotto.github.io/tech-blog/2013/11/05/design-patterns-the-four-oo-basics.html).


**Design Pattern #1: Strategy Pattern**
- Defines a family of algorigthms, encapsulates each one, and makes them interchangeable.  It lets the algorithm vary independently from clients that use it.
- Design Principles:
    - _Design Principle #1_ : Separate code that change from code that stays the same
    - _Design Principle #2_ : Program to an interface and not to an implementation
    - _Design Principle #3_ : Favor composition (HAS-A) over inheritance (IS-A)
        - Note: To implement composition, a class will have an interface type reference to a concrete implementation that is usually initialized during the class constructor
- C# Examples:
    - [Basic calculation of two numbers (+,-) that can expand to any number of operators (/,*,etc.)](http://newguid.net/vs2008-vs2010/2010/design-patternsc-basic-example-strategy-pattern/)
    - [Simple shipping cost calculation that can take in different shipping methods](http://dotnetcodr.com/2013/04/29/design-patterns-and-practices-in-net-the-strategy-pattern/).  This example also shows how to implement the strategy pattern using the [delegate](http://msdn.microsoft.com/en-us/library/900fyy8e(v=vs.110).aspx) approach.
    - [Consultant search algorithm using different strategies](http://blog.lowendahl.net/design-patterns/strategy-pattern/).  It also has [delegate implementation](http://blog.lowendahl.net/design-patterns/strategy-patterns-using-delegates/).


**Design Pattern #2: Observer Pattern**
- Defines a one-to-many dependency between objects so that  when one object changes state, all of its dependents are notified and  updated automatically.  A good example is a newspaper publisher and its  subscribers.
- Design Principles:
    - _Design Principle #4_ : Strive for loosely coupled designs between objects that interact
- C# Examples:
    - [Structural C# code implementation](http://sourcemaking.com/design_patterns/observer/c-sharp-dot-net)
    - [Simple notification service when a database is down](http://dotnetanalysis.blogspot.ca/2012/07/introduction-to-observer-pattern-in-c.html)
    - [Simple investor stock price monitoring application](http://www.dotnetexamples.com/2013/08/observer-design-pattern.html)


**Design Pattern #3: Decorator Pattern**
- Attaches additional responsibilities to an object dynamically.  Decorators provide a flexible alternative to sub-classing for extending functionality.  It does this by using composition and delegation.  Decorator classes have same types as the components they decorate, either through inheritance or interface implementation.  They add behavior by adding new functionality before and/or after method calls to the component.
- Design Principles:
    - _Design Principle #5_ : Classes should be open for extension but closed for modification
- C# Examples:
    - [Crazy example about a normal dude who got super powers after a freak meteor shower](http://www.c-sharpcorner.com/UploadFile/rmcochran/csharp_wrapper302122006080905AM/csharp_wrapper3.aspx)
    - [Simple pizza ordering with add-ons such as cheese, pepper, or chicken](http://www.c-sharpcorner.com/Blogs/12993/decorator-design-pattern-in-C-Sharp.aspx)
    - [Calculating selling price of sugar after transportation cost, profit, and sales tax have been added](http://www.csharpque.com/2013/05/DecoratorPattern.html)
