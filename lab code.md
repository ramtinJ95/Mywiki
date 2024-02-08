-------- Load Data ------------
```sql
create warehouse transforming;
create database raw;
create database analytics;
create schema raw.jaffle_shop;
create schema raw.stripe;

```

```sql
create table raw.jaffle_shop.customers 
( id integer,
  first_name varchar,
  last_name varchar
);

copy into raw.jaffle_shop.customers (id, first_name, last_name)
from 's3://dbt-tutorial-public/jaffle_shop_customers.csv'
file_format = (
    type = 'CSV'
    field_delimiter = ','
    skip_header = 1
); 

```

```sql
create table raw.jaffle_shop.orders
( id integer,
  user_id integer,
  order_date date,
  status varchar,
  _etl_loaded_at timestamp default current_timestamp
);

copy into raw.jaffle_shop.orders (id, user_id, order_date, status)
from 's3://dbt-tutorial-public/jaffle_shop_orders.csv'
file_format = (
    type = 'CSV'
    field_delimiter = ','
    skip_header = 1
);

```

```sql
create table raw.stripe.payment 
( id integer,
  orderid integer,
  paymentmethod varchar,
  status varchar,
  amount integer,
  created date,
  _batched_at timestamp default current_timestamp
);

copy into raw.stripe.payment (id, orderid, paymentmethod, status, amount, created)
from 's3://dbt-tutorial-public/stripe_payments.csv'
file_format = (
    type = 'CSV'
    field_delimiter = ','
    skip_header = 1
);

```
---- check to se if data is loaded properly ------ 
```sql
select * from raw.jaffle_shop.customers;
select * from raw.jaffle_shop.orders;
select * from raw.stripe.payment; 

```

-------- First Model ------------------------------

create a new file under in model/ called customers.sql

```sql

with customers as (

    select
        id as customer_id,
        first_name,
        last_name

    from raw.jaffle_shop.customers

),

orders as (

    select
        id as order_id,
        user_id as customer_id,
        order_date,
        status

    from raw.jaffle_shop.orders

),

customer_orders as (

    select
        customer_id,

        min(order_date) as first_order_date,
        max(order_date) as most_recent_order_date,
        count(order_id) as number_of_orders

    from orders

    group by 1

),

final as (

    select
        customers.customer_id,
        customers.first_name,
        customers.last_name,
        customer_orders.first_order_date,
        customer_orders.most_recent_order_date,
        coalesce(customer_orders.number_of_orders, 0) as number_of_orders

    from customers

    left join customer_orders using (customer_id)

)

select * from final

```
change name to jaffle_shop and set defaul materializes parameters

models:
  jaffle_shop:
    +materialized: table
  example:
    +materialized: view

We can override these default values by adding the following at the top of our
model files:

{{ config(materialized='view') }} 

---- Now to follow dbt ways of doing things ---------

create 1 new file in models/ called stg_customers and break it out from the
customers.sql file. 
Make a ref call to it
```sql
with customers as (

    select * from {{ ref('stg_customers') }}
)

```
create a new yaml file in models/ called sources.yml

version: 2

sources:
    - name: jaffle_shop
      description: This is a replica of the Postgres database used by our app
      database: raw
      schema: jaffle_shop
      tables:
          - name: customers
            description: One record per customer.

Some organizational tips. Its a good idea to organize your models into folders
that correspond to the schema they are going be related to. 

sources:
  - name: stripe
    description: This is a replica of the Postgres database used by our app
    tables:
        - name: payment
          description: One record per customer

----- pause for lab 1 ----------

------ Test exempel ------------

version: 2

models:
  - name: customers
    columns:
      - name: customer_id
        tests:
          - unique
          - not_null

  - name: stg_customers
    columns:
      - name: customer_id
        tests:
          - unique
          - not_null

  - name: stg_orders
    columns:
      - name: order_id
        tests:
          - unique
          - not_null
      - name: status
        tests:
          - accepted_values:
              values: ['placed', 'shipped', 'completed', 'return_pending', 'returned']
      - name: customer_id
        tests:
          - not_null
          - relationships:
              to: ref('stg_customers')
              field: customer_id
              
--- singular test case ----

```sql
select amount
from {{ ref('stg_payment') }}
where amount < 0
```
---- generic test case ----

```sql
string_not_empty.sql
{% test string_not_empty(model, column_name) %}
    select {{ column_name}}
    from {{ model }}
    where TRIM({{ column_name }}) = ''
{% endtest %}
```

```sql

```

```sql

```
