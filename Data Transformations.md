### transformation functions
VARIANT is a data type that can hold a value of any other data type (including 
ARRAY and OBJECT). VARIANT is used to build and store hierarchical data. 
VARIANT is not a function to FLATTEN. FLATTEN is a table function that is used 
to produce a lateral view of a VARIANT, OBJECT, or ARRAY column.

A scalar function is a function that returns one value per invocation; in most 
cases, you can think of this as returning one value per row. This contrasts 
with Aggregate Functions, which return one value per group of rows. Scalar 
functions take every row in your table, perform some calculation on that row 
and give you another value back.

UDF does not support sql DDL / DML. That means you can select from a table, 
but you can't create or modify tables inside of a UDF.

Aggregate functions operate on values across rows to perform mathematical 
calculations such as sum, average, counting, minimum/maximum values, standard 
deviation, and estimation, as well as some non-mathematical operations. An 
aggregate function takes multiple rows (actually, zero, one, or more rows) as 
input and produces a single output. In contrast, scalar functions take one row 
as input and produce one row (one value) as output. An aggregate function 
always returns exactly one row, even when the input contains zero rows. 
Typically, if the input contained zero rows, the output is NULL. However, an 
aggregate function could return 0, an empty string, or some other value when 
passed zero rows.

FLATTEN is a table function that produces a lateral view of a VARIANT, OBJECT, 
or ARRAY column. INFER_SCHEMA table function is used to detect the file 
metadata schema in a set of staged data files that contain semi-structured data 
and retrieves the column definitions. RESULT SCAN returns the result set of a 
previous command (within 24 hours of when you executed the query) as if the 
result was a table. SPLIT_TO_TABLE table function splits a string (based on a 
specified delimiter) and flattens the results into rows.

The expansion is performed for all sub-elements recursively by argument 
RECURSIVE => TRUE. Only the element referenced by PATH is expanded BY RECURSIVE 
=> FALSE. The OUTER argument is used to handle the input rows that cannot be 
expanded, either because they cannot be accessed in the path or because they 
have zero fields or entries.

A table function returns a set of rows for each input row. The returned set can
contain zero, one, or more rows. Each row can contain one or more columns.
Table functions are sometimes called “tabular functions”.

### UDFs
Java UDFs and tabular Java UDFs can read and process unstructured data in 
staged files using either the SnowflakeFile class or the InputStream class in the 
UDF code.

An UDF evaluates to a value, and can be used in contexts in which a general
expression can be used (e.g. SELECT my_function() ...). A stored procedure does
not evaluate to a value, and cannot be used in all contexts in which a general
expression can be used. For example, you cannot execute SELECT
my_stored_procedure()

UDF only runs as the function owner. A stored procedure runs with either the
caller’s rights or the owner’s rights. It cannot run with both at the same
time. A caller’s rights stored procedure runs with the privileges of the
caller. The primary advantage of a caller’s rights stored procedure is that it
can access information about that caller or about the caller’s current session.
For example, a caller’s rights stored procedure can read the caller’s session
variables and use them in a query. An owner’s rights stored procedure runs
mostly with the privileges of the stored procedure’s owner. The primary
advantage of an owner’s rights stored procedure is that the owner can delegate
specific administrative tasks, such as cleaning up old data, to another role
without granting that role more general privileges, such as privileges to
delete all data from a specific table. At the time that the stored procedure is
created, the creator specifies whether the procedure runs with owner’s rights
or caller’s rights. The default is owner’s rights.

### Sampling and Estimation
Snowflake uses HyperLogLog to estimate the approximate number of distinct 
values in a data set. HyperLogLog is a state-of-the-art cardinality estimation 
algorithm, capable of estimating distinct cardinalities of trillions of rows 
with an average relative error of a few percent.

SYSTEM | BLOCK sampling is often faster than BERNOULLI | ROW sampling. Also, 
BERNOULLI | ROW method is good for Smaller Tables and SYSTEM | BLOCK method for 
Larger Tables.

Snowflake recommends using HyperLogLog whenever the input is potentially
large, and an approximate result is acceptable.

SAMPLE / TABLESAMPLE returns a subset of rows sampled randomly from the 
specified table. The following sampling methods are supported: Sample a 
fraction of a table with a specified probability for including a given row. The 
number of rows returned depends on the size of the table and the requested 
probability. A seed can be specified to make the sampling deterministic. 

Sample a fixed, specified number of rows. The exact number of specified rows is 
returned unless the table contains fewer rows. SAMPLE and TABLESAMPLE are 
synonymous and can be used interchangeably.

