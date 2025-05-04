>The driver in Neo4j is a way to establish a connection with the Neo4j database.
>To access the data is used BOLT, which default port is 7687.

It's possible to do a secure connection with: 
	bolt+s
	Neo4j + s
	Neo4j + ssc (The driver will establish an encrypted connection but it will not verify the SSL certificate)

A statement of results comprises a stream of records.

Ex:
```python
driver = GraphDatabase.driver(
    "neo4j://localhost:7687" auth=("neo4j", "letmein")
)

df = driver.execute_query
(
    "MATCH (n) RETURN count(n) AS count",
    result_transformer_=Result.to_df
)
```

When there's a failure on a transaction will be automatically retrieved a **Transaction Functions**