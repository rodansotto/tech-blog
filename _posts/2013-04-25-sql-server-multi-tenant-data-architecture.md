---
title: "SQL Server: Multi-Tenant Data Architecture"
date: "2013-04-25"
categories: 
  - "sql-server"
---

As promised in my previous post, I will look briefly into ways on how to architect multi-tenant data.  Multi-tenant means servicing multiple clients or tenants.  In the case of a data architecture, it's how to store data from multiple clients.  I learned there are three options to do this, not just two.  I know the two of them are the most common which I will talk first.

First option, is using **Separate Databases**.  This is the simplest approach of all the three.  Basically each client has its own copy of the database, and sometimes depending on the client's strict security requirements, can be located on a server separate from the others.  It may be inexpensive in terms of development cost to do this way initially, but in the long run, it will be more expensive in terms of operational cost.

Second option, is using **Shared Database and Shared Schema**.  Only one database and one set of tables are used to store all the clients' data.  The only thing that differentiates them from each other is an ID unique to each client.  In contrast to using separate databases, using shared database and shared schema has a higher development cost but a lower operational cost.

These two options are popular, at least in my experience.  They are actually mostly used by application service provider companies.  In my last company, they use the separate databases option.  The company before that, I know they used the shared database and shared schema option.  Little did I know that there is a third option, which I still have yet to see implemented in an ASP company.

So the third option, is using **Shared Database and Separate Schemas**.  What this means is that there is only database but each client has its own copy of the set of tables that are grouped into a schema unique to each client.  So basically, when onboarding a new client, a schema unique to the client is created first and assigned and defaulted to the client account.  From within that client's schema, you then create the tables with the schema name as the qualifier for naming the tables to be created.  When accessing the client's data, since the client's default schema is set, you don't have to qualify the table names with the client's schema name.  Therefore, you use the same SQL statements for all clients.  There is no duplication of SQL statements here.

These three options have their own pros and cons which I won't be talking here.  This is just to give an idea what these options are.  If you need more information, check this [link](http://msdn.microsoft.com/en-us/library/aa479086.aspx).
