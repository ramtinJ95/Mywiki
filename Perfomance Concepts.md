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

### Materializations
Materialized views are particularly useful when: - Query results contain a 
small number of rows and/or columns relative to the base table (the table on 
which the view is defined). - Query results contain results that require 
significant processing, including: Analysis of semi-structured data. Aggregates 
that take a long time to calculate. - The query is on an external table (i.e., 
data sets stored in files in an external stage), which might have a slower 
performance compared to querying native database tables. - The view’s base 
table does not change frequently.
