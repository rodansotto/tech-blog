---
title: "Design Patterns: Mediator, Adapter, Proxy, and Observer Patterns"
date: "2009-04-02"
categories: 
  - "design-patterns"
---

**Mediator Pattern**

This pattern mediates between objects.  If you have several objects that need to interact with each other and you find yourself having common attributes and behaviors on each of your objects, you can use the mediator pattern.  You create a mediator object that encapsulates these common attributes and behaviors and if you need to change the way your objects interact with each other, you only have to change the mediator object.

**Adapter Pattern**

This pattern adapts an object to be usable by another object.  If you have an object A that is being used by another object B and later you upgraded object B thereby making object A unusable, you can use the adapter pattern.  You create an adapter object that fits between object A and object B and this will allow object A to remain usable by object B.

**Proxy Pattern**

This pattern allows a local code to work with a remote object all the while thinking it’s a local object.  If you have a code where you use a local object and later found yourself needing to use a remote object and you don’t want your local code to know it’s using a remote object, you can use the proxy pattern.  You create a proxy object that your local code will use and this proxy object will then connect to the remote object.

**Observer Pattern**

This pattern is about objects that are observing for a particular event to occur and waiting for the subject that they registered to to notify them when the event has occurred.  In .NET, this pattern is implemented as events or event handlers.
