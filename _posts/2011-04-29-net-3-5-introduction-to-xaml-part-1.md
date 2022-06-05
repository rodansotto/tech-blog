---
title: ".NET 3.5: Introduction to XAML - Part 1"
date: "2011-04-29"
categories: 
  - "net"
---

**What is XAML**

So what is **XAML** anyways?  It stands for e**X**tensible **A**pplication **M**arkup **L**anguage and is based on **[XML](http://www.w3schools.com/xml/default.asp)**.  It was initially created to be used in **WPF** (Windows Presentation Foundation) but is now being used also in **WF** (Windows Workflow Foundation), [Silverlight](http://www.silverlight.net/), and **[XPS](http://msdn.microsoft.com/en-us/windows/hardware/gg463373.aspx)** (XML Paper Specification). 

**Why XAML**

So why another markup language?  The reason behind creating this to be used in WPF is to allow the designers (those responsible for the graphical user interface) and developers (those who code the behavior)  to collaborate well, to have them work on their stuff separately, and once done merge their stuff without a hitch.  End result is a top notched graphical user interface and a perfectly working application.

**XAML Tools**

The major tools for creating XAML are: [Expression Design](http://www.microsoft.com/expression/products/Design_Overview.aspx), [Expression Blend](http://www.microsoft.com/expression/products/Blend_Overview.aspx), and Visual Studio (starting from version 2008).  As a developer, you can actually just use Visual Studio to create your visual elements in XAML and code-behind it.  But for more complex graphics, the two Expression products are more suitable.

**XAML in WPF**

Since XAML is a declarative language, it is used to describe objects in .NET, just like what HTML is used to describe what should be displayed on a Web page.  XAML describes objects form a subset of .NET namespaces, which include **System.Windows**, **System.Windows.Controls**, **System.Windows.Data**, and **System.Windows.Media**. 

Since XAML is XML based, it can be used to represent a tree of objects.  And as with all XML markups, XAML is case sensitive.

XAML in WPF uses WPF namespace (the same namespace concept used in XML) to avoid confusion with XAML used in WF, and so on.

XAML is compiled, at runtime, into **BAML** (Binary Application Markup Language), a more optimized form for parsing, and embedded as a resource in **EXE** or **DLL**.

A sample XAML listed below describes a button object.  It will display a **Button** control on a **StackPanel** layout on the UI with default visual presentation and default behaviors.

\[sourcecode language="xml" padlinenumbers="true" gutter="false" light="true" toolbar="false"\]
<StackPanel>
  <Button Content="Click Me"/>
</StackPanel>
\[/sourcecode\]

Other sample XAMLs:

\[sourcecode language="xml" gutter="false" light="true" toolbar="false"\]
<Button Background="Blue" Foreground="Red" Content="This is a button"/>
\[/sourcecode\]

\[sourcecode language="xml" gutter="false" light="true" toolbar="false"\]
<Button>
  <Button.Background>
    <SolidColorBrush Color="Blue"/>
  </Button.Background>
  <Button.Foreground>
    <SolidColorBrush Color="Red"/>
  </Button.Foreground>
  <Button.Content>
    This is a button
  </Button.Content>
</Button>

\[/sourcecode\]

If you are coming form an ASP.NET or Web background, these XAML samples do look familiar.  Stylesheets is what comes into my mind though.
