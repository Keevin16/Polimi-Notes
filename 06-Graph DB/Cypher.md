>It's a **declarative query language** for property graph databases, used in Neo4J.

To see all the dataset in a nutshell 
``` Cypher
CALL db.schema.visualization()
CALL db.labels() YIELD label RETURN label
CALL db.relationshipTypes() YIELD relationshipType RETURN relationshipType
``` 

### Create a node
``` Cypher
CREATE  ( p: Person { name: "Emil", from: "Italy", age: 22} ),
		( Person { name: "Tony"})
````
Note:
- It's possible to create multiple nodes in a row

### Create a relationship

``` Cypher
MATCH (a: Person), (b: Person)
WHERE a.name = "Emil" and b.name = "Tony"
CREATE (a)-[r:knows]->(b)
return 
````
Note:
- It's possible to create multiple relationships between the same entities

### Delete ALL

``` Cypher
MATCH (n) DETACH DELETE n
````
Note:
- DETACH removes all the relationships before removing the nodes!
	It's not possible to delete a node if there are relationship attached to it!

### Delete Node

``` Cypher
MATCH (n: Person {name : "Tony"})
DELETE n
````
It's the same for the relationship

### Merge (Ensure Uniqueness)
`MERGE` finds or creates the specified pattern.
	If exists it doesn't do nothing, otherwise it creates it
	
``` cypher
MERGE (p:Person {name: "Alice"})
MERGE (p)-[:FRIENDS_WITH]->(q:Person {name: "Bob"})
```

### Optional Match 
If the relationship exists, it is returned. If it does not, `null` is returned in its place.
```cypher
MATCH (a:Movie {title: 'Wall Street'})
OPTIONAL MATCH (a)-->(x)
RETURN x
```
The result will be: |x| ---> |`<null>`|


### Load CSV with Headers
```cypher
LOAD CSV WITH HEADERS FROM 'file:///path/to/file.csv' AS row
MERGE (p:Person {name: row.name})
```
Note: If you omit the "with headers" each row will be treated as a list.

### Create Indexes
They are useful to speed up look ups on a specific property
```cypher
CREATE INDEX FOR (p:Person) ON (p.name)
SHOW IDEXES
```

### Full text Index
For **searching text** with partial matches, stemming, case insensitivity, etc.
```cypher
CALL db.index.fulltext.queryNodes("personIndex", "alice~") YIELD node RETURN node

```

### Create Constraints
Ensure property uniqueness
```cypher
CREATE CONSTRAINT FOR (p:Person) REQUIRE p.name IS UNIQUE
```

### Assert (with WHERE)
 Validate conditions in `WITH` clauses (especially useful for pipelines).
```cypher
MATCH (p:Person)
WITH p, p.age AS age
WHERE age > 18
RETURN p
```

### Paths
- Define paths and work with them.
```cypher
MATCH p = (a)-[:REL_TYPE*1..3]->(b)
RETURN p
```

- **Return Nodes in a Path**:
```cypher
MATCH p = (a)-[:FRIENDS_WITH*1..3]->(b)
RETURN nodes(p)
```

- **Return Relationships in a Path**:
```cypher
MATCH p = (a)-[:FRIENDS_WITH*1..3]->(b)
RETURN relationships(p)
```

### Different type of patterns

- **Unidirectional Relationship**: `(a)-[:REL_TYPE]->(b)`

- **Bidirectional Relationship**: `(a)-[:REL_TYPE]-(b)`

- **Unidirected Relationship**: `(a)--(b)`

- **Variable Length Path**: `(a)-[:REL_TYPE*1..3]->(b)` (1 to 3 hops)

- **Path Definition**: `p = (a)-[:REL_TYPE*]->(b)` (assigns a path to variable `p`)


Full example of: **Importing Data, Creating Nodes, Relationships, and Constraints**
```cypher
// Import data
USING PERIODIC COMMIT
LOAD CSV WITH HEADERS FROM 'file:///people.csv' AS row
MERGE (p:Person {name: row.name})
ON CREATE SET p.age = toInteger(row.age), p.createdAt = timestamp()

// Create Relationships
MATCH (p:Person {name: row.name}), (f:Person {name: row.friend_name})
MERGE (p)-[:FRIENDS_WITH]->(f)

// Create Index
CREATE INDEX FOR (p:Person) ON (p.name)

// Create Unique Constraint
CREATE CONSTRAINT FOR (p:Person) REQUIRE p.name IS UNIQUE

// Query with Aggregation, Skip, and Limit
MATCH (p:Person)-[:FRIENDS_WITH]->(f:Person)
WITH p, COUNT(f) AS friendsCount
WHERE friendsCount > 1
RETURN p.name, friendsCount
ORDER BY friendsCount DESC
SKIP 5 LIMIT 10
```

***

Note: 
- Difference between Match and Merge
	 In Cypher, **`MATCH`** and **`MERGE`** are both used to find patterns (nodes or relationships) in the graph, but they serve different purposes and behave differently when no match is found.

- **`MATCH`**: Used to **find** existing nodes or relationships in the graph. If the specified pattern is not found, `MATCH` returns nothing.
- **`MERGE`**: Used to **find or create** nodes or relationships. If the specified pattern is not found, `MERGE` creates it.

Additional control on Merge:
- **`MERGE`** can be followed by `ON CREATE SET` and `ON MATCH SET` clauses to set properties conditionally based on whether the pattern was created or matched.

```cypher
MERGE (p:Person {name: "Alice"})
ON CREATE SET p.createdAt = timestamp()
ON MATCH SET p.lastAccessed = timestamp()
```
- If `Alice` doesn’t exist, this will create a new node with a `createdAt` timestamp.
- If `Alice` already exists, it will update her `lastAccessed` timestamp.

- **`MATCH`** does not support `ON CREATE SET` or `ON MATCH SET` because it only matches existing data and does not create anything.
***
- Suggested number of Labels for a node is 4

Example:
Say you open up a new database and run the following Cypher command to create a new `(:Movie)` node.

```cypher
CREATE (:Movie {title: "Barbie"})
```

Then, you run the following `MERGE` Cypher statement.

```cypher
MERGE (p:Person {name: "Margot Robbie"})-[:ACTED_IN]-(m:Movie {title: "Barbie"})
```
**How many nodes will exist in your database?**
Due the fact that Neo4j doesn't find all the pattern, the entire pattern will be created, so we'll have three nodes.
1 Person and 2 Movies.


 https://smbud-polimi-summary.vercel.app/content/B_GraphDB/Neo4j_Syntax
***
Data Types accepted:
	- String
	- Integer
	- Boolean
	- Date
	- Float
	- Duration, list, local datetime, localtime, point, zoned datetime, zoned time
