## Description and explation of different normal from levels

#### First Normal Form
Needs to have primary key column.
Row order should not have any meaning.
Storing a repeating group of data items on a single row violates First Normal
Form. This means that we cannot have for example a table where we have some
player_id then an inventory column which contains a string of like 5 coins, 3
shields etc. Neither can we have 100 columns for each possible item and so on.
Instead we should have player_id, item_typ pe and item_quanitity. Where the
combination of player_id and item_typ is the PK.

#### Second Normal Form
The main benifit of this normal form is that we are protected against 3 types of
anomalies:
* Deletion anomaly
* Insertion anomaly
* update anomaly
The definition of the second normal form is this: Each non-key attribute (column)
must depend on the entire primary key.

For example lets assume we have a table which has the columns: player_id,
item_type, item_quantity and player_rating. The PK for this table is the
combination of player_id and item_type. 

So our non-key columns are item_quantity and player_rating. The column
item_quantity depends on the entire primary key so it is OK, i.e it is 2NF. But
the player_rating column only depends on the player_id, so it is NOT in 2NF
#### Third Normal Form
#### Fourth Normal Form
#### Fifth Normal Form
