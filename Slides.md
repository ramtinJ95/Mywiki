Allt är select statements

```sql
{{ config(materialized=table) }}

SELECT *
FROM public.orders
WHERE is_deleted = false

-- Kompileras till följande ------

CREATE TABLE analytics.orders AS(
  SELECT *
  FROM public.orders
  WHERE is_deleted = false
);

```

Refs
```sql
-- orders.sql
SELECT 
    *,
    CASE WHEN user_id = 12 THEN 1 ELSE 0
    END AS is_manual
FROM {{ ref('base_orders') }}
WHERE app_id = 'production'

-- Kompileras till följande ------
    
SELECT 
    *,
    CASE WHEN user_id = 12 THEN 1 ELSE 0
    END AS is_manual
FROM analytics.dev.base_orders 
WHERE app_id = 'production'

```

Tests
```yaml
models:
  - name: question_respondents_date
    columns:
      - name: count
        description: Total number of votes
        meta:
          contains_pii: false
          contains_user_generated_data: false
      - name: question_id
        meta:
          contains_pii: false
          contains_user_generated_data: false
      - name: question_group
        description: The type of question group [competition, content, question]
        meta:
          contains_pii: falyaml          contains_user_generated_data: false
      - name: question_group_subtype
        description: The subtype of question group [competition, content, open_text, defined]
        meta:
          contains_pii: false
          contains_user_generated_data: false
      - name: session
        meta:
          contains_pii: false
          contains_user_generated_data: false
      - name: vote_created_at
        description: The date and time (UTC) the vote was created
        meta:
          contains_pii: false
          contains_user_generated_data: false
        tests:
          - not_null

```

Macros
```sql
```
