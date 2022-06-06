---
title: "C#: A Review on Generics"
date: "2014-05-27"
categories: 
  - "c-sharp"
---

I think a good C# developer needs to get a handle on .NET generics.  Most of the advanced features in C# deal with lots of generics and having a very good understanding of generics will help considerably, most especially when dealing with generic delegates.  So here in this post, we will review generics.

_Generic type definitions_ can be methods, classes, structures, and interfaces.

// an example generic class
public class MyGenericClass<T>
{
    public T MyProperty;
}

 

 

The placeholders (e.g. **<T>**) are called _generic type parameters_, or _type parameters_.

You specify the actual types to substitute for the type parameters during instantiation.

// instantiate generic class with string type
MyGenericClass<string\> c = new MyGenericClass<string\>();

 

 

When instantiated, a generic type definition becomes a _constructed generic type_.

You can place limits or _constraints_ on generic type parameters.

// limit type to value types except Nullable
public class MyGenericClass<T> where T : struct {/*...*/}
    
// limit type to reference types which can include classes,
//  interfaces, delegates, and array types
public class MyGenericClass<T> where T : class {/*...*/}
    
// limit type to types with public parameterless constructor
// must be specified last in multiple constraints
public class MyGenericClass<T> where T : new() {/*...*/}
    
// limit type to specified base class or to types derived from it
public class MyGenericClass<T> where T : MyBaseClass {/*...*/}
    
// limit type to specified interface or to types that implement it
public class MyGenericClass<T> where T : IMyInterface {/*...*/}
    
    
// limit type to specified type parameter    
    
// in a generic member function, it limits its type to the type 
//  parameter of the containing type
public class MyGenericClass<T>
{
    void MyMethod<U>(List<U> items) where U : T {/*...*/}
}
    
// in a generic class, it enforces an inheritance relationship
//  between the two type parameters
public class MyGenericClass<T, U> where U : T {/*...*/}
    
    
// type parameter can have multiple constraints 
//  and constraints can also be generics
//  and constraints can be applied to multiple type parameters
public class MyGenericClass<T, U> 
    where T : MyClass, IMyInterface, System.IComparable<T>, new()
    where U : struct
{
    // ...
}

 

 

A method is considered a _generic method definition_ if it has two parameter lists: a list of type parameters enclosed in <> and a list of formal parameters enclosed in ().  A method belonging to a generic or non-generic type does not make the method generic or non-generic.  Only the existence of the two parameter lists will make the method generic, as in the example below.

public class MyClass
{
    // a generic method inside a non-generic class
    T MyGenericMethod<T>(T arg) {/*...*/}
}

 

 

A type nested in a generic type is considered by CLR to be generic even if it doesn’t have generic type parameters of its own.  When you instantiate a nested type, you need to specify the type arguments for all enclosing generic types.

// generic type
public class MyGenericType<T, U>
{
    // nested type
    public class MyNestedType
    {
        // ...
    }
}
    
// ... somewhere in code you instantiate the nested type   
MyGenericType<string, int\>.MyNestedType nt = 
    new MyGenericType<string, int\>.MyNestedType();

 

 

The following are some common _generic collection counterparts_ provided by the .NET framework:

