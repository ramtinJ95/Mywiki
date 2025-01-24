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
the player_rating column only depends on the player_id, so it is NOT in 2NF.

#### Third Normal Form
The definition of 3NF is this: Every non-key attribute in a table should depend
on the key, the whole key, and nothing but the key.

For example lets assume we have a table with the following columns: player_id,
player_rating and player_skill_level.

From 1-3 = beginner, 4-6 = intermediate and 7-9 = advanced

Now lets say player with id 1 goes from skill level 3 to 4 and we write this
update to the table in the player_skill_level column. Since this means in 
increase in rating aswell from beginner to intermediate we write this to 
the player_rating column but something goes wrong and we fail to update this
column. How did we end up in this data inconsistent situation while following
2NF?

Player_skill_level depends on player_id.
Player_rating depends on player_skill_level which depends on player_id.
So in other words player_rating has a transitive dependency on player_id, and it
is this type of dependency which is forbidden in 3NF. In other words we have
here a dependency of a non-key column on another non-key column which is not
allowed by the definition of 3NF.

Solution is to break out into a new table such that player_skill_level is the
key and player_rating is the non-key column. And our original table should be
only player_id as the key column and player_skill_level as the non-key column.

