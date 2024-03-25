### warehouse performance
Queuing can be solved by SCALE-OUT (provision new clusters), i.e., increasing 
MAX_CLUSTER_COUNT helps in additional cluster provisioning to handle the 
concurrent workloads.

Multi-cluster warehouses are best utilized for scaling resources to improve 
concurrency for users/queries. They are not as beneficial for improving the 
performance of slow-running queries or data loading. For these types of 
operations, resizing the warehouse provides more benefits

### Materializations
Materialized views are particularly useful when: - Query results contain a 
small number of rows and/or columns relative to the base table (the table on 
which the view is defined). - Query results contain results that require 
significant processing, including: Analysis of semi-structured data. Aggregates 
that take a long time to calculate. - The query is on an external table (i.e., 
data sets stored in files in an external stage), which might have a slower 
performance compared to querying native database tables. - The view’s base 
table does not change frequently.
