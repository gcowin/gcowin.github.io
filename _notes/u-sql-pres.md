CDP/Azure Data Lake Presentation Nov 30

Why?
----
Learn about CDP and Data Lake.

What?
-----
Customer Data Platform (CDP) is a marketer-based management system. It creates a persistent, unified customer database that is accessible to other systems. Data is pulled from multiple sources, cleaned and combined to create a single customer profile. This structured data is then made available to other marketing systems.

CDP is currently a $300 million industry. $1 billion in 2019.

In addition, some CDPs provide additional functions such as marketing performance measurement analytics, predictive modeling, content marketing and Enterprise Campaign Management.

CDPs collect data that is tied to an identifiable individual. 

What is Data Lake?
------------------

What is u-sql?
---------------

When?
When you have big data and compute jobs. Not for simple queries.

How?
U-SQL, Pipelines, 

ML

Key Points
----------
T-SQL Differences
Join: only join using the equality operator (which, remember, is ==, not =) with u-sql
Equijoins
EXTRACT Schema on read

Pros
----
+ Can handle big data quickly and cheaply.
+ Integration with Azure services and ML
+ Familiar set of tools and tech

Cons
----
+ Deals with structured and unstructured data
+ 
+ You can't query and see result. You can generate results and download or preview data.
+ Nulls
+ Without initial checks, corrupt data may be ingested and used, before the problem is recognized
The problems of stale and corrupt data can turn a data lake into a “data swamp.”

Lessons Learned
---------------
Workaround for slow performance and freezes while editing u-sql:
+ at top of editor, select adla account: local-machine

If a table has theater_id, you'd better use it in queries.