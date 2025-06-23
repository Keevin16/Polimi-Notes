It's a [[Columnar databases]] management system highly scalable, high-performance and distributed; designed to handle **large amounts of data**, providing **high availability** with **no single point of failure**.

[[Cassandra Structure]] ---  How component are organized
[[Cassandra Architecture]] --- Overall design of the system (Structure + Behavior)

| Feature           | Description                                                                       |
| ----------------- | --------------------------------------------------------------------------------- |
| [[Open Source]]   | Yes                                                                               |
| Origin            | Designed at Facebook                                                              |
| Architecture      | Fusion of Google Bigtable (**column-based**) + Amazon Dynamo (**key-value**, DHT) |
| Consistency Model | Tunable consistency                                                               |
| CAP Focus         | [[AP]] (Availability + Partition Tolerance)                                       |
| Memory Usage      | Works in **main memory**                                                          |
| Schema            | **No joins, no foreign keys, no normalization**                                   |
| Redundancy        | Allows data redundancy                                                            |
| Performance       | **Very fast writes and reads**                                                    |
| Fault Tolerance   | **Masterless**, **no single point of failure**, commit log + replication          |
| Node Roles        | **Decentralized**, symmetric (all nodes equal)                                    |
| Durability        | **Data persists even after crash** (commit log + replication)                     |
| Scalability       | **Linear and elastic** (automatic redistribution)                                 |
| Integration       | Easy via API                                                                      |
| Data Lookup       | **O(1)** time via Distributed Hash Table **(DHT)**                                |
| Use Case          | Optimized for **big data** (less ideal for small datasets)                        |
| Properties        | [[BASE]] (Basically Available, Soft state, Eventually consistent)                 |
### Cassandra vs RDBMs

| Property                  | Cassandra                                                                                 | RDBMSs                                                                                                   |
| ------------------------- | ----------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| Core Architecture         | **Masterless** (no single point of failure)                                               | **Master-slave** (single points of failure)                                                              |
| High Availability         | **Always-on** continuous **availability**                                                 | **General replication** with **master-slave**                                                            |
| Data Model                | Dynamic, **structured** and **unstructured** data                                         | Legacy RDBMS: **structured data**                                                                        |
| Scalability Model         | **Big data** / linear scale performance                                                   | Oracle RAC or Exadata                                                                                    |
| Multi-Data Center Support | **Multi-directional, multi-cloud availability**                                           | Nothing specific                                                                                         |
| Enterprise Search         | Integrated search on Cassandra data                                                       | Handled via Oracle search                                                                                |
| In-Memory Database Option | Built-in in-memory option                                                                 | Columnar in-memory option                                                                                |
| Joining                   | Does **not support joining**                                                              | **Support joining**                                                                                      |
| Referential Integrity     | Cassandra has **no concept of referential integrity** across tables. No cascading deletes | Support foreign keys in a table to reference the primary key of another table. Supports cascading delete |
| Normalization             | **Tables contain duplicate denormalize data**                                             | **Tables normalized to avoid redundancy**                                                                |
RDBMs :
![[Pasted image 20250418190631.png]]
Cassandra:
![[Pasted image 20250418190714.png]]
#Cassandra