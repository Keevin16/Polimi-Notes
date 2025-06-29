>**Elasticsearch** is a fast, scalable, and versatile **search** and analytics engine that can handle various data types and use cases.

It's built on Apache Lucene, with the purpose to be an internal search engine for large companies to retrieve data, with **database-like capabilities**.

Features:
- **Real-time search**: Documents can be searched almost immediately after being indexed ("loaded" into the database).
- **Short latency**: Optimized for schemaless fast operations on text.
- **Distributed system**: Designed to scale across multiple servers.
- **RESTful API**: Communicates using HTTP and JSON.
- **Full-text search**: Can perform fast, simple searches across huge datasets.
- **Storage format**: Uses JSON documents.
- [[Schemaless]]
- [[CP]]
- **Fast, scalable, resilient**.

---
### From RDBMS to Elasticsearch
| RDBMS Concept | Elasticsearch Equivalent |
| ------------- | ------------------------ |
| Table         | Index                    |
| Row           | Document (JSON)          |
| Column        | Field                    |
| Schema        | Mapping                  |
***
### Relevance and Ranking 

In the traditional databases the queries return **exact matches**.
All result are **equally important** (they all meet the query condition).

Instead in Elasticsearch the queries return the **best match**, results are **ranked** by **relevance** based on how closely they match the user's interest. 

How to compute the Relevance?

**TF-IDF** ---- Term frequency - Inverse Document frequency
Which measures the relevance of a term inside a document, it penalizes the world that are more frequent across different document
- More it **shines** --> More is **important** 
![[Pasted image 20250427113207.png]]
![[Pasted image 20250427113221.png]]

---
### Inverted Index
In relational databases we have **key-value indexing**, **inverted index** is the **opposite** way:
- Index the value and lets you find the ID 
- Used for text analysis and text ranking 
	Elasticsearch **look for the world** (index) and **retrieves the document ID** in which it appears (value)
- **Each document is broken into individual words** (tokens)
- **Each word** is stored **along with the index** of in **which document it appears** in  
- Every world in the text point to all the keys of the document containing that

![[Pasted image 20250427112416.png]]

Based on the [[Sharding]]!
By the way despite of MongoDB, it's all replicated, so there's a division between Primary Sharding and Replica Sharding.

Different from the MongoDB Sharding, there are only two types of mapping:
- **Dynamic Mapping**: Elasticsearch takes care of **adding the new fields** **automatically** when a document is indexed.
- **Explicit Mapping**: Makes the user define the mapping. Drawback: If the user doesn't have the knowledge it'll be a mess, breaking up the index. 

Note: It's not possible to change the mapping on an existing Index that already has document!