- [Dictionary<TKey, TValue>](http://msdn.microsoft.com/en-us/library/xfhwa508.aspx) which is the generic version of _Hashtable_.  It uses [KeyValuePair<TKey, TValue>](http://msdn.microsoft.com/en-us/library/5tbh8a42.aspx) for enumeration instead of _DictionaryEntry_.
- [List<T>](http://msdn.microsoft.com/en-us/library/6sh2ey19.aspx) which is the generic version of _ArrayList_.
- [Queue<T>](http://msdn.microsoft.com/en-us/library/7977ey2c.aspx) and [Stack<T>](http://msdn.microsoft.com/en-us/library/3278tedw.aspx) which is the generic versions of collections with same names.
- [SortedList<TKey, TValue>](http://msdn.microsoft.com/en-us/library/ms132319.aspx) which is a hybrid of a dictionary and list, just like it’s nongeneric version of same name.
- [SortedDictionary<TKey, TValue>](http://msdn.microsoft.com/en-us/library/f7fta44c.aspx) which is a pure dictionary, and [LinkedList<T>](http://msdn.microsoft.com/en-us/library/he2s3bh7.aspx).  Both don’t have nongeneric versions.
- [Collection<T>](http://msdn.microsoft.com/en-us/library/ms132397.aspx) which is a base class for generating custom collection types, [ReadOnlyCollection<T>](http://msdn.microsoft.com/en-us/library/ms132474.aspx) which provides read-only collection from any type implementing _IList<T>_, and [KeyedCollection<TKey, TItem>](http://msdn.microsoft.com/en-us/library/ms132438.aspx) for storing objects containing their own keys.

 

There are also _generic interface counterparts_ for ordering and equality comparisons and for shared collection functionality:

- [System.IComparable<T>](http://msdn.microsoft.com/en-us/library/4d7sx9hd.aspx) and [System.IEquatable<T>](http://msdn.microsoft.com/en-us/library/ms131187.aspx) which define methods for ordering comparisons and equality comparisons.
- [IComparer<T>](http://msdn.microsoft.com/en-us/library/8ehhxeaf.aspx) and [IEqualityComparer<T>](http://msdn.microsoft.com/en-us/library/ms132151.aspx) in the _System.Collections.Generic_ namespace, which offer alternative way for types that do not implement System.IComparable<T> and System.IEquatable<T>.  They are used by methods and constructors of many of the generic collection classes.  An example would be passing a generic IComparer<T> object to the constructor of SortedDictionary<TKey, TValue> to specify a sort order.  Generic classes _Comparer<T>_ and _EqualityComparer<T>_ are their base class implementations.
- [ICollection<T>](http://msdn.microsoft.com/en-us/library/92t2ye13.aspx) which provides basic functionality for adding, removing, copying, and enumerating elements in a generic collection type.  It inherits from _IEnumerable<T>_ and the nongeneric _IEnumerable_.
- [IList<T>](http://msdn.microsoft.com/en-us/library/5y536ey6.aspx) which extends ICollection<T> with methods for indexed retrieval.
- [IDictionary<TKey, TValue>](http://msdn.microsoft.com/en-us/library/s4ys34ea.aspx) which extends ICollection<T> with methods for keyed retrieval.  Generic dictionary types also inherit from nongeneric _IDictionary_.
- [IEnumerable<T>](http://msdn.microsoft.com/en-us/library/9eekhta0.aspx) which provides a generic enumerator structure used by _foreach._  It inherits from nongeneric _IEnumerator_ because _MoveNext_ and _Reset_ methods appear only on the nongeneric interface.  This means consumer of the nongeneric interface can also consume the generic interface because the generic interface provides for nongeneric implementation.

 

You also have _generic delegates_ in .NET framework.  An example is the _EventHandler<TEventArgs>_ which you can use in handling events with custom event arguments.  No need to declare your own delegate type for the event.  If you need to brush up on events and delegates, see my post on [raising events](http://rodansotto.wordpress.com/2014/05/21/c-quick-review-on-raising-events/ "C#: Quick Review on Raising Events") and [nongeneric delegates](http://rodansotto.wordpress.com/2014/05/16/c-quick-review-on-delegates/ "C#: Quick Review on Delegates").

public event EventHandler<PublishedEventArgs> Published;

 

 

There are also a bunch of useful generic delegates available for manipulating arrays and lists

- [Action<T>](http://msdn.microsoft.com/en-us/library/018hxwa8.aspx) which allows you to perform action on an element by passing an Action<T> delegate instance and an array to the generic method [Array.ForEach<T>](http://msdn.microsoft.com/en-us/library/zecdkyw2.aspx).  You can also pass an Action<T> delegate instance to the nongeneric method [List<T>.ForEach](http://msdn.microsoft.com/en-us/library/bwabdf9z.aspx).
- [Predicate<T>](http://msdn.microsoft.com/en-us/library/bfcke1bz.aspx) which allows you to specify a search criteria to _Array_’s _Exists<T>_, _Find<T>_, _FindAll<T>_, and so on and also to _List<T>_’s _Exists_, _Find_, _FindAll_, and so on.
- [Comparsion<T>](http://msdn.microsoft.com/en-us/library/tfakywbh.aspx) which allows you to provide a sort order.
- [Converter<TInput, TOutput>](http://msdn.microsoft.com/en-us/library/kt456a2y.aspx) which allows you to convert between two types of arrays or lists.

 

Ok so that’s all we have for generics.  Just a review of the basics that a C# developer need to know.
