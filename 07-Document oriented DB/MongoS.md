>MongoS process the **request**, knows **where the data is** and **redirect the query** to the **right shard** (aka decide which [[MongoD]] **should receive the query**).

The user sends a query to the query router ([[MongoS]]), which have a **registry** (config server) that **store** where each data is.
	For **Reading** data, [[MongoS]] will redirect the query to the most efficient node
	For **Writing** instead will redirect the query at the **primary copy**.


#MongoDB