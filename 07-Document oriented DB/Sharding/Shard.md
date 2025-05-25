> A **shard** is a **physical server (or replica set)** that stores a **subset of the data**.

A single shard could be a single [[MongoD]] or a **replica set**

- A full dataset is split across multiple shards
- Each shard handles read/write for its own data

#MongoDB