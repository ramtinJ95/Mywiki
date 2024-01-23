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

```sql
```
Macros
```sql
```
