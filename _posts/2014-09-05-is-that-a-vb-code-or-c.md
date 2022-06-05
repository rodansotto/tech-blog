---
title: "Is that a VB code or C#?"
date: "2014-09-05"
categories: 
  - "c-sharp"
---

Ok, so the below code got me confused for a moment and I had to verify a couple of times if I am in the right language environment :).

int myNumber = 1;  
string myString = myNumber as string;

  

My initial question is, what’s the _as_ keyword doing in a C# code?  Is that a variable declaration like in VB?  As it turned out, it’s another operator in C# that performs like a cast operation but instead of raising an exception if the conversion is not possible, it returns _null_.  So there you go, next time you see _as_ keyword in C#, you are not hallucinating :).
