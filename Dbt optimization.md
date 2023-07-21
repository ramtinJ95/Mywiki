# Dbt optimazation


## Incremntal materialzation

#### Normal table materialization on a new run that results in 5
steps:
- Process start with CREAT TABLE AS then uses te dbt code as a reference. it
  will create a table in the same scheam and with the same name, but including
  the suffix "_dbt_tmp"
- Old table is renamed, addin the suffix "_dbt_backup"
- temp table get the offical name
- if the schema.yml is filled out the process identifges and comments all the
  comlums in the offical table
- finally the proccess drop the backpup table

#### Incremental without unique key
First execution the table is created from scratch. Second execution onwards, it
is possbile to better control how the table will be updated, instead of having
to be recreated daily. Since in this case we dont have and unique key dbt does
not really care and simply appends the new data to the previous data. In
Redshift this is accomplished in 3 steps:
- Creates a temp table
- Use temp table to insert data into the offical table
- If schema.yml has been filled out it identifies and comments on all cols in
  the offical table.
  
#### Incremental with unique key
When we include an unique key we can tell dbt which cols cannot have repeated
values. With this addition dbt execustes and addtional step: deletion of the
uniquies keys to be inserted into the final table thorugh the delete command.
This way, it is possible to ensure that the inserted data ins not reptead and
that the other colums which are not keys are uipdates with the latest veriosn of
the data. 

One important note is that when using more than one unique key, dbt does not
execute the usla delete from - select command, but rather a cast process which
significantly impact processing time, especially on large tables. So be careful
when choosing many unique kets to include in the incremental model in order to
avoid negative impacts on performance. 

# Redshift
## Rules to get good join performance
The merge join is the Holy Grail.
This is the and the only method which allows the timely joining of two Big Data
tables.
It comes with a wide range of constraints and restrictions, all of which must
be met for the merge join to be viable. AWS have never actually enumerated
the conditions and restrictions, but you can either figure them out from first
principles or you notice them over time; the join must be an equijoin (all join
clauses must use the “equals” operator), the columns in the join must be a
contiguous subset of the sorting order for both tables which begins with the
first column in the sorting order - so the first column in the sort order must
be joined, then you could also join the second, and the third, and so on, but
you could not join on the third only, or the second and the third - and both
tables must be up-to-date with VACUUM, and both tables must have the same
distribution key.
So here again you can see - the tables must be designed correctly so they can
merge join, which is hard enough, but then also the user must get the query
right. The query must follow the sorting orders of the tables.
If you can manage all this, life is amazing. A merge join passes once down each
table, uses no memory or processor time to speak of.
