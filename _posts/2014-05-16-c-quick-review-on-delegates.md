---
title: "C#: Quick Review on Delegates"
date: "2014-05-16"
categories: 
  - "c-sharp"
---

A **delegate** is a type, much like the **C/C++ function pointer**, that can reference or encapsulate any method with the same method signature as the delegate.

Declaring a delegate is like declaring a regular method but without the method body and using the _delegate_ keyword.

// declaring a delegate that accepts string as input and returns void
public delegate void MyDelegate(string msg);
    
// declaring a method with similar method signature as the delegate
public static void MyDelegateMethod(string msg)
{
    Console.WriteLine(msg);
}
    
// instantiating the delegate
MyDelegate d = MyDelegateMethod;
    
// calling the delegate
d("Hello Delegate!!!");

 

 

The instantiated delegate is an object, and as such can be passed as a parameter or assigned to a property.

// here is a method accepting a delegate as a parameter
// the delegate parameter is often called the callback method
public static void PassMeTheDelegate(MyDelegate callBack)
{
    callBack("Passed as a parameter");
}
    
// passing the instantiated delegate as a parameter to another method
// basically passing a callback method to another method
PassMeTheDelegate(d);
    
// assigning the instantiated delegate to another variable
MyDelegate v = d;
v("Assigned to a variable");

 

 

A delegate can call more than one method when invoked and this is referred to as _multicasting_, a feature extensively used in _event handling_.

// instantiate another delegate,
//  encapsulating another method with same method signature
MyDelegate e = MyDelegateMethod2;
    
// to multicast, add the delegates using the addition operator
MyDelegate multiCast = d + e;
    
// invoking a multicast delegate will invoke 
//  each of the delegate methods in the invocation list
multiCast("I am multicasting!");
    
// and you can also remove a method from the invocation list
multiCast -= d;
multiCast("Now I am not");

 

 

Because delegates are derived from [System.Delegate](http://msdn.microsoft.com/en-us/library/system.delegate.aspx), you can call the methods and properties defined by that class on the delegate.  Multicast delegates or delegates with more than one method in their invocation list derive from [MulticastDelegate](http://msdn.microsoft.com/en-us/library/system.multicastdelegate.aspx), which is a subclass of System.Delegate.

So far we have instantiated a delegate using a named method, where the method is defined elsewhere.  Another way of instantiating a delegate is with _anonymous methods_ and _lambda expressions_, both are forms of inline code that you can pass as parameter or assign to property in place of a named method, except that lambda expressions are more concise.  Check out my post [here](https://rodansotto.github.io/tech-blog/2013/11/11/c-quick-notes-on-some-cool-features.html "C#: Quick notes on some cool features…") on anonymous methods and lambda expressions.
