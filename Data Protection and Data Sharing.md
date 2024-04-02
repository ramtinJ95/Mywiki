### Time travel
Snowflake Time Travel enables accessing historical data (i.e. data that has 
been changed or deleted) at any point within a defined period. It serves as a 
powerful tool for performing the following tasks: 

Restoring data-related objects (tables, schemas, and databases) that might have been accidentally or intentionally deleted.

Duplicating and backing up data from key points in the past.

Analyzing data usage/manipulation over specified periods of time.

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

### Fail-safe
Fail-safe is not provided as a means for accessing historical data after the 
Time Travel retention period has ended. It is for use only by Snowflake to 
recover data that may have been lost or damaged due to extreme operational 
failures. Data recovery through Fail-safe may take from several hours to 
several days to complete.

Decreasing Retention reduces the amount of time data is retained in Time Travel:
For active data modified after the retention period is reduced, the new shorter period applies.
For data that is currently in Time Travel:     
If the data is still within the new shorter period, it remains in Time Travel.     
If the data is outside the new period, it moves into Fail-safe. 
For example, if you have a table with a 30-day retention period and you decrease the period to 
20-day, data from days 21 to 30 will be moved into Fail-safe, leaving only the data from day 
1 to 20 accessible through Time Travel. 

However, the process of moving the data from Time Travel into Fail-safe is performed by a background process, so the change is not immediately visible. Snowflake guarantees that the data will be moved, but does not specify when the process will complete; until the background process completes, the data is still accessible through Time Travel.

### Sharing of data
There are three types of accounts involved in data sharing.
- Data Providers: Share data with others
- data consumers: Accesses shared data with their own Snowflake account.
- Reader Accounts: Query data using compute from the data provider's account.
Reader Accounts are what you can use to share data with somebody who does not
already have a Snowflake account

__Shared dabase__: Shared databases are read-only. A consumer cannot UPDATE a 
share. However, the consumer can do a CREATE TABLE AS to make a point-in-time
copy of the data that's been shared. The consumer cannot clone and re-share a 
share or forward it. And also, time travel data on a share is not available to 
the consumer. A share can be imported into one database. This is super important
for the exam. 

Snowflake data providers can share data that resides in different databases by 
using secure views. A secure view can reference objects such as schemas, tables,
and other views from one or more databases, as long as these databases 
belong to the same account.

### Shares
Shares are named Snowflake objects that encapsulate all of the information 
required to share a database. Each share consists of:
The privileges that grant access to the database(s) and the schema containing the objects to share.
The privileges that grant access to the specific objects in the database.
The consumer accounts with which the database and its objects are shared. 

Example:
CREATE SHARE "SHARED_DATA" COMMENT='';
GRANT USAGE ON DATABASE "DEMO_DB" TO SHARE "SHARED_DATA";
GRANT USAGE ON SCHEMA "DEMO_DB"."TWITTER_DATA" TO SHARE "SHARED_DATA";
GRANT SELECT ON VIEW "DEMO_DB"."TWITTER_DATA"."FOLLOWERS" TO SHARE "SHARED_DATA";

##### Snowflake Secure Data sharing feature
Secure Data Sharing enables sharing selected objects in a database in your 
account with other Snowflake accounts. The following Snowflake database objects
can be shared: 

- Tables 
- External tables 
- Secure views 
- Secure materialized views 
- Secure UDFs 

Snowflake enables the sharing of databases through shares created by data 
providers and “imported” by data consumers.
