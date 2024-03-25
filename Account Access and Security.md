### Networks
By default, Snowflake allows users to connect to the service from any computer or 
device IP address. A security administrator (or higher) can create a network 
policy to allow or deny access to a single IP address or a list of addresses


Network policies currently support only Internet Protocol version 4 (i.e. IPv4) addresses.


### Access
MODIFY - Enables altering any properties of a warehouse, including changing its 
size. Required to assign a warehouse to a resource monitor. Note that only the 
ACCOUNTADMIN role can assign warehouses to resource monitors. 

MONITOR - Enables viewing current and past queries executed on a warehouse as 
well as usage statistics on that warehouse. 

OPERATE - Enables changing the state of a warehouse (stop, start, suspend, 
resume). In addition, enables viewing current and past queries executed on a 
warehouse and aborting any executing queries. 

USAGE - Enables using a virtual warehouse and, as a result, executing queries 
on the warehouse. If the warehouse is configured to auto-resume when a SQL 
statement (e.g. query) is submitted to it, the warehouse resumes automatically 
and executes the statement. 

OWNERSHIP - Grants full control over a warehouse. Only a single role can hold 
this privilege on a specific object at a time. 

ALL [ PRIVILEGES ] - Grants all privileges, except OWNERSHIP, on the warehouse.

### User/Roles
A user's default role is the role a user gets set to each time the user logs in 
to Snowflake. Snowflake uses roles to control the objects (virtual warehouses, 
databases, tables, etc.) that users can access: 

Snowflake provides a set of predefined roles, as well as a framework for 
defining a hierarchy of custom roles.      All Snowflake users are 
automatically assigned the predefined PUBLIC role, which enables login to 
Snowflake and basic object access. 

In addition to the PUBLIC role, each user can be assigned additional roles, 
with one of these roles designated as their default role. A user’s default role 
determines the role used in the Snowflake sessions initiated by the user; 
however, this is only a default. Users can change roles within a session at any 
time. 

Roles can be assigned at user creation or afterward.


#### Data Security
ExplanationDynamic Data Masking is a Column-level Security feature that uses 
masking policies to selectively mask plain-text data in table and view columns 
at query time. 

External Tokenization enables accounts to tokenize data before loading it into 
Snowflake and detokenize the data at query runtime. Tokenization is the process 
of removing sensitive data by replacing it with an undecipherable token. 
External Tokenization makes use of masking policies with external functions.

### Platform security
Snowflake is a highly secured platform and provides multi-level security like 
Multi-Factor Authentication (MFA), provision to set up Network policy to block 
access by unwanted IPs, Single Sign On (SSO), Role-Based Access Control, and 
Tri Secret Secure, and so on. Tri-Secret Secure is the combination of a 
Snowflake-maintained key and a customer-managed key in the cloud provider 
platform that hosts your Snowflake account to create a composite master key to 
protect your Snowflake data.

