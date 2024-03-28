### warehouse performance
Queuing can be solved by SCALE-OUT (provision new clusters), i.e., increasing 
MAX_CLUSTER_COUNT helps in additional cluster provisioning to handle the 
concurrent workloads.

Multi-cluster warehouses are best utilized for scaling resources to improve 
concurrency for users/queries. They are not as beneficial for improving the 
performance of slow-running queries or data loading. For these types of 
operations, resizing the warehouse provides more benefits

The warehouse performance can be evaluated by querying the Account Usage QUERY_HISTORY view.

If the cache does fill up, it is flushed out in a least-recently used fashion.

Snowflake uses columnar scanning of partitions so that an entire partition is 
not scanned if a query only filters by one column. The closer the ratio of 
scanned micro-partitions and columnar data is to the ratio of actual data 
selected, the more efficient is the pruning performed on the table

Snowflake has three types of cache:

- The metadata cache that lives in the cloud services layer. 

- The data cache/local disk cache that lives on the SSD drives in the virtual 
warehouses 

- The query result cache. If a result is small, it will be stored in the cloud 
services layer, but larger results are going to be stored in the storage
layer.

Results are retained for 24 hours in Query Result Cache. Snowflake resets the 
24-hour retention period for the result, up to a maximum of 31 days from the 
date and time that the query was first executed. After 31 days, the result is 
purged and the next time the query is submitted, a new result is generated and 
persisted.

### Warehouse Scaling
In Standard Scaling policy, the first cluster starts immediately when either a 
query is queued, or the system detects that there’s one more query than the 
currently-running clusters can execute. Each successive cluster waits to start 
20 seconds after the prior one has started. For example, if your warehouse is 
configured with ten max clusters, it can take 200+ seconds to start all 10 
clusters.

When we suspend a warehouse, Snowflake immediately shuts down all idle compute 
resources for the warehouse. However, it allows any compute resources executing 
statements to continue until the statements are complete. At this time, the 
resources are shut down, and the warehouse status changes to “Suspended”. 
Compute resources waiting to shut down are considered to be in “quiesce” mode.

Until data has not changed and the query is the same - Snowflake reuses the 
data from the cache. Please note,  Each time the persisted result for a query 
is reused, Snowflake resets the 24-hour retention period for the result up to a 
maximum of 31 days from the date and time that the query was first executed. 
After 31 days, the result is purged, and the next time the query is submitted, 
a new result is generated and persisted.

#### Query Performance
When Snowflake warehouse cannot fit an operation in memory, it starts spilling (
storing) data first to the local disk of a warehouse node and then to remote 
storage. In such a case, Snowflake first tries to temporarily store the data on 
the warehouse's local disk. As this means extra IO operations, any query that 
requires spilling will take longer than a similar query running on similar data 
that is capable to fit the operations in memory. Also, if the local disk is 
insufficient to fit the spilled data, Snowflake further tries to write to the 
remote cloud storage, which will be shown in the query profile as "Bytes 
spilled to remote storage". 

The spilling can't always be avoided, especially for large batches of data, but 
it can be decreased by: 

- Reducing the amount of data processed. For example, by trying to improve 
partition pruning or projecting only the columns that are needed in the output. 

- Decreasing the number of parallel queries running in the warehouse. 

- Trying to split the processing into several steps (for example, by replacing 
the CTEs with temporary tables). 

- Using a larger warehouse - effectively means more memory and more local disk 
space.

If a node has insufficient memory to complete its portion of a query, it will 
"spill" to local SSD storage. This can negatively impact performance but is 
sometimes acceptable. If a node has insufficient local SSD storage to complete 
its portion of a query, it will "spill" to remote cloud storage. This is almost 
always very bad for performance. The solution, in either case, is to simplify 
the SQL query or increase the warehouse size.

As a best practice, Group and Execute similar queries on the same virtual 
warehouse to maximize local disk cache reuse for performance and cost 
optimization. The results get stored in the SSD of Virtual Warehouse. So, if 
the Virtual Warehouse gets suspended, then results get lost.

Please note, not all predicate expressions can be used to prune. Snowflake does 
not prune micro-partitions based on a predicate with a subquery, even if the 
subquery results in a constant.

### Materializations
Materialized views are particularly useful when: - Query results contain a 
small number of rows and/or columns relative to the base table (the table on 
which the view is defined). - Query results contain results that require 
significant processing, including: Analysis of semi-structured data. Aggregates 
that take a long time to calculate. - The query is on an external table (i.e., 
data sets stored in files in an external stage), which might have a slower 
performance compared to querying native database tables. - The view’s base 
table does not change frequently.

Materialized views are designed to improve query performance for workloads 
composed of common, repeated query patterns. However, materializing 
intermediate results incur additional costs. As such, before creating any 
materialized views, you should consider whether the costs are offset by the 
savings from re-using these results frequently enough.


### Good to know
Snowflake does not begin executing SQL statements submitted to a warehouse 
until all of the compute resources for the warehouse are successfully 
provisioned, unless any of the resources fail to provision: If any of the 
compute resources for the warehouse fail to provision during start-up, 
Snowflake attempts to repair the failed resources. During the repair process, 
the warehouse starts processing SQL statements once 50% or more of the 
requested compute resources are successfully provisioned.
