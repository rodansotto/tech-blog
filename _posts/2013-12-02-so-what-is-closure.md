---
title: "So what is Closure?"
date: "2013-12-02"
categories: 
  - "c-sharp"
  - "javascript"
---

I’m not talking about closure in a relationship :).  I am talking about closure in programming.  I first encountered closure in JavaScript the hard way.  I was debugging for days the following code as to why it was not behaving the way I expect it to be.

```js
var setRowsOnclickEvent = function () {
    var table = $("tableList");
    
    for (var i = 1; i < table.rows.length; i++) {
        var row = table.rows[i];
        
        row.onclick = function () {
            var table = $("tableList");
            
            for (var j = 1; j < table.rows.length; j++) {
                var row = table.rows[j];
                
                if (j == i) {
                    row.className = "selectRow";
                }
                else {
                    row.className = "unselectRow";
                }
            }
        }
    }
}
```

The JavaScript function above is setting the onclick event of all the rows in the table.  It iterates through each row in the table and assigns an inline function, an event handler, to the row’s onclick event.  Note that the event handler, or the inner function, uses the loop variable i of the outer function, containing the row number, so that whenever the row is clicked it get’s highlighted.

My mistake was to think that the value of i is passed on to the event handler like a function parameter and placed on the stack.  Don’t make that mistake. The value of i actually closes on you, I mean on the event handler, or the inner function.  So variable i is a closure variable, while the inner function is a closure function.

Again don’t make the mistake that assigning the event handler to the onclick event actually calls the event handler.  It’s an event handler so it can be called even after the outer function has been out of scope.

So you ask, what happens to the value of i then? Well for closure situations like this, the compiler creates a special context object containing the closure variables so that closure functions, when they get executed, will have access to these variables even if the function that the closure variables are declared in are already out of scope.

In the above JavaScript code, what’s happening is whenever any row is clicked, the last row always gets highlighted, so which is to say, the variable i always has the value of the last row number.  The reason is because, again, even if the closure function, or the event handler in our example, is inside a loop that iterates through each row and incrementing the closure variable i, when the loop exits, the closure variable i will contain the last value in the loop which is the last row number and that is the value that the event handler will get when it gets executed at a later time.  So the value of the closure variable i will be the value at runtime and not at capture time, or in our example, not at the time when the event handler is declared and assigned.

Below is my solution to the JavaScript code above.  The solution is to wrap the event handler in another function where I pass in i as a function parameter, thereby forcing the compiler to capture the value of i as it increments itself inside the loop.

```js
var setRowsOnclickEvent = function () {
    var table = $("tableList");
    
    for (var i = 1; i < table.rows.length; i++) {
        var row = table.rows[i];
        
        row.onclick = (function (i) {
            return function () {
                var table = $("tableList");
                
                for (var j = 1; j < table.rows.length; j++) {
                    var row = table.rows[j];
                    
                    if (j == i) {
                        row.className = "selectRow";
                    }
                    else {
                        row.className = "unselectRow";
                    }
                }
            }           
        })(i);
    }
}
```

**EDIT:**  The code above works by making the function (outer function) that wraps the event handler (inner function) as an IIFE (Immediately Invoked Function Expressions).  This creates a scope object for the outer function (remember Javascript scoping stops at the function level while C# continues at the block level) containing the current value of _i_ in the loop which is retained even after the outer function has returned.  Then each row's onclick event will end up having an inner function with access to a separate outer function's scope object, each containing a different value of _i_.

It’s not only the JavaScript language that has closure.  Other languages have it as well, like C#.  I encountered closure in C# the same way I did in JavaScript.  I was declaring/passing in a lambda expression to a function call inside a foreach loop, that references the foreach variable.  And since C# has a slightly different handling of closure than JavaScript, the solution is different.  In C#, one just need to assign the foreach or loop variable to a temporary variable and reference the temporary variable instead.

```js
public void SomeFunction()
{
    // ...
    foreach (Filter filter in filters)
    {
        // have to assign filter value to temp variable in the loop
        //  because the lambda expression we're using here is in a closure
        string filterVal = filter.Value;
        switch (filter.Field)
        {
            case "Location Name":
                locs = locs.Where(l => l.LocationName.Contains(filterVal));
                break;
            // ...
        }
    }
    // ...
}
```

It’s not easy to wrap your mind around closure, at least for me.  [Closures in C# vs JavaScript - Same But Different](http://www.smartik.net/2013/07/Closures-CSharp-vs-JS-Same-But-Different.html) really explains it to me clearly, from a really really technical point of view, as in how the compiler handles closure both in C# and JavaScript.  Don’t worry it’s not a long read but one needs to really read through the code. I’ve got other links for further reading if need be:

- [Outer Variable Trap in C#](http://stackoverflow.com/questions/3416758/outer-variable-trap)
- [Closing over the loop variable considered harmful in C#](http://blogs.msdn.com/b/ericlippert/archive/2009/11/12/closing-over-the-loop-variable-considered-harmful.aspx)
- [How do JavaScript closures work?](http://stackoverflow.com/questions/111102/how-do-javascript-closures-work)
- [JavaScript Closures ??](http://blogs.msdn.com/b/kartikb/archive/2009/02/08/closures.aspx)

I can’t guarantee you to become a closure relationship expert, but after going through the readings and links above,  I can guarantee you to become a closure programming expert ;).
