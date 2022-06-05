---
title: "C#: Predicates in LINQ to Entities"
date: "2013-11-26"
categories: 
  - "c-sharp"
---

If you started programming **MVC**, in particular the **Entity Framework Model**, and find yourself filtering your data model using the **Where<TSource>()** method, you should know by now that you can chain this method instead of using the query syntax.

// using query syntax - calling Where method once  
carQuery.Where(c => c.Color == 'red' && c.Price < 10000);  
      
// using method chaining - calling Where method multiple times  
carQuery.Where(c => c.Color == 'red').Where(c => c.Price < 10000);  
      
// method chaining is useful in a loop  
foreach (KeyValuePair<string, string\> filter in filters)  
{  
    string filterVal = filter.Value;      
    switch (filter.Key)  
    {          
        case "Color":  
            carQuery = carQuery.Where(c => c.Color == filterVal).  
            break;  
        case "Price":  
            int price = Int32.Parse(filterVal);  
            carQuery = carQuery.Where(c => c.Price < price).  
            break;  
    }  
}

  

There are other ways to do predicates but  are more advance topic than the ones mentioned above.  The links below talks about them:

- [LINQ to Entities: Combining Predicates](http://blogs.msdn.com/b/meek/archive/2008/05/02/linq-to-entities-combining-predicates.aspx)
- [Dynamic LINQ Queries with Expression Trees](https://www.simple-talk.com/dotnet/.net-framework/dynamic-linq-queries-with-expression-trees/)
- [Dynamically Composing Expression Predicates](http://www.albahari.com/nutshell/predicatebuilder.aspx)
- [Giving Clarity to LINQ Queries by Extending Expressions](https://www.simple-talk.com/dotnet/.net-framework/giving-clarity-to-linq-queries-by-extending-expressions/?utm_source=simpletalk&utm_medium=pubemail&utm_campaign=reflector&utm_content=linqqueries&utm_term=reflector19)