BERNOULLI | ROW and SYSTEM | BLOCK are used to specify the sampling method in
SELECT query. BERNOULLI (or ROW): Includes each row with a <probability> of
p/100. Similar to flipping a weighted coin for each row. SYSTEM (or BLOCK):
Includes each block of rows with a <probability> of p/100. Similar to flipping
a weighted coin for each block of rows. This method does not support fixed-size
sampling. Sampling method is optional. If no method is specified, the default
is BERNOULLI. Example : select * from t1 tablesample bernoulli (25); This query
will return a sample of a table in which each row has a 25% probability of
being included in the sample

User-defined functions (UDFs) let you extend the system to perform operations
that are not available through the built-in, system-defined functions provided
by Snowflake. Snowflake currently supports the following languages for writing
UDFs: Java: A Java UDF lets you use the Java programming language to manipulate
data and return either scalar or tabular results. JavaScript: A JavaScript UDF
lets you use the JavaScript programming language to manipulate data and return
either scalar or tabular results. Python: A Python UDF lets you use the Python
programming language to manipulate data and return either scalar or tabular
results. SQL: A SQL UDF evaluates an arbitrary SQL expression and returns
either scalar or tabular results.




### Data URL
The expiration period of Scoped URL: The URL expires when the persisted query 
result period ends. The expiration period of the File URL: It is permanent. The 
expiration period of Pre-Signed URL: Length of time specified in the 
expiration_time argument.

The following types of URLs are available to access files in cloud storage: 
- Scoped URL: Encoded URL that permits temporary access to a staged file without 
granting privileges to the stage. The URL expires when the persisted query 
result period ends (i.e., the results cache expires), which is currently 24 
hours. Ideal for use in custom applications, providing unstructured data to other
accounts via a share, or for downloading and ad hoc analysis of unstructured
data via Snowsight
- File URL: URL that identifies the database, schema, stage, and file path 
to a set of files. A role that has sufficient privileges on the stage can 
access the files. Ideal for custom applications that require access to unstructured data files.
- Pre-signed URL: Simple HTTPS URL used to access a file via a 
web browser. A file is temporarily accessible to users via this URL using a pre-
signed access token. The expiration time for the access token is configurable.
Ideal for business intelligence applications or reporting tools that need to
display the unstructured file contents

The expiration period of Scoped URL: The URL expires when the persisted query 
result period ends. The expiration period of the File URL: It is permanent. The 
expiration period of Pre-Signed URL: Length of time specified in the 
expiration_time argument.

Only the user who generated the scoped URL can use the URL to access the
referenced file. In case of File URL, any role that has sufficient privileges on
the stage can access the file.

An HTTP client that sends a URL (either scoped URL or file URL) to the 
REST API must be configured to allow redirects.

BUILD_SCOPED_FILE_URL generates a scoped Snowflake-hosted URL to a staged file 
using the stage name and relative file path as inputs. A scoped URL is encoded 
and permits access to a specified file for a limited period of time. Scoped 
URL: Encoded URL that permits temporary access to a staged file without 
granting privileges to the stage. The URL expires when the persisted query 
result period ends (i.e., the results cache expires), which is currently 24 
hours.

A Directory table is not a separate database object; it stores a catalog of
staged files in cloud storage. Roles with sufficient privileges can query a
directory table to retrieve file URLs to access the staged files and other
metadata.

BUILD_STAGE_FILE_URL generates a Snowflake-hosted file URL to a staged file 
using the stage name and relative file path as inputs. A file URL permits 
prolonged access to a specified file. That is, the file URL does not expire. 
File URL: URL that identifies the database, schema, stage, and file path to a 
set of files. A role that has sufficient privileges on the stage can access the 
files.

GET_PRESIGNED_URL generates the pre-signed URL to a staged file using the stage 
name and relative file path as inputs. Pre-signed URL: Simple HTTPS URL used to 
access a file via a web browser. A file is temporarily accessible to users via 
this URL using a pre-signed access token. The expiration time for the access 
token is configurable.

GET_STAGE_LOCATION retrieves the URL for an external or internal named stage 
using the stage name as the input.


### Transform on load/unload
Snowflake supports transforming data while loading it into a table using the 
COPY command. Options include: 
- Column reordering 
- Column omission 
- Casts 
- Truncating text strings that exceed the target column length

