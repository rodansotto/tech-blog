---
title: "General: Recursive Programming"
date: "2013-10-12"
categories: 
  - "general"
---

So what is recursive programming?  As someone who took up Computer Science, this is something you learn in school but never really used it at work.  Unless you work in a specialized field, it is not something that one might use when programming business applications.

Remember Fibonacci?  Fibonacci numbers are defined as the sum of the two preceding numbers.

0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, ...

  

I still remember Fibonacci because I was given a test on it in my job interview 4 years ago.  In fact, I blogged about it [here](https://rodansotto.github.io/tech-blog/2009/04/14/general-fibonacci-sequence-using-a-loop-versus-a-recursive-function.html).  You can use a loop function to program Fibonacci, but a recursive function is the way to go, as in below:

public int fibonacci(int n)  
{  
   if (n <= 0) return 0;  
   else if (n == 1) return 1;  
   else return fibonacci(n - 1) + fibonacci(n - 2);  
}  

  

You can use recursive functions to implement linked lists and binary search as well.  Go to this [link](http://www.cs.cmu.edu/~adamchik/15-121/lectures/Recursions/recursions.html) to quickly refresh yourself on recursive programming.
