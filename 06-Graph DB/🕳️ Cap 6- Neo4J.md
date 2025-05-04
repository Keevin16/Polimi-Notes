**Neo4J** is a **[[Graph database]]** designed to store, query, and manage data using a **graph structure** rather than traditional tables. 
#### 🔍 When to use it?
> Use **Neo4j** when your data has **complex relationships** and your queries **depend on them** — and especially when **performance and flexibility** are key.

#### ❌ **When NOT to Use Neo4j**

| Scenario                           | Use Instead                          |
| ---------------------------------- | ------------------------------------ |
| Simple tabular data & reporting    | Relational DB                        |
| Heavy write throughput + flat data | NoSQL (Cassandra, MongoDB)           |
| Analytics on massive batch data    | Data warehouse (BigQuery, Snowflake) |
|                                    |                                      |
 
 **Note**:
	-->It's implemented in Java, that's not the better option because it doesn't have the better performance and reliability. 
	-->[[ACID]]
	-->[[Schemaless]] (Schema - free)
	-->[[Open Source]]
	-->[[Drivers]]
	-->Efficient on nodes but not in whole-graph analysis 
	-----> remark that is not a distributed system, so the CAP theorem is useless


**Software architecture**:
![[Pasted image 20250414145954.png]]
[[Cypher]]

#Neo4J