VALIDATION_MODE instructs the COPY command to validate the data files instead of 
loading them into the specified table; i.e., the COPY command tests the files 
for errors but does not load them. The command validates the data to be loaded 
and returns results based on the validation option specified: Syntax : 
VALIDATION_MODE = RETURN_n_ROWS | RETURN_ERRORS | RETURN_ALL_ERRORS 
RETURN_n_ROWS (e.g. RETURN_10_ROWS) - Validates the specified number of rows, 
if no errors are encountered; otherwise, fails at the first error encountered 
in the rows. RETURN_ERRORS - Returns all errors (parsing, conversion, etc.) 
across all files specified in the COPY statement. RETURN_ALL_ERRORS - Returns 
all errors across all files specified in the COPY statement, including files 
with errors that were partially loaded during an earlier load because the 
ON_ERROR copy option was set to CONTINUE during the load.

ENFORCE_LENGTH: - If TRUE, the COPY statement produces an error if a loaded
string exceeds the target column length. - If FALSE, strings are automatically
truncated to the target column length. TRUNCATECOLUMNS: - If TRUE, strings are
automatically truncated to the target column length. - If FALSE, the COPY
statement produces an error if a loaded string exceeds the target column length.

The OUTER => FALSE argument with FLATTEN omits the output of the input rows
that cannot be expanded, either because they cannot be accessed in the path or
because they have zero fields or entries. The OUTER => TRUE argument with
FLATTEN generates exactly one row for zero-row expansions (with NULL in the
KEY, INDEX, and VALUE columns). RECURSIVE is used to instruct if only the
element referenced by PATH is expanded or expansion is performed for all sub-
elements recursively MODE Specifies whether only objects, arrays, or both
should be flattened.

### Rest API and http
CREATE SECURITY INTEGRATION command is used to create a security integration 
that supports OAuth to redirect users to an authorization page and generate 
access tokens for access to the REST API endpoint.

The Snowflake SQL API provides operations that we can use to
- Submit SQL statements for execution. 
- Check the status of the execution of a statement.
- Cancel the execution of a statement. 
- Fetch query results concurrently. Currently, Snowflake SQL API has limitation
for the call command with stored procedures that return a table (stored 
procedures with the RETURNS TABLE clause).

Snowflake SQL API supports Oauth, and Key Pair authentication.

### Directory table
The metadata for a directory table can be refreshed automatically using the 
event notification service for your cloud storage service. The refresh 
operation synchronizes the metadata with the latest set of associated files in 
the external stage and path, i.e.: - New files in the path are added to the 
table metadata. - Changes to files in the path are updated in the table 
metadata. - Files no longer in the path are removed from the table metadata.

Snowflake customers' charges include an overhead to manage event notifications
for automatically refreshing directory table metadata. This overhead increases
in relation to the number of files added in cloud storage for customers' stages
that include directory tables. Snowflake charges 0.06 credits per 1000 event
notifications received.

A Directory table is not a separate database object; it stores a catalog of
staged files in cloud storage. Roles with sufficient privileges can query a
directory table to retrieve file URLs to access the staged files and other
metadata. A directory table can be added explicitly to a stage when the stage
is created (using CREATE STAGE) or later (using ALTER STAGE) with supplying
directoryTableParams. directoryTableParams (for internal stages) ::= [
DIRECTORY = ( ENABLE = { TRUE | FALSE } [ REFRESH_ON_CREATE = { TRUE |
FALSE } ] ) ] ENABLE = TRUE | FALSE Specifies whether to add a directory table
to the stage. When the value is TRUE, a directory table is created with the
stage.


### Good to know
If files downloaded from an internal stage are corrupted, verify with the 
stage creator that ENCRYPTION = (TYPE = 'SNOWFLAKE_SSE') is set for the stage.

AUTO_REFRESH_REGISTRATION_HISTORY table function can be used to query the
history of data files registered in the metadata of specified objects and the
credits billed for these operations. The table function returns the billing
history within a specified date range for your entire Snowflake account. This
function returns billing activity within the last 14 days. Please note,
STAGE_DIRECTORY_FILE_REGISTRATION_HISTORY table function can be used to query
information about the metadata history for a directory table, including: -
Files added or removed automatically as part of a metadata refresh. - Any
errors found when refreshing the metadata.

Snowflake stores semi-structured data, such as JSON, Avro, Parquet, ORC, and XML, 
as VARIANT data type. A VARIANT can store a value of any other type, including 
OBJECT and ARRAY.

Unstructured data is information that does not fit into a predefined data model
or schema. Typically text-heavy, such as form responses and social media
conversations, unstructured data also encompasses images, video, and audio.
Industry-specific file types such as VCF (genomics), KDF (semiconductors), or
HDF5 (aeronautics) are included in this category.

System function that is used to execute an action in the system or return
information about the system. Snowflake provides the following types of system
functions: Control functions that allow you to execute actions in the system (
e.g. aborting a query). Information functions that return information about the
system (e.g. calculating the clustering depth of a table). Information
functions that return information about queries (e.g. information about EXPLAIN
plans).


