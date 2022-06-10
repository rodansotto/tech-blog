---
title: "Design Patterns: Factory Method, Abstract Factory, and Singleton"
date: "2014-02-11"
categories: 
  - "design-patterns"
---

Back again with design patterns, defining them briefly and the design principles they are based on, and providing several very good (almost) real-world C# examples that are available on the Internet.  In this series we have the factory patterns and the singleton pattern and their several different implementations.

**Design Pattern #4: Factory Method Pattern**

- Defines an interface for creating an object but lets subclasses decide which class to instantiate.  It lets a class defer instantiation to the subclasses.

- Design Principle:
    - _Design Principle #6_ :  Depend on abstraction.  Do not depend on concrete classes.

- C# Examples:
    
    - [Example using multiple vehicle factories where each vehicle factory produces only one type of vehicle](http://www.intstrings.com/ramivemula/articles/c-design-patternfactory-method/).
        
        > <table style="font-size:.85em;" border="1" cellspacing="0" cellpadding="0" width="898"><tbody><tr><td valign="top" width="150">Product</td><td valign="top" width="746">Vehicle</td></tr><tr><td valign="top" width="150">ConcreteProduct</td><td valign="top" width="746">Bike, Car, Bus</td></tr><tr><td valign="top" width="150">Creator</td><td valign="top" width="746">Factory; with abstract method <em>GetVehicle()</em></td></tr><tr><td valign="top" width="150">ConcreteCreator</td><td valign="top" width="746">TwoWheeler, CompactFourWheeler, FourWheeler</td></tr></tbody></table>
        
    
    - [An online bookstore application using multiple distributors to send books to its customers](http://www.codeproject.com/Articles/184765/Factory-Method-Design-Pattern).  This example uses the _parameterized factory_ implementation or the _procedural solution/basic noob_ implementation, wherein the bookstore factory receives the customer location to determine which distributor to choose from.
        
        > <table style="font-size:.85em;" border="1" cellspacing="0" cellpadding="0" width="896"><tbody><tr><td valign="top" width="153">Product</td><td valign="top" width="741">IDistributor</td></tr><tr><td valign="top" width="153">ConcreteProduct</td><td valign="top" width="741">EastCoastDistributor, MidwestDistributor, WestCoastDistributor</td></tr><tr><td valign="top" width="153">Creator</td><td valign="top" width="741">IBookStore; with abstract method <em>GetDistributor()</em></td></tr><tr><td valign="top" width="153">ConcreteCreator</td><td valign="top" width="741">BookStoreA</td></tr></tbody></table>
        
    
    - [A lodging inquiry system wherein a customer can get details of different types of available rooms](http://www.codeproject.com/Articles/37547/Exploring-Factory-Pattern).  This example also shows the _registration with reflection_ implementation, the _self registration without reflection_ implementation and the _self registration with reflection_ implementation.  It is actually using a _factory pattern_, a pattern that is the basis for the _factory method pattern_ and the _abstract factory pattern_. The only difference between the factory pattern and the factory method pattern is in the creator. The factory method pattern requires an abstract class which defines the interface for several factories, thus abstracting the client from both the type of product and type of factory used to create the product.
        
        > <table style="font-size:.85em;" border="1" cellspacing="0" cellpadding="0" width="896"><tbody><tr><td valign="top" width="154">Product</td><td valign="top" width="740">IRoomType</td></tr><tr><td valign="top" width="154">ConcreteProduct</td><td valign="top" width="740">ACRoom, DeluxeRoom, NonACRoom</td></tr><tr><td valign="top" width="154">Creator</td><td valign="top" width="740">-</td></tr><tr><td valign="top" width="154">ConcreteCreator</td><td valign="top" width="740">RoomFactory; concrete class with concrete method <em>GetRoomType()</em></td></tr></tbody></table>
        

**Design Pattern #5: Abstract Factory Pattern**

- Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

- Design Principle:
    - Same as the factory method pattern, it follows the _Design Principle #6_.

- C# Examples:
    - [A drawing and printing machine that can process low and high resolution](http://gugiaji.wordpress.com/2013/01/19/abstract-factory-pattern-example-with-c/).  This can be extended to process medium resolution by creating a medium resolution factory that provides the medium resolution display and print drivers.
        
        > <table style="font-size:.85em;" border="1" cellspacing="0" cellpadding="0" width="896"><tbody><tr><td valign="top" width="154">AbstractFactory</td><td valign="top" width="738">ResFactory; with abstract methods <em>getDispDrvr()</em> and <em>getPrtDrvr()</em></td></tr><tr><td valign="top" width="154">ConcreteFactory</td><td valign="top" width="738">LowResFact, HighResFact</td></tr><tr><td valign="top" width="154">AbstractProduct</td><td valign="top" width="738">DisplayDriver, PrintDriver</td></tr><tr><td valign="top" width="154">ConcreteProduct</td><td valign="top" width="738">LowDisplayDriver, HighDisplayDriver, LowPrintDriver, HighPrintDriver</td></tr><tr><td valign="top" width="154">Client</td><td valign="top" width="738">ApControl</td></tr></tbody></table>
        
    - [An audio/video device object providing access to it’s audio and video properties](http://www.codeguru.com/csharp/.net/net_general/patterns/article.php/c4673/Abstract-Factory-Design-Pattern-Sample-in-C-and-VB-NET.htm).  Again this can be extended to include Bluray by creating a Bluray object that exposes Bluray audio and video objects.
        
        > <table style="font-size:.85em;" border="1" cellspacing="0" cellpadding="0" width="896"><tbody><tr><td valign="top" width="32">AbstractFactory</td><td valign="top" width="555">IAVDevice; with abstract methods <em>GetAudio()</em> and <em>GetVideo()</em></td></tr><tr><td valign="top" width="32">ConcreteFactory</td><td valign="top" width="555">CCd, CDvd</td></tr><tr><td valign="top" width="32">AbstractProduct</td><td valign="top" width="555">IAudio, IVideo</td></tr><tr><td valign="top" width="32">ConcreteProduct</td><td valign="top" width="555">CCdAudio, CDvdAudio, CCdVideo, CDvdVideo</td></tr><tr><td valign="top" width="32">Client</td><td valign="top" width="555">CAVMaker</td></tr></tbody></table>
        
    - [An example using employee and customer factories that provides personal information](http://blog.bekijkhet.com/2012/05/c-abstract-factory-pattern-combined.html).  This example shows the _dependency injection_ implementation and the _inversion of control container_ implementation.  These types of implementations, factory pattern, dependency injection, and inversion of control container, are all techniques to implement _inversion of control_, a programming technique in which object coupling is bound at run time and is typically not known at compile time.  I will talk more about inversion of control on a separate post, as this I think, is a hot topic too in the object oriented programming world.
        
        > <table style="font-size:.85em;" border="1" cellspacing="0" cellpadding="0" width="896"><tbody><tr><td valign="top" width="28">AbstractFactory</td><td valign="top" width="550">IPersonAbstractFactory</td></tr><tr><td valign="top" width="28">ConcreteFactory</td><td valign="top" width="550">EmployeeFactory, CustomerFactory</td></tr><tr><td valign="top" width="28">AbstractProduct</td><td valign="top" width="550">IPerson</td></tr><tr><td valign="top" width="28">ConcreteProduct</td><td valign="top" width="550">Employee, Customer</td></tr><tr><td valign="top" width="28">Client</td><td valign="top" width="550">MySample</td></tr></tbody></table>
        

**Design Pattern #6: Singleton Pattern**

- Ensures a class only has one instance and provides a global point of access to it

- C# Examples:
    
    - [Singleton implementations from MSDN](http://msdn.microsoft.com/en-us/library/ff650316.aspx).  It shows 3 implementations: the _basic_ implementation, the _static initialization_ implementation, and the _multithreaded_ or _double-check locking_ implementation.
    
    - [Singleton implementations from the book C# In Depth](http://csharpindepth.com/articles/general/singleton.aspx).  It shows 6 implementations:
        
        - basic implementation that is not thread-safe
        - simple thread-safe implementation using a lock
        - attempted thread-safe using double-check locking implementation
        - static initialization implementation that is thread-safe without using locks but not quite as lazy
        
        - full lazy static initialization implementation
        
        public sealed class Singleton  
        {  
            private Singleton()  
            {  
            }  
              
            public static Singleton Instance { get { return Nested.instance; } }  
                  
            private class Nested  
            {  
                // Explicit static constructor to tell C# compiler  
                // not to mark type as beforefieldinit  
                static Nested()  
                {  
                }  
          
                internal static readonly Singleton instance = new Singleton();  
            }  
        }
        
          
        
        - C# 4.0’s Lazy<T> static initialization implementation
        
        public sealed class Singleton  
        {  
            private static readonly Lazy<Singleton> lazy =  
                new Lazy<Singleton>(() => new Singleton());  
              
            public static Singleton Instance { get { return lazy.Value; } }  
              
            private Singleton()  
            {  
            }  
        }
        
          
        

* This is the second in the Design Patterns series.  The first one is [Design Patterns: Strategy, Observer, and Decorator](https://rodansotto.github.io/tech-blog/2013/11/05/design-patterns-strategy-observer-and-decorator.html).
