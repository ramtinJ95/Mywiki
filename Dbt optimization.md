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

