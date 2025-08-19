
## Overview
Essentially the main driver behind the creating of WAP was a desire for
increased data quality and thus an increase of trust in the data. 

Lets says we have a user/query/dashboard/pipeline/transformation that fetches
data from some table. Now we want to update that table with some new data.

1) Write the data that yo are processing to somewhere that is not read by
consumers downstream. This could be a staging or temporary area, a branch, etc.
2) Audit the data to make sure that it meets the data quality specifications
3) Publish the data by writing it to the place form which consumers downstream
read it.

Publishing the data could be something like:
- Insert data from a staging table into the main table against which users run
their queries
- Flipping a flag ina table so that users querying it now include that data in
their results (perhaps using a view to effect this) or like a column with a
boolean etc.

Viewed like this, the WAP pattern is essentially the Blue-Green pattern that
operational database setups have been using for over a decade now. The key
difference is that we dont have a router, its the same queries that consumers
run but we are logically controlling what data gets included in their results


### Sources
- https://lakefs.io/blog/data-engineering-patterns-write-audit-publish/
- https://www.youtube.com/watch?v=fXHdeBnpXrg&ab_channel=DataWorksSummit
