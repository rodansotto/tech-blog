---
title: "General: Problem importing Access into Oracle using SQL*Loader"
date: "2007-05-05"
categories: 
  - "general"
  - "ms-access"
---

My wife is into [Oracle](http://www.oracle.com/index.html) and recently she had this problem of importing data from Access to Oracle using [SQL*Loader](http://www.oracle.com/technology/products/database/utilities/htdocs/sql_loader_overview.html).  What she was doing was export the Access data to CSV text file first and then have SQL*Loader import this CSV text file.  I helped her debug the problem after she told me it might be Access having problem in exporting the data correctly.  I checked the data in Access and found that it has embedded line feed and carriage return characters in the text and memo fields of the Access table she is importing. 

Now, knowing the cause of the problem, my wife tried to make SQL*Loader to replace these line feed (**CHR(10)**) and carriage return (**CHR(13)**) characters into space characters.  But still SQL*Loader interprets these as record terminator characters first before it can be replaced with space characters. 

I suggested to her to solve this problem from Access.  I went to the Access database and wrote an Access query that will replace these line feed and carriage return characters in the text and memo fields with space characters using Access built-in **[Replace()](http://office.microsoft.com/en-us/access/HA012288981033.aspx)** function:

    Replace(\[Text/Memo Field Column\], Chr(10) & Chr(13), ' ')

Instead of exporting the table, I exported the query to the CSV text file.  SQL*Loader imported this file and it worked.
