### Networks
By default, Snowflake allows users to connect to the service from any computer or 
device IP address. A security administrator (or higher) can create a network 
policy to allow or deny access to a single IP address or a list of addresses

Network policies currently support only Internet Protocol version 4 (i.e. IPv4) addresses.

If you provide both Allowed IP Addresses and Blocked IP Addresses, Snowflake 
applies the Blocked List first. This would block your own access.Additionally, 
in order to block all IP addresses except a select list, you only need to add 
IP addresses to ALLOWED_IP_LIST. Snowflake automatically blocks all IP 
addresses not included in the allowed list.

Only a single network policy can be activated for each user at a time; however, 
different network policies can be activated for different users for granular 
control. Associating a network policy with a user automatically removes the 
currently-associated network policy (if any)

The "Policy Name" is the only required parameter because it serves as the 
unique identifier for the network policy within your Snowflake account. This 
name is essential for creating, managing, and referencing the network policy 
within Snowflake. 

Other parameters, such as "Allowed IP Addresses" (ALLOWED_IP_LIST), "Blocked IP 
Addresses" (BLOCKED_IP_LIST), and "Comment," are optional. These parameters 
allow for further customization of the network policy but are not mandatory for 
the policy's creation. The flexibility in specifying allowed and blocked IP 
addresses enables administrators to tailor network access controls according to 
their security requirements, but the policy can be created with just a name and 
detailed configurations can be added or adjusted later

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

Access History in Snowflake refers to when the user query reads column data and 
when the SQL statement performs a data write operation, such as INSERT, UPDATE, 
and DELETE, along with variations of the COPY command, from the source data 
object to the target data object. The user access history can be found by 
querying the Account Usage ACCESS_HISTORY view.

Snowflake’s approach to access control combines aspects from both of the 
following models: 

- Discretionary Access Control (DAC): Each object has an owner, who can in turn 
grant access to that object. 

- Role-based Access Control (RBAC): Access privileges are assigned to roles, 
which are in turn assigned to users.

To view the current set of privileges granted on an object, you can execute the 
SHOW GRANTS command. To view the current permissions on a schema, execute the 
following command: SHOW GRANTS ON SCHEMA  <database_name>.<schema_name>;

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

The SHOW PARAMETERS command determines whether a network policy is set on the account or for a specific user.
- For Account level: SHOW PARAMETERS LIKE 'network_policy' IN ACCOUNT;

- For User level: SHOW PARAMETERS LIKE 'network_policy' IN USER <username>; 

- Example - SHOW PARAMETERS LIKE 'network_policy' IN USER john;


#### Data Security
ExplanationDynamic Data Masking is a Column-level Security feature that uses 
masking policies to selectively mask plain-text data in table and view columns 
at query time. 

External Tokenization enables accounts to tokenize data before loading it into 
Snowflake and detokenize the data at query runtime. Tokenization is the process 
of removing sensitive data by replacing it with an undecipherable token. 
External Tokenization makes use of masking policies with external functions.

Active Key is used for both encryption and decryption.  The retired Key is used 
for decryption only.  The destroyed Key is no longer used.

Snowflake supports Role-Based Access control. Permissions on database objects 
such as databases or tables are granted to Roles.

A row access policy uses Conditional Expression Functions and Context Functions 
to determine which rows should be visible in a given context. Context Functions 
such as CURRENT_USER(), CURRENT_ROLE(), and CURRENT_ACCOUNT(), which act as 
dynamic filters and are commonly used with secure views to limit row access in 
a table.

### Platform security
Snowflake is a highly secured platform and provides multi-level security like 
Multi-Factor Authentication (MFA), provision to set up Network policy to block 
access by unwanted IPs, Single Sign On (SSO), Role-Based Access Control, and 
Tri Secret Secure, and so on. Tri-Secret Secure is the combination of a 
Snowflake-maintained key and a customer-managed key in the cloud provider 
platform that hosts your Snowflake account to create a composite master key to 
protect your Snowflake data.

### good to know
Snowflake Query history page allows you to view the details of all the queries 
executed in the last 14 days. You can query the Query_History view in 
Snowflake's Account Usage schema for older queries.

**Virtual Warehouse Privileges:**

USAGE: Enables using a virtual warehouse and, as a result, executing queries on 
the warehouse. If the warehouse is configured to auto-resume when a SQL 
statement (e.g. query) is submitted to it, the warehouse resumes automatically 
and executes the statement. 

MODIFY:  Enables altering any properties of a warehouse, including changing its 
size.   Required assigning a warehouse to a resource monitor. Note that only 
the ACCOUNTADMIN role can assign warehouses to resource monitors. 

MONITOR: Enables viewing of current and past queries executed on a warehouse as 
well as usage statistics on that warehouse. 

OPERATE: Enables changing the state of a warehouse (stop, start, suspend, 
resume). In addition, enables viewing current and past queries executed on a 
warehouse and aborting any executing queries. 

OWNERSHIP: Grants full control over a warehouse. Only a single role can hold 
	this privilege on a specific object at a time.
