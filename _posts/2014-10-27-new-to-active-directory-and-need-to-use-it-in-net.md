---
title: "New to Active Directory and need to use it in .NET?"
date: "2014-10-27"
categories: 
  - "net"
---

Don’t worry, it’s easier than you think. 

_AD Explorer_

If you haven’t seen what _Active Directory (AD)_ looks like, you can use a free AD viewer application, like the [AD Explorer](http://technet.microsoft.com/en-us/sysinternals/bb963907.aspx).  I would recommend downloading it because it’s a useful tool in navigating the tree structure of an AD and viewing the object properties or attributes that you want to use in your .NET program.

_Logging In To AD_

When using an AD viewer application, you will need to login to the AD and provide your Windows user login and password.  Usually the AD would be the domain name your computer is logged into.

Two ways to determine the domain your computer is logged into.  One is from _Control Panel –> System_ and there will be a _Domain:_ entry if you are logged into one.  Another way is looking at the environment variable _USERDOMAIN_.  From the command prompt, type _set user_ and press _ENTER_.  Look at the _USERDOMAIN=_ entry.  If it does not contain your computer name, then it should be the AD name.  For a more detailed instruction, click [here](https://www.cites.illinois.edu/network/activedirectory.html).

_Distinguished Names_

Once you get into the AD, you will see the AD tree structure and each item in the tree structure is an object.  Each object can be uniquely identified by it’s _distinguished name (DN)_ or path and contains a sequence of _RDN_s connected by commas.  _RDN_s are _relative distinguished names_ and they are basically attributes with associated values.  You can find a list of typical RDNs [here](http://msdn.microsoft.com/en-us/library/aa366101(v=vs.85).aspx) with some examples of distinguished names and a table listing the reserved characters that need to be escaped when used in attribute values.

_AD Objects in .NET_

To get starting coding AD in .NET, you will need to reference _System.DirectoryServices_ in your program and add the following statement:

using System.DirectoryServices;

  

And the two objects that you need to use are: _DirectoryEntry_ and _DirectorySearcher_.

You use _DirectoryEntry_ in which to bind the object in the AD tree to.  You  need to supply the provider (usually it’s _LDAP:_// ) and the path which can include the AD name.  The example below is querying an AD user.

// sADName would be the AD you want to log into  
string sADName = "addomain.com";   
      
// sDN would be the distinguished name or path of an object in the AD tree  
string sDN = "CN=Users,DC=addomain,DC=com";   
      
// create an instance of DirectoryEntry supplying in the provider and path  
// in example below, provider is LDAP:// and path is the combination of   
//  AD name and distinguished name  
DirectoryEntry adEntry =   
    new DirectoryEntry(@"LDAP://" + sADName + "/" + sDN);  
      
// read the property or attribute of an AD object,   
//  such as the user's display name  
MessageBox.Show(adEntry.Properties\["displayName"\].Value.ToString();

  

For a list of all attributes defined by AD, click [here](http://msdn.microsoft.com/en-us/library/ms675090(v=vs.85).aspx).  The list there does not show the attribute names to use in the _Properties_ collection of the _DirectoryEntry_ object.  When you click an attribute in the list, it will show the detailed information about the attribute.  The attribute name to use should be under the _Ldap-Display-Name_.

You use _DirectorySearcher_ when you want to search AD, say for example users with Smith as their last names.

// you pass in an instance of the DirectoryEntry object containing the root   
//  or path in AD as a starting point to search from, to DirectorySearcher  
DirectoryEntry adEntry =   
    new DirectoryEntry(@"LDAP://addomain.com/DC=addomain,DC=com");  
DirectorySearcher adSearch = new DirectorySearcher(adEntry);  
      
// set the filter  
adSearch.Filter = "(&(objectCLass=user)(sn=Smith))";  
      
// then search  
SearchResultCollection adResultCol = adSearch.FindAll();  
listBoxResults.DataSource =  
    (from SearchResult r in adResultCol  
     select new  
     {  
         Value = r.GetDirectoryEntry().Properties\["distinguishedName"\]  
                    .Value.ToString(),  
         Text = r.GetDirectoryEntry().Properties\["displayName"\]  
                    .Value.ToString()  
     }  
    ).ToList();

  

For more details on the search filter syntax, click [here](http://msdn.microsoft.com/en-us/library/aa746475(v=vs.85).aspx).

_Other Resources_

- [Active Directory Technology Backgrounder](http://msdn.microsoft.com/en-us/library/ws96bs11(VS.71).aspx)
- [Creating DirectoryEntry Component Instances](http://msdn.microsoft.com/en-us/library/x8wxt72e(v=vs.71).aspx)
- [Howto: (Almost) Everything In Active Directory via C#](http://www.codeproject.com/Articles/18102/Howto-Almost-Everything-In-Active-Directory-via-C#27)
- [MS Outlook: How Do LDAP Attributes Map to Address Book Fields?](http://www.openldap.org/faq/data/cache/294.html)
