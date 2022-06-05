---
title: "Multi-threading in C#: A must have in your programming arsenal (IMO)"
date: "2017-11-16"
categories: 
  - "c-sharp"
---

![](/technical-blog/assets/images/csbloglogo21.png)

You might not need to use multi-threading in all of your C# applications but as a modern software developer, you should make this part of your toolkit.

- Wikipedia best explains what [thread](https://en.wikipedia.org/wiki/Thread_(computing)) is.  It also explains the difference between threads and processes and delves into the topic of multi-threading as well, which is what thread is for.
- Benefits of using multi-threading:
    - To maintain a responsive user interface.
    - To perform CPU bound work while waiting for I/O operations to complete.
    - To scale the application using parallel execution.
- Price to pay for  using multi-threading:
    - Slower execution time on single-processor machines due to context switching.
    - Added program complexity.
- [Threading (C#)](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/threading/index) at Microsoft docs describes the basic concurrency and synchronization mechanisms provided by the .NET Framework, but not much example C# code though.
- [Threading in C# by Joseph Albahari](http://www.albahari.com/threading/) is a good one as it provides example C# code.  It goes through the basics of threading and synchronization in C# which would help you get started writing C# code.  Then it talks about the event-based asynchronous pattern (EAP) and lastly about parallel programming.
- [C# Programming Examples on Threads](http://www.sanfoundry.com/csharp-programming-examples-on-threads/) is the simplest C# codes I found on C# threading.
- Microsoft recommends using the [task-based asynchronous pattern (TAP)](https://docs.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap) though.  The [async](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/async) and [await](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/await) keywords in C# support TAP.  So I think it would be best to focus on this instead of the older patterns like the event-based asynchronous pattern (EAP) and the asynchronous programming model (APM).
- [Parallel Processing and Concurrency in the .NET Framework](https://docs.microsoft.com/en-us/dotnet/standard/parallel-processing-and-concurrency) in Microsoft docs contains links to information about threading, asynchronous programming patterns (both legacies and new) and parallel programming.
- For parallel programming, the [Task Parallel Library (TPL)](https://docs.microsoft.com/en-us/dotnet/standard/parallel-programming/task-parallel-library-tpl) is the center of it all and would be wise to get familiar on this library.
