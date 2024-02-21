### Time travel

### Fail-safe

### Retention times and polices

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
