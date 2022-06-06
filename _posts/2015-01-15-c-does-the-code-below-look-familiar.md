---
title: "C#: Does the code below look familiar?"
date: "2015-01-15"
categories: 
  - "c-sharp"
---

[![extmethod]({{ site.baseurl }}/assets/images/extmethod.jpg)](https://rodansotto.files.wordpress.com/2015/01/extmethod.jpg)

If not or you are struggling to understand it, then no worries.  I too didn’t understand it fully well when I coded this, but it worked wonderfully.  I am going to break down this code into digestible parts because there is just too much.  I would suggest going through the provided links as well to fully understand each part before going to the next.

In the code, I am declaring a new extension method, named _OrderByWithDirection_, to be used as a LINQ query operation to sort elements in either ascending or descending order.  See [Standard Query Operators Overview](http://msdn.microsoft.com/en-us/library/bb397896(v=vs.100).aspx).  In LINQ query, you have separate methods for sorting in ascending order, the _OrderBy_ , and sorting in descending order, the _OrderByDescending_.  OrderByWithDirection can do both ways, so I am passing a sort direction in the third parameter:

```cs
public static IOrderedQueryable<TSource> OrderByWithDirection<TSource, TKey>( this IQueryable<TSource> query, Expression<Func<TSource, TKey>> keySelector, string sortDir) 
```

So what’s an _extension method_?  An extension method is like a static function that you can add to an existing type so you can call it from any instance of that (extended) type.  See [Extension Methods](http://msdn.microsoft.com/en-us/library/bb383977(v=vs.100).aspx) and [How to: Implement and Call a Custom Extension Method](http://msdn.microsoft.com/en-us/library/bb311042(v=vs.100).aspx).  In the code, I am making OrderByWithDirection available to any data structures that implement _IQueryable<TSource>_, which is why the first parameter to this method is of that type:

```cs
public static IOrderedQueryable<TSource> OrderByWithDirection<TSource, TKey>( this IQueryable<TSource> query, Expression<Func<TSource, TKey>> keySelector, string sortDir) 
```

Depending on the sort direction, OrderByWithDirection calls either OrderBy or OrderByDescending, both of which are actually extension methods themselves extending `IQueryable<TSource>`.  So it’s only logical that OrderByWithDirection extends the same type as well.  OrderBy and OrderByDescending are part of the _Queryable_ class, much like OrderByWithDirection is part of _ExtensionMethods_ class in the code.  See [Queryable Class](http://msdn.microsoft.com/en-us/library/system.linq.queryable(v=vs.100).aspx), [Queryable.OrderBy Method](http://msdn.microsoft.com/en-us/library/bb549264(v=vs.100).aspx), and [Queryable.OrderByDescending Method](http://msdn.microsoft.com/en-us/library/bb534316(v=vs.100).aspx).

OrderBy and OrderByDescending requires an `Expression<Func<TSource, TKey>>`, basically a function to extract a key from an element.  So in OrderByWithDirection, I am passing this function on the second parameter:

```cs
public static IOrderedQueryable<TSource> OrderByWithDirection<TSource, TKey>( this IQueryable<TSource> query, Expression<Func<TSource, TKey>> keySelector, string sortDir) 
```

To call OrderByWithDirection you would code something like this:

```cs
// products variable is of type IQueryable<Product> 
products = products.OrderByWithDirection(p => p.ProductName, "desc"); 
```

Here we are passing a lambda expression.  At first, it might look like this lambda expression is returning the product name value and not the product name key, _ProductName_.  But because we are passing this as an `Expression<Func<TSource, TKey>>`, the lambda expression is being represented as an expression tree which makes this possible.  See [Expression\<TDelegate\> Class](http://msdn.microsoft.com/en-us/library/bb335710(v=vs.100).aspx), [Func\<T, TResult\> Delegate](http://msdn.microsoft.com/en-us/library/bb549151(v=vs.100).aspx), [Expression Trees](http://msdn.microsoft.com/en-us/library/bb397951(v=vs.100).aspx), and [How to: Use Expression Trees to Build Dynamic Queries](http://msdn.microsoft.com/en-us/library/bb882637(v=vs.100).aspx).

Last but not the least, the return type.  Since OrderByWithDirection returns whatever the OrderBy or OrderByDescending returns, it’s only logical to return the same type as well, which is `IOrderedQueryable<TSource>`. See [IOrderedQueryable Interface](http://msdn.microsoft.com/en-us/library/System.Linq.IOrderedQueryable(v=vs.100).aspx).

Below is the complete code in text:

```cs
using System;
using System.Linq;
using System.Linq.Expressions;

public static class ExtensionMethods {
  public static IOrderedQueryable < TSource > OrderByWithDirection < TSource, TKey > (this IQueryable < TSource > query, Expression < Func < TSource, TKey >> keySelector, string sortDir) {
    if (sortDir.ToUpper().Equals("DESC")) {
      return query.OrderByDescending(keySelector);
    } else {
      return query.OrderBy(keySelector);
    }
  }
}
```
