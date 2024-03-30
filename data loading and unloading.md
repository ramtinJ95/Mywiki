### Commands


### Insert Performance
Pattern matching using a regular expression is generally the slowest of the
three options for identifying/specifying data files to load from a stage;
however, this option works well if you exported your files in named order from
your external application and want to batch load the files in the same order

If the data exceeds 16 MB, enable the STRIP_OUTER_ARRAY file format option for
the COPY INTO <table> command to remove the outer array structure and load the
records into separate table rows: copy into <table> from @~/<file>.json
file_format = (type = 'JSON' strip_outer_array = true);

The number of load operations that run in parallel cannot exceed the number of
data files to be loaded. To optimize the number of parallel operations for a
load, we recommend aiming to produce data files roughly 100-250 MB (or larger)
in size compressed.

XS sized warehouse can load eight files parallelly. S sized warehouse can load
sixteen files parallelly. M sized warehouse can load thirty-two files
parallelly. L sized warehouse can load sixty-four files parallelly. XL sized
warehouse can load one hundred twenty-eight files parallelly and so on.

In a VARIANT column, NULL values are stored as a string containing the word
“null,” not the SQL NULL value. If the “null” values in your JSON documents
indicate missing values and have no other special meaning, you should recommend
setting the file format option STRIP_NULL_VALUES to TRUE for the COPY INTO <
table> command when loading the JSON files. Retaining the “null” values often
wastes storage and slows query processing

Of the three options for identifying/specifying data files to load from a
stage, providing a discrete list of files is generally the fastest; however,
the FILES parameter supports a maximum of 1,000 files, meaning a COPY command
executed with the FILES parameter can only load up to 1,000 files. Example:
copy into load1 from @%load1/data1/ files=('test1.csv', 'test2.csv',
'test3.csv', 'test4.csv')

A file in a stage has the LAST_MODIFIED date older than 64 days and the initial
set of data was loaded into the table more than 64 days earlier. In this case,
to prevent any data loss, the COPY command cannot definitively determine
whether a file has been loaded already if the LAST_MODIFIED date is older than
64 days and the initial set of data was loaded into the table more than 64 days
earlier (and if the file was loaded into the table, that also occurred more
than 64 days earlier). In this case, to prevent accidental reload, the command
skips the file by default.

### Insert Misc
The status of COPY INTO command can be checked from the Resource Monitors tab
in the Snowflake user interface, as well as querying the
INFORMATION_SCHEMA.LOAD_HISTORY and ACCOUNT_USAGE.LOAD_HISTORY view.

To load files whose metadata has expired, set the LOAD_UNCERTAIN_FILES copy
option to true. The copy option references load metadata, if available, to
avoid data duplication, but also attempts to load files with expired load
metadata. Alternatively, set the FORCE option to load all files, ignoring load
metadata if it exists. Note that this option reloads files, potentially
duplicating data in a table.

OVERWRITE specifies that the target table should be truncated before inserting
the values into the table. Note that specifying this option does not affect the
access control privileges on the table.

Using the PUT command in SnowSQL. It grabs the file or files, compresses them,
encrypts them, and then copies them up into the stage you chose. Once in the
stage, you can use a COPY INTO command to load the data from the stage into
Snowflake tables.

VALIDATION_MODE instructs the COPY command to validate the data files instead
of loading them into the specified table; i.e., the COPY command tests the
files for errors but does not load them. The command validates the data to be
loaded and returns results based on the validation option specified: Syntax :
VALIDATION_MODE = RETURN_n_ROWS | RETURN_ERRORS | RETURN_ALL_ERRORS
RETURN_n_ROWS (e.g. RETURN_10_ROWS) - Validates the specified number of rows,
if no errors are encountered; otherwise, fails at the first error encountered
in the rows. RETURN_ERRORS - Returns all errors (parsing, conversion, etc.)
across all files specified in the COPY statement. RETURN_ALL_ERRORS - Returns
all errors across all files specified in the COPY statement, including files
with errors that were partially loaded during an earlier load because the
ON_ERROR copy option was set to CONTINUE during the load.

The syntax for the VALIDATION_MODE parameter is: VALIDATION_MODE = RETURN_<n>
_ROWS | RETURN_ERRORS | RETURN_ALL_ERRORS.

It is important to note that the option RETURN_ROWS can only be used with the
COPY INTO <location> command and not with COPY INTO <table>. This option is the
only one available for the VALIDATION_MODE in COPY INTO <location>.

Staged files can be deleted from a Snowflake stage (user stage, table stage, or
named stage) using the following methods: 1- Files that were loaded
successfully can be deleted from the stage during a load by specifying the
PURGE copy option in the COPY INTO <table> command. 2- After the load
completes, use the REMOVE command to remove the files in the stage. Please
note, DELETE or REMOVE are not COPY command options. REMOVE is a different DML
command which is used to remove files in the stage.


### Snowpipe
Automating Snowpipe using cloud messaging (notification) and Calling Snowpipe
REST endpoints are the mostly uses methods for triggering loading with Snowpipe.

Snowpipe uses compute resources provided by Snowflake (i.e. a serverless
compute model). These Snowflake-provided resources are automatically resized
and scaled up or down as required, and are charged and itemized using per-
second billing. Data ingestion is charged based upon the actual workloads. User
doesn't need to create any warehouse as it is taken care by Snowflake.

Snowpipe is designed to load small volume of data (i.e., micro-batches) and 
incrementally make them available for analysis.

AUTO_INGEST = TRUE enables automatic data loading. Snowpipe supports loading
from external stages (Amazon S3, Google Cloud Storage, or Microsoft Azure).
AUTO_INGEST = FALSE disables automatic data loading. You must make calls to the
Snowpipe REST API endpoints to load data files.

When you recreate a pipe, if you do CREATE OR REPLACE PIPE, that load history
is reset to empty, so Snowflake doesn't know which files we've already loaded.

### Unload Misc
By default, all unloaded data files in Snowflake are compressed using the gzip
compression method, unless compression is explicitly disabled or one of the
other supported compression methods, such as bzip2 or Brotli, is explicitly
specified. Gzip is a widely used compression method that provides a balance of
high compression and fast decompression speeds, making it a suitable default
option in Snowflake.

The preferred way to distinguish empty strings from NULLs while unloading in
CSV files is to us an empty string is typically represented by a quoted empty
string (e.g. '') toindicate that the string contains zero characters. The 
preferred way is to enclose strings in quotes by setting the 
FIELD_OPTIONALLY_ENCLOSED_BY option,to distinguish empty strings from NULLs in
output CSV files.

In Snowflake, all output files are encoded using the UTF-8 character set. No
other character sets are supported. The use of UTF-8 ensures compatibility with
a wide range of platforms and applications.

The OBJECT_CONSTRUCT function can be used in combination with the COPY command
to convert the rows in a relational table to a single VARIANT column and unload
the rows into a file.

To unload data to a single output file (at the potential cost of decreased
performance), specify the SINGLE = true copy option in your statement. You can
optionally specify a name for the file in the path.

### Unload Performance


