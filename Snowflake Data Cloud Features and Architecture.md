#aqaaq  q ## Roles
Users with the ACCOUNTADMIN role can view the billing for Automatic Clustering 
using Snowsight, the classic web interface, or SQL: 
- Snowsight: Select Admin » Usage. 
- Classic Web Interface: Click on Account tab » Billing & Usage The billing for
Automatic Clustering shows up as a separate Snowflake-provided warehouse named 
AUTOMATIC_CLUSTERING. 
- SQL:Query either of the following: AUTOMATIC_CLUSTERING_HISTORY table 
function (in the Snowflake Information Schema). AUTOMATIC_CLUSTERING_HISTORY
View (in Account Usage).

### Interface / Snowsight

There are three interfaces in Snowsight. Left Nav, User Menu, and Account 
Selector:

- Left Navigation consists of Worksheets, Dashboards, Data, ,
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

Snowsight is the new Snowflake Web Interface. It can be used to perform the following operations:

- Building and running queries.
- Loading data into tables.
- Monitoring query performance and copy history.
- Creating and managing users and other account-level objects.
- Creating and using virtual warehouses.
- Creating and modifying databases and all database objects.
- Sharing data with other Snowflake accounts.
- Exploring and using the Snowflake Marketplace.  
- One of the cool features is the smart autocomplete, which suggests SQL or object syntax to insert

### Snowflake Service Layers

- The search optimization service speeds up Equality and IN predicates
searches. Futhermore the following are the only datatypes that search
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

### Snowflake stage
An internal stage is a cloud repository that resides within a Snowflake account
and is managed by Snowflake. An external stage is a pointer to a cloud file 
repository outside a Snowflake account, which the customer manages independently. 
There are three types of stages, and they are table stage, user stage, and 
named stage. Table Stage: When you create a table, the system will create a 
table stage with the same name but with the prefix @%. User Stage: A user stage
is created whenever you create a new user in Snowflake. The user stage uses the
@~. Named Stage: Named stages are created manually. They can be internal or 
external and are prefixed with an @ and then the stage's name.

__User Stage:__ User stages cannot be altered or dropped. A user stage is 
allocated to each user for storing files. This stage type is designed to store 
staged and managed files by a single user but can be loaded into multiple tables.   

__Table Stage:__ Table stages cannot be altered or dropped. A table stage is 
available for each table created in Snowflake. This stage type is designed to 
store staged and managed files by one or more users but only loaded into a 
single table. Note that a table stage is not a separate database object but an 
implicit stage tied to the table itself. A table stage has no grantable 
privileges of its own.   

__Named Stage:__ A named internal stage is a database object created in a schema. 
This stage type can store files staged and managed by one or more users and 
loaded into one or more tables. Because named stages are database objects, the 
ability to create, modify, use, or drop them can be controlled using security 
access control privileges.

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

### Views

Snowflake supports three types of views.
Standard View, Secure View, and Materialized View.

- Standard View: It is a default view type. Its underlying DDL is available
to any role with access to the view. When you create a standard view, 
Snowflake saves a definition of the view. Snowflake does not run the query. 
When someone accesses the view, that is when the query is run. The standard 
view will always execute as the owning role. 

 - Secure View: The secure view is exactly like a standard view, except users 
cannot see how that view was defined. Sometimes a secure view will run a little 
slower than a standard view to protect the information in a secure view.
Snowflake may bypass some of the optimizations.

- Materialized View: A materialized view is more like a table. Unlike a 
standard or secure view, Snowflake runs the query right away when you create a 
materialized view. It takes the results set and stores that result set as a 
table in Snowflake. Because Snowflake is storing that materialized view as a 
table, creating micro partitions. Snowflake is creating metadata about those 
micro partitions. So when you query a materialized view, if you put a filter on 
the view, you get the same benefit of micro partition pruning that you would 
get from a table. With Snowflake, the materialized view is automatically 
refreshed every time there is a transaction against the base table. So it is 
always going to be in sync. If you want, you can also create a secure 
materialized view, which again will hide the logic from the user. A note about
materialized views, because Snowflake is auto-refreshing them in the background
,they use some credits, so there is a little bit of a cost there. Moreover, 
there is some storage, and Snowflake stores the result set as a table in 
Snowflake. So materialized views use more storage and compute than standard or 
secure views.

### Table
Insert-only stream type for streams on the external table.
Adding a stream to a table appends three metadata column: METADATA$ACTION, METADATA$ISUPDATE, 
METADATA$ROW_ID.  These columns track the CDC records and their type:  appends,  deletes, 
or both (updates = inserts + deletes).
METADATA$ACTION - Indicates the DML operation (INSERT, DELETE) recorded.

METADATA$ISUPDATE - Indicates whether the operation was part of an UPDATE statement.

METADATA$ROW_ID - Specifies the unique and immutable ID for the row, which can 
be used to track changes to specific rows over time.

__Snowflake supports four different table types: Permanent Table, Temporary Table,
Transient Table, and External Table:__ 

__Permanent Table:__ It persists until dropped. It is designed for data requiring 
the highest data protection and recovery level and is the default table type. 
Permanent Tables can be protected by up to 90 days of time travel with 
Enterprise Edition or above. Moreover, the failsafe is covered on all the 
Permanent Tables.

__Temporary Table:__ A Temporary table is tied to a specific session, which means 
it is tied to a single user. Temporary tables are used for things like materializing 
subquery. You can only cover temporary tables by up to one day of time travel, 
and they are not covered by a failsafe.     

__Transient Table:__ A Transient table is essentially a temporary table that more 
than one user can share because multiple users share a transient table. You 
have to drop it when you are finished with it, and it also is only covered by 
up to one day of time travel and is not covered by a failsafe. NOTE - WE CAN 
ALSO HAVE TRANSIENT DATABASES AND SCHEMAS.     

__External Table:__ An External Table is used to access data in a data lake. It is 
always read-only because it is based on files that live outside of Snowflake 
and are not managed by Snowflake, and Time Travel and Failsafe do not cover it.

### Snowflake connectors
There are three available connectors for snowflake; Python, Spark and Kafka.

__kafka connector__:
* Kafka topics can be mapped to existing Snowflake tables in the Kafka 
configuration. If the topics are not mapped, then the Kafka connector creates a
new table for each topic using the topic name. The Kafka connector subscribes 
to one or more Kafka topics based on the configuration information provided via
the Kafka configuration file or command line (Or the Confluent Control Center;
Confluent only).

### Good to know
standard retention period is 1 day and auto enabled for all snowflake accounts.
Snowflake keeps the batch load history for 64 days.
For snowflake Enterprise Edition
- For transient databases, schemas, and tables, the retention period can be set
to 0 (or unset back to the default of 1 day). The same is also true for temporary tables.
- For permanent databases, schemas, and tables, the retention period can be set to
any value from 0 up to 90 days.
- Snowflake keeps the Snowpipe's load history for 14 days. [Note / Important for exam]: 
If you recreate the PIPE then the load history will reset to empty.

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

__File staging commands__: Put(to a stage), Get(from a stage), List and Remove.
