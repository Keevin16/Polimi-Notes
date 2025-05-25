It has be done to query the data stored in Cassandra.
## KeySpace
It's the first operation to perform before the creation of the table.
Note that is the outermost container in Cassandra.
``` cql
CREATE KEYSPACE population
WITH replication = {
	'class': 'SimpleStrategy', 
	'replication_factor': 3
	};
``` 

## Partition & Clustering key
A table can employ many different **Clustering** and/or **Partition Key**.
The first value is called **[[Partition Key]](s)**.
The second value is named **[[Clustering Key]](s)**.
``` cql
PRIMARY KEY ((personal_id, ...), age, ...)
```

## Create a table
When it's created a table, clustering keys can be used to define an ordering
``` cql
CREATE TABEL person( 
	column_definition_1 column_type,
	column_definition_2 column_type
)
WITH CLUSTERING OERD BY (age ASC, ...);
``` 
All the different [[Column Type]]
## Describe & Use
The **Describe** command can be used to check whether a **KeySpace** (or a table) has **been correctly created**.
it's possible to check to the tables!
``` cql
	DESCRIBE keyspaces;
``` 

In order to be able to perform the operations on the tables, we must choose in which **KeySpace** we want to work.
``` cql
	USE keyspaces_name;
```

## Alter & Drop( or Truncate)
**Keyspaces** and **Table** can also be modified with **Alter** and deleted with **Drop** with the corresponding commands.
``` cql
	ALTER KEYSPACE identifier WITH properties 
	
	ALTER TABLE Table_name ADD //In orfer to add s new column to our table
	ALTER TABLE Table_name DROP Column_name //Remove it 
```
---
``` cql
	DROP KEYSPACE identifier;
	DROP TABLE table_name;
	---
	TRUNCATE TABLE table_name;
```

## Index
**Indexes** are one of the most important elements of a table in Cassandra. 
It's kind of hard to notice an advantage on a small set of data, while it's essential in big dataset.
They allow to query the column efficiently.
``` cql
// MUST BE ON A KEYSPACE
CREATE INDEX <identifier>
ON <table_name> (<column_name>);
---
CREATE INDEX person_address
ON person (name);
---
// Then TO DELETE IT
DROP INDEX <person_address>
```
## Batch
it's possible to organize a set of operations, like **INSERT**, **UPDATE** and **DELETE** in a **Batch**.
In this way they are execute one after another with a single command.
``` cql
BEGIN BATCH
	<insert_statement>;
	<update_statement>;
	<delete_statement>;
APPLY BATCH;
```
### Capture
the **Capture** command followed by the path of the folder in which store the results and the name of the file.
``` cql
CAPTURE <uri>;
// . . . . .  .
CAPTURE off;
```
### Expand
The expand command provides extended outputs within the console when performing queries. It must be executed before the query to enable it. 
``` cql
EXPAND on;
...
EXPAND off;
``` 
### SOURCE
In order to run queries from textual files. The command accept the URI.
``` cql
SOURCE <uri>
``` 


>There aren't foreign keys! It's the same for relationships.
>If you want to do cross-table check you must manage it by your self.



## Example
- Try to add two new columns to the person table named address(text) and salary(float).
``` cql
ALTER TABLE person
ADD address text;
---
ALTER TABLE person
ADD salary float;
```

### Insert
- Insert data within our table
``` cql
//For sure you must be in a KeySpace
INSERT INTO person ( peronsal_id, address, age, birth_date, gender, name)
VALUES ("123234345456", "Via Ampere", "26", "12-1-2000", "Male", "Tonino")
)
```
### Select / Delect
- Let's see how to select data within our tables
``` cql
//For sure you must be in a KeySpace
SELECT <field_list>
FROM <table_name>
WHERE <conditions>
---
SELECT *
FROM person
WHERE personal_id = "xxxxxxx"
```
**NOTE**: An **Invalid Request Error** is shown if you try to retrieve data which are not associated with primary or secondary index.
All the operation are optimized to extract data from columns.
case study of not working query:
``` cql
//For sure you must be in a KeySpace
SELECT *
FROM person
WHERE age = 26
//This will lead to an **Invalid Request Error**
```
Instead to make it works - **ALLOW FILTERING** at the end of the query.
otherwise **define the index**.
``` cql
CREATE INDEX car_price ON car(price);
SELECT * FROM car where price = 35000;
``` 
***
``` cql
DELETE 
FROM <table_name>
WHERE <condition>;
---
DELETE 
FROM person
WHERE address = "Via x 7";
```
### Update
``` cql
UPDATE <table_name>
SET <columun_name> = <new_value>, ...
WHERE <condition>;
``` 
As below
``` cql
UPDATE person
SET address 0 "Via Milani 13"
WHERE personal_id = "yyyyyyy"
```


#### CASE STUDY
-  Create a KeySpace named "car_dealer"
``` cql
CREATE KEYSPACE car_dealer 
WITH replication = {
'class'='SimpleStrategy',
'replication_factor'=3
}
```
- Check if they have been described
``` cql
DESCRIBE keyspaces;
DESCRIBE car_dealer;
``` 
- Create a table named “car” within the keyspace with the following attributes car_id (uuid, primary key), brand (textual), max_speed (integer), price (float), consumption_lt_per_km (float) and sorted by max_speed in ascending order.
``` cql
CREATE TABLE car(
	car_id uuid,
	brand text,
	max_speed int,
	price float,
	consumption_it_per_km float, 
	PRIMARY KEY (car_id, max_speed) )
)
WITH CLUSTERING ORDER BY(max_speed ASC); 
``` 
 - Add a new column to the table, named “features” that contains the set/list of features of the cars (e.g., air conditioning, etc.). Each “feature” is made of name and description.
 ``` cql
 CREATE TYPE feature(
	 name text,
	 description text
 );
 ALTER TABLE car
	 ADD features list<frozen<feature>>;
 ``` 
 NOTE: 
 When it's created a user-defined data type, it's necessary to use the **frozen** keyword. It's possible only to overwritten, NOT to edit anymore.
 - delete features
``` cql
ALTER TABLE car DROP features;   
``` 
- insert a new value in the table, use the function uuid() to get a unique identifier
``` cql
INSERT INTO CAR (car_id, brand, max_speed, price, cosumption_lt_per_km)
VALUES (uuid(), 'Ferrrai', '...', '...', '...');
```