---
title: "WinForms: Using DevExpress, there is a quick way of making sure only one instance of a form is open"
date: "2014-03-03"
categories: 
  - "net"
---

If you are lucky enough to be using **DevExpress** and you don’t like the idea of using the **Singleton** pattern in enforcing this rule, then look no further.

You can use DevExpress’ **DocumentManager** control to manage your opened forms.  My solution is to create a static **FormManager** class encapsulating the document manager control and providing the one important method **ShowChildForm** which the **WinForms** application can call, passing in the type of the form it wishes to open.  Very simple.

Below is the code for the **FormManager** class:

namespace WindowsFormsApplication1
{
    public static class FormManager
    {
        private static DocumentManager documentManager;
        //   
        public static void InitializeFormManager(Form parentForm)
        {
            documentManager = new DocumentManager();
            documentManager.MdiParent = parentForm;
            documentManager.View = new NativeMdiView();
        }
        //
        public static void ShowChildForm(Type type)
        {
            if (documentManager == null)
            {
                return;
            }
            //    
            // check if child form is already open
            // if it's already open, then just activate it
            foreach (BaseDocument doc in documentManager.View.Documents)
            {
                if (doc.Control.GetType() == type)
                {
                    documentManager.View.ActivateDocument(doc.Control);
                    return;
                }
            }
            //
            // otherwise, create a new instance of the child form and display
            Form childForm = (Form)Activator.CreateInstance(type);
            childForm.MdiParent = documentManager.MdiParent;
            childForm.Show();
        }
    }
}

 

And somewhere in your WinForms application UI code, you call this function:

FormManager.ShowChildForm(typeof(MyForm));
