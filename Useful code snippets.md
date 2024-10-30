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

This little snippet is how I built the clustering of vote pins:


```sql
 RESPONDENTS_SQL = <<~SQL
          SELECT COUNT(DISTINCT identifier_id) as respondents
          FROM vote_pins
          WHERE question_id = ? AND session = ?
        SQL

        NO_AGGREGATION_SQL = <<~SQL
          SELECT st_x(pin) AS percentage_x, st_y(pin) AS percentage_y, session
          FROM vote_pins
          WHERE  question_id = ?
        SQL

        AGGREGATION_SQL = <<~SQL
          SELECT ST_NumGeometries(t.cluster) AS num_pins, st_x(ST_Centroid(t.cluster)) AS percentage_x, st_y(ST_Centroid(t.cluster)) AS percentage_y
          FROM (
            SELECT unnest(st_ClusterWithin(pin, ?)) AS cluster
            FROM vote_pins WHERE question_id = ?
            AND session = ?
          ) AS t
          GROUP BY t.cluster
        SQL

        CORRECT_AREA_AGGREGATION_SQL = <<~SQL
          SELECT ST_NumGeometries(t.cluster) AS num_pins,
                st_x(ST_Centroid(t.cluster)) AS percentage_x,
                st_y(ST_Centroid(t.cluster)) AS percentage_y,
                t.is_correct AS is_correct
          FROM
            (SELECT unnest(st_ClusterWithin(pin, :pin_distance)) AS CLUSTER,
                    ST_Contains(
                                  (SELECT geometry
                                  FROM correct_areas
                                  WHERE question_id = :question_id
                                  AND SESSION = :session ),
                                  pin) AS is_correct
            FROM vote_pins
            WHERE question_id = :question_id
              AND SESSION = :session
            GROUP BY is_correct) AS t
          GROUP BY t.cluster,
                  t.is_correct
        SQL
```

When you want to run docker container which you want to jump into but there are
some entrypoint issues and you get an error like " No ID provided" or something
along these lines then you can run this command:

```bash
docker run -it --rm --entrypoint /bin/sh <Image Name>
```
When wanting to list all columns in a table seperated with a new line in google
bigquery run the following query:

```sql
SELECT STRING_AGG(column_name, ',\n') AS column_list
FROM `your_project.your_dataset.INFORMATION_SCHEMA.COLUMNS`
WHERE table_name = 'your_table';
```


