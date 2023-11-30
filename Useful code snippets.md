## Bash/Unix commands
If you want to rename all the files in a dir that does not contain any spaces
use this one liner

```bash

ls | xargs -I {} mv {} Unix_{}

```

## Vim motions/commands
- "syy yanks the current line into a register called s that one can paste from by doing "sp, in this way its possible to paste from 1 register and not hav it be overwritten when doing deletes. Note that the lowercase naming of the register, in this case s, can be any letter as long as it does not interfere with the normal vim motions, for example a does not work since it will move you into insert mode. 

## Git
If one wants to clean up their local git repo that has a bunch of branches which
are not used and just making it hard to find the branch one is looking for then
run the following

```bash
git branch | grev -v "main" | xargs git branch -D 
```


This little snippet is super cool. It show how one can generate many sql queries
by just using plain sql, super coolt
```sql

SELECT 'GRANT ALTER ON TABLE ' || table_schema || '.' || table_name || ' TO aeadmin;' AS grant_statement
FROM information_schema.tables
WHERE table_schema = 'snapshots';

```


This little snippet is a good example of how to find duplicate rows and then
look at them to being able to debug it faster. 
```sql

WITH find_duplicates AS (

	select
		id, 
		count(*) AS c
	FROM looker_models.dim_series_latest
	GROUP BY id
	HAVING c  >1

),

duplicates AS (

	SELECT dim_series_latest.* 
	FROM looker_models.dim_series_latest
	INNER JOIN find_duplicates
	ON dim_series_latest.id = find_duplicates.id 

)

SELECT * FROM duplicates
```
