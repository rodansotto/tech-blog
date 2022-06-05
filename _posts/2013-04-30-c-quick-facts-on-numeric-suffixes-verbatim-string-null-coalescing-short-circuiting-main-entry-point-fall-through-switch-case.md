---
title: "C#: Quick facts on numeric suffixes, verbatim string, null coalescing, short-circuiting, main entry point, fall through switch-case"
date: "2013-04-30"
categories: 
  - "c-sharp"
---

Use a **numeric suffix** to explicitly declare a numeric literal to be of a specific numeric type (**U** for unsigned int, **L** for long, **UL** for unsigned long, **M** for decimal, **F** for float, and **D** for double).

uint a = 123U;
long b = 1234L;
ulong c = 1234UL;
decimal d = 123.4M;
float e = 123.4F;
double f = 123.4D;

 

Use **verbatim string** (prefixed with the **@** character) if you don’t want the characters in your string translated (e.g. if you have escape sequences, etc.), except for the double quote escape sequence, as in below:

string s = @"Hello \\t ""Universe""!"; // Hello \\t "Universe"! 

 

Use **null coalescing** (**??**) if the variable you are working on can be null and you don’t want null.

int? i = null;
int j = i ?? 0;

 

Use **|** or **&** if you are not **short-circuiting**, otherwise use **||** or **&&**.  

There are actually **4 types of main entry point** in a C# program.  They are:

static void Main()
{
    // ...
}
    
static int Main()
{ 
    // ... 
    return 0; 
} 
    
static void Main(string\[\] args) 
{ 
    // ... 
} 
    
static int Main(string\[\] args) 
{ 
    // ... 
    return 0; 
}

 

There is no cascading of **case**  in **switch** which is why each case including the **default** need to have the **break**.  But you can cascade cases that have no statements, as in below.  Useful when you need to handle multiple cases in the same way.

switch (i)
{
    case 1:
    case 2:
        Console.WriteLine("1 or 2");
        break;
    default:
        break;
}
