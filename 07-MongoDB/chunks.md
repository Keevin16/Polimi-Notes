> A **chunk** is a **logical range of documents** defined by the shard key.

- MongoDB splits each collection into **chunks**

- Each chunk has a **range of shard key values**

- Chunks are **migrated across shards** as needed for **balancing**

>HOW THE DATA IS GROUPED BEFORE TO BE ASSIGNED TO A SHARD
