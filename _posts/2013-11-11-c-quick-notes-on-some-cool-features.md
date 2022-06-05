---
title: "C#: Quick notes on some cool features…"
date: "2013-11-11"
categories: 
  - "c-sharp"
---

… namely object initializer, collection initializer, implicitly typed local variable, anonymous type, anonymous method, and lambda expression.  

 **Object Initializer**

// we have here an object we are going to initialize in some other class  
public class ToDoItem  
{  
    // the following are the auto-implemented or automatic properties  
    public int ToDoItemID { get; set; }  
    public string Description { get; set; }  
    public DateTime DueDate { get; set; }  
    public string Notes { get; set; }  
}  
      
public class SomeOtherClass  
{  
    //...  
    private void someMethod()  
    {  
        // so below we use the object initializer, enclosed by {}, to set the object's  
        //  properties at creation time without having to define a corresponding   
        //  constructor  
        // it uses the default constructor to process the the object initializers  
        ToDoItem toDoItem = new ToDoItem   
        {   
            Description = "Attend French class",   
            DueDate = DateTime.Parse("11/7/2013"),   
            Notes = "@6:30p"   
        };  
    }  
}  

  

 

**Collection Initializer**

// collection initializer lets you specify one or more element initializers  
//  which can be a simple value, an expression or an object initializer  
      
// initializing a list of ints using simple values  
List<int\> intList = new List<int\> { 1, 2, 3, 4, 5 };  
      
// initializing a list of to do items using object initializers  
List<ToDoItem> toDoList = new List<ToDoItem>   
{   
    new ToDoItem { Description = "Visit Milton", ..., Notes = "" },   
    new ToDoItem { Description = "Attend French class", ..., Notes = "@6:30p" },   
    new ToDoItem { Description = "Attend Adv JavaScript class", ..., Notes = "@1p" }   
};  

  

 

**Implicitly Typed Local Variable**

// implicitly typed local variable, whose type is determined at compile time, is declared  
//  using the var keyword  
var x = 10;  
int y = 10; // explicitly typed

  

 

**Anonymous Type**

// anonymous types are objects created with read-only properties and without explicit   
//  type  
// they are created using the new operator with an object initializer and assigned to a  
//  variable declared as var  
var t = new  
{  
    Description = "Attend French class",  
    DueDate = DateTime.Parse("11/7/2013"),  
    Notes = "@6:30p"  
};  
      
// they are typically used in the select clause of a LINQ query expression  
var toDoQuery =  
    from toDo in toDoList  
    select new {toDo.Description, toDo.DueDate};  
foreach (var t in toDoQuery)  
{  
    Console.WriteLine(t.Description);  
    Console.WriteLine(t.DueDate);  
}  

  

 

**Anonymous Method**

// anonymous method is another way of initializing a delegate  
// before anonymous method, delegates are initialized with named method that is declared  
//  elsewhere in the code  
// with anonymous method, delegates can now be initialized inline as in below  
      
// first declare the delegate  
delegate void IntOpDelegate(int i, int j);  
      
private void DoIntOps()  
{  
    // then instantiate the delegate with unnamed inline statement block called the  
    //  anonymous method  
    IntOpDelegate intOpSum = delegate(int i, int j)  
    {  
        Console.WriteLine("Sum: {0}", i + j);  
    };  
      
    IntOpDelegate intOpDiff = delegate(int i, int j)  
    {  
        Console.WriteLine("Diff: {0}", Math.Abs(i - j));  
    };  
      
    // lastly, invoke the delegates  
    intOpSum(2, 3);  
    intOpDiff(4, 9);  
}  

  

 

**Lambda Expression**

// lambda expression uses => as the lambda operator  
// left side of => contains the input parameter(s) and right side of => contains the  
//  statement(s) or expression  
      
// example below is using lambda expression in place of anonymous method in our previous  
//  example  
// the right side of => contains one statement  
// note that our delegate here does not return a value so the statement should not return  
//  any value  
IntOpDelegate intOpSum2 = (i, j) => Console.WriteLine("Sum: {0}", i + j);  
intOpSum2(2, 3);  
      
// a lambda expression example with only 1 input parameter, hence () is not required  
IntUnaryOpDelegate intOpInc = i => Console.WriteLine("Increment: {0}", i++);  
intOpInc(4);  
      
// a lambda expression example with statements enclosed in {} on the right side of =>  
IntUnaryOpDelegate intOpInc2 = i =>   
{  
    Console.Write("Increment: ");   
    Console.WriteLine(i++);   
};  
intOpInc2(4);  
      
// here the delegate returns a value so the right side of => contains an expression  
// when you say expression it usually returns a value  
IntUnaryOpDelegateWithRetVal intOpInc3 = i => i++;  
Console.WriteLine("Increment: {0}", intOpInc3(4));  
      
// you can also use statements in place of an expression as in below, but expression is  
//  more elegant  
IntUnaryOpDelegateWithRetVal intOpInc4 = i => { return i++; };  
Console.WriteLine("Increment: {0}", intOpInc4(4));
