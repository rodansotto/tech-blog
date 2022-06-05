---
title: ".NET Code Documentation And Testing:  They Are There, Why Not Use It?"
date: "2017-11-28"
categories: 
  - "net"
---

![]({{ site.baseurl }}/assets/images/xmldoccomments_01d.jpg)

Remember the "///"?  They are the C# XML documentation comments and they are pretty useful when you are building your APIs and frameworks so other developers who use your code can at least see some useful information on your classes and methods through the intellisense provided by the Visual Studio IDE.

Take the following sample code below.  I have a constructor and a method decorated with XML comments.

{% gist 2b0818cb3279e065d9fc6e18a89d2950 %}

And on the code where they are used, when I hover over them I will see my comments displayed.

![xmldoccomments_01]({{ site.baseurl }}/assets/images/xmldoccomments_01.jpg)

![xmldoccomments_02b]({{ site.baseurl }}/assets/images/xmldoccomments_02b.jpg)

So how about code testing?  .NET or more accurately Visual Studio comes with the Microsoft unit test framework.  It's so easy to add one to your new project or existing project.  Once you have the stubs created for you, you can start coding your tests.

Below is a sample unit testing code I created.

{% gist 9f607d9b76a910caefc4211c94340c7e %}

So every time you make changes to your code, and I say you will always need to change or refactor code, running these tests will make sure you didn't break anything.  So it is a pretty useful tool and I see the benefit in this.  And it's so nice to see so many green check marks on your Test Explorer.

![unittesting_01]({{ site.baseurl }}/assets/images/unittesting_01.jpg)

**For more information, check out these links:**

- [Recommended Tags for Documentation Comments (C# Programming Guide)](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments)
- [Unit Test Your Code](https://docs.microsoft.com/en-us/visualstudio/test/unit-test-your-code)
- [Testing for Continuous Delivery with Visual Studio 2012](https://msdn.microsoft.com/en-us/library/jj159345.aspx) - this might seem old but it contains best practices and fundamentals that still apply today
