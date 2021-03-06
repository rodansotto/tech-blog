---
title: "VB 2005: Code generation in Visual Studio 2005"
date: "2007-05-05"
categories: 
  - "vb-net"
---

Visual Studio 2005 generates some code for us when we create our projects.  Code generated by this tool can be found in a separate file with **.Designer.vb** extension.  The code we make are saved in a file with **.vb** extension only.  This is possible with the use of **partial class**.

Let's take an example, say **Form1.vb**.  Code generated by Visual Studio 2005 is in **Form1.Designer.vb**.  Inside this file you will see your **Form1** class being declared as a partial class and being inherited from **System.Windows.Forms.Form**.  One of it's method is **InitializeComponent()** which is where all initializations and custom settings of properties of the form and the controls that you put on the form are generated.  So if you've set the **Text** property of your **Form1** to something else, say **My Form** on the form's **Properties** window, you will see this property being set inside the **InitializeComponent()** method.  Also if you added a button control on the form, you will also see initialization code for this button as well:

    Me.Button1 = New System.Windows.Forms.Button
    Me.SuspendLayout()
    '
    'Button1
    '
    Me.Button1.Location = New System.Drawing.Point(116, 150)
    Me.Button1.Name = "Button1"
    Me.Button1.Size = New System.Drawing.Size(75, 23)
    Me.Button1.TabIndex = 0
    Me.Button1.Text = "Button1"
    Me.Button1.UseVisualStyleBackColor = True
    '
    'Form1
    '
    Me.AutoScaleDimensions = New System.Drawing.SizeF(6.0!, 13.0!)
    Me.AutoScaleMode = System.Windows.Forms.AutoScaleMode.Font
    Me.ClientSize = New System.Drawing.Size(292, 273)
    Me.Controls.Add(Me.Button1)
    Me.Name = "Form1"
    Me.Text = "My Form"
    Me.ResumeLayout(False)

Note that **Button1** is declared outside the InitializeComponent() method but inside the Form1 class as:

    Friend WithEvents Button1 As System.Windows.Forms.Button 

It's cool that we can view the generated code and this will actually help us understand more what's involved in let's say, creating a form and adding a button control on the form.
