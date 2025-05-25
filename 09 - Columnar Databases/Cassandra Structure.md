In Cassandra, data is organized into a **hierarchy**:
- At the top level, there is a **[[cluster]]**, which is a **group of connected machines** (nodes) that work together.
- Inside a [[cluster]], you define one or more **[[keyspaces]]** — **similar to databases** in relational systems. The [[keyspace]] also defines **replication settings**.
- Within [[keyspaces]], you have **tables** (also called [[column families]]), which are similar to SQL tables and **store your actual data**.
- A **row** in a table is uniquely identified by a **primary key**, which consists of a **[[Partition Key]]** and optional **[[Clustering Key]]**.
- Each row contains **[[columns]]**, and each column holds a **cell**, which is the actual value + **timestamp** to resolve the problem of consistency.
- Cassandra supports **wide rows**, meaning **rows can have a dynamic set of columns**.

**Summary**:
![[Pasted image 20250418192259.png]]

Having **more in detail**:
![[Pasted image 20250418192903.png]]

---
This structure is designed to optimize for **high write throughput**, **scalability**, and **fast reads by primary key**. Data is often **denormalized** and modeled based on **query patterns**, since joins and foreign keys are not supported.

#Cassandra