---
title: ".NET 2.0: Addendum to Notes on Foundation Part 1"
date: "2011-05-11"
categories: 
  - "net"
---

Addendum to [.NET 2.0: Notes on Foundation Part 1](https://rodansotto.wordpress.com/2009/03/28/net-2-0-notes-on-foundation-part-1-3/)

**Value Types – Built-in, User-defined, and Enumerations**

**Built-in value types** in .NET are **sbyte**, **byte**, **short**, **int**, **uint**, **long**, **float**, **double**, **decimal**, **char**, **bool**, and **date**.  For performance, use **int** and **double** by default.  When using a nullable value type, you can use the **HasValue** method to determine if the variable has been set or not.  To get the value, use the **Value** method.

**User-defined value types** are types declared as **struct**.

\[sourcecode language="csharp" gutter="false" light="true" toolbar="false"\]
struct MyStruct
{
  ...
}
\[/sourcecode\]

They are almost identical to classes except that they are stored on stack and contain their data directly.  Use **struct** only if it represents a single value, less than 16 bytes, will not be changed after creation, and will not be cast to a reference type.

**Enumerations** are declared using **enum.**

\[sourcecode language="csharp" gutter="false" light="true" toolbar="false"\]
enum MyEnum : int { Raw, MediumRare, MediumWell, WellDone };
\[/sourcecode\]

They are used to assign names to values to improve readability and their names are displayed by default unless you type cast them.

**Operator**

Operator is new in .NET 2.0.  It allows a user-defined type to overload most of the operators provided by the language.  The example below overloads the + binary operator.

\[sourcecode language="csharp" gutter="false" light="true" toolbar="false"\]
public static MyStruct operator +(MyStruct arg1, int arg2)
{
  arg1.Value += arg2;
  return arg1;
}
\[/sourcecode\]

**Reference Types**

Reference types store the address of their data on the stack.  They are like pointers, if you’re coming from a C or C++ background.  The actual data is stored in the heap.  Since the heap is managed by the garbage collector, which recovers memory periodically, there is no need to dispose of the memory.  To trigger a garbage collection, you can call **GC.Collect()**.

The following are the most common reference types:

- **System.Object** – from which all types are derived; where **ToString()**, **GetType()**, and **Equals()** come from

- **System.String** – behaves like a value type because it overrides the **+**, **\==**, **!=**, and **\=** operators

- **System.Text.StringBuilder**

- **System.Array** – base class for all arrays

- **System.IO.Stream** – abstract base class for buffering file, device, and network I/O

- **System.Exception**

**Classes**

A class can **inherit** from one base class and can implement any number of **interface** classes.  In C#, you use the **:** (colon) symbol to indicate either an inheritance or an interface implementation, which is why it’s good practice to prefix an interface class with I as in IMyInterface.

Commonly used interfaces:

- **IComparable** – for sorting

- **IDisposable** – for  manually disposing objects that consume/lock resources such as databases

- **IConvertible** – for converting to a base type

- **ICloneable** – for copying object

- **IEquatable** – for comparing instances with **\==** operator

- **IFormattable** – for formatting string

Classes can also be declared as **partial**, allowing a class definition to be split across multiple files.

**Generic** classes allows one to specify the type for its generic types.  It reduces run-time errors and improves performance.
