---
title: "ASP.NET 2.0: Learning the Basics, Part II"
date: "2007-05-05"
categories: 
  - "asp-net"
---

**Validation Controls**

You also have the ability to put some validation onto your controls using some of the available validation controls.

**RequiredFieldValidator** will check if the control you assigned to it (**ControlToValidate**) has a value.  Other properties you can set are **Text**, and **ErrorMessage**.  **Text** is displayed when no value is entered for the control while **ErrorMessage** will show up on the **ValidationSummary** control if you have it setup on your webpage.

**CompareValidator** will compare the value of the control you assigned to it (**ControlToValidate**) to some value you specify (**ValueToCompare**) given the comparison operator you indicated (**Operator**).  You can also compare it to another control (**ControlToCompare**).  You also need to set the **Type** to indicate the type of the values that you want to compare (e.g. **String**, **Integer**, **Double**, **Date**, or **Currency**).  As with the **RequiredFieldValidator**, you can also set the **Text** and **ErrorMessage** properties.

**Layout Toolbar**

If you want to align your controls or lay them out in relation to the other controls, you can make use of the **Layout** toolbar.  Go to **View -> Toolbars** and select **Layout**.  You can align lefts, centers, rights, tops, middles, and bottoms, make same width, height, and size, increase/decrease/remove horizontal/vertical spacing, and bring to front/send to back.

**AutoPostBack**

If you need to postback to the server after selection to the control is changed without having the user to initiate the postback (using a **Button** control), you can set the **AutoPostBack** property to **True**.
