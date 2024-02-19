### Roles

### Interface / Snowsight

There are three interfaces in Snowsight. Left Nav, User Menu, and Account 
Selector:

- Left Navigation consists of Worksheets, Dashboards, Data, Marketplace,
Activity, Admin, Help & Support.
- User Menu lets you Switch Role, Profile including multi-factor authentication
(MFA) , Partner Connect, Documentation, Support and Sign Out.
- The account selector, located at the bottom of the left nav, lets you sign in
to other Snowflake accounts.

Using the ACCOUNTADMIN role you can use Snowsight or the classic web UI to veiw
data storage across your entire account:
- Using Snowsight: Select Admin > Usage > Storage
- Using Classic Web Interface: Click on Account > Billing & Usage > Average 
Storage Used

### Snowflake Service Layers

- The search optimization service sppeds up Equality and IN predicates
serarches. Futhermore the following are the only datatypes that search
optimization supports: Fixed-point numbers (e.g. INTEGER, NUMERIC). 
DATE, TIME, and TIMESTAMP. VARCHAR. BINARY.

- User-managed Tasks is recommended when you can fully utilize a single 
warehouse by scheduling multiple concurrent tasks to take advantage of 
available compute resources. Also recommended when adherence to the schedule
interval is less critical.

- Serverless Tasks is recommended when you cannot fully utilize a 
warehouse because too few tasks run concurrently or they run to 
completion quickly (in less than 1 minute). Also recommended when adherence to
the schedule interval is critical.

- Snowgrids capabilites are: Live, ready to query data. Secure, goverened data
  sharing. Share internally with private data exchange or externally with public
  data exchange.

##### Time travel

Snowflake Time Travel enables accessing historical data (i.e. data that has 
been changed or deleted) at any point within a defined period. It serves 
as a powerful tool for performing the following tasks: 

- Restoring data-related objects (tables, schemas, and databases) that might have been accidentally or intentionally deleted.
- Duplicating and backing up data from key points in the past.
- Analyzing data usage/manipulation over specified periods of time.

Using Time Travel, you can perform the following actions within a defined period:     

- Query data in the past that has since been updated or deleted.
- Create clones of entire tables, schemas, and databases at or before specific points in the past.     
- Restore tables, schemas, and databases that have been dropped.

### Clustering

In general for clutering of tables these are some good rules to keep in mind:

Clustering keys are not for every table. Tables in the multi-terabyte range 
are good candidates for clustering keys. Both automatic clustering and reclustering 
consume credit. A single clustering key can contain one or more columns or expressions.
Snowflake recommends a maximum of three or four columns (or expressions) per key for 
most tables. Adding more than 3-4 columns tends to increase costs more than benefits.

### Micro partitions
Micro-partitioning is automatically performed on all Snowflake tables. Tables are 
transparently partitioned using the Ordering of the data as inserted/loaded.
Snowflake stores metadata about all rows stored in a micro-partition, including:

- The range of values for each of the columns in the micro-partition.
- The number of distinct values. 
- Additional properties used for both optimization and efficient query processing.

Each micro-partition contains between 50 MB and 500 MB of uncompressed data
(Note that the actual size in Snowflake is smaller because data is always
stored compressed). Groups of rows in tables are mapped into individual
micro-partitions, organized in a columnar fashion. This size between 50 MB and
500 MB, and the structure allows for extremely granular pruning of very large
tables, which can be comprised of millions, or even hundreds of millions, of
micro-partitions. It enables extremely efficient DML and fine-grained pruning
for faster queries


TODO figure out clustering overlap depth meaning.

### Views

### Table
Insert-only stream type for streams on the external table.


### Good to know
standard retatation period is 1 day and auto enabled for all snowflake accounts.
Snowflake keeps the batch load history for 64 days.


__Stored Procedure__: A stored procedure runs with either the caller’s rights or 
the owner’s rights. It cannot run with both at the same time. A caller’s rights 
stored procedure runs with the privileges of the caller. The primary advantage 
of a caller’s rights stored procedure is that it can access information about 
that caller or about the caller’s current session. For example, a caller’s rights
stored procedure can read the caller’s session variables and use them in a query.

An owner’s rights stored procedure runs mostly with the privileges of the stored 
procedure’s owner. The primary advantage of an owner’s rights stored procedure is 
that the owner can delegate specific administrative tasks, such as cleaning up old 
data, to another role without granting that role more general privileges, such as 
privileges to delete all data from a specific table. 

At the time that the stored procedure is created, the creator specifies whether the
procedure runs with the owner’s rights or the caller’s rights. The default is 
owner’s rights.


__Zero-Copy cloning__:Zero-copy cloning allows us to make a snapshot of any table, 
schema, or database without actually copying data. A clone is writable and is 
independent of its source (i.e., changes made to the source or clone are not 
reflected in the other object). A new clone of a table points to the original 
table's micro partitions, using no data storage. If we make any changes in the 
cloned table, then only its changed micro partitions are written to storage.

TODO figure out meaning of staging in snowflake.
