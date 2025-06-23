>The fundamental data structure in Spark Core, representing an **immutable**, **fault-tolerant**, and **distributed** collection of data.

- **Key Features:**    
    1. **Distributed:** Logically a single entity but physically spread across multiple nodes.
    2. **Fault-Tolerant / Resilient:** Automatically recovers from node failures through data replication.
    3. **Parallel Operation (Partitioned):** Divided into partitions, each processed independently by different nodes.
    4. **Many Data Sources:** Can be created from diverse sources (HDFS, local files, etc.).
    5. **Immutable:** Once an RDD is created, its value cannot change. New RDDs are created for transformations.
    6. **Lazily Evaluated:** Transformations are not executed immediately but are built into a Directed Acyclic Graph (DAG) of operations. Execution only triggers when an _action_ is invoked.
    7. **Cacheable:** RDDs can be cached in memory to speed up iterative computations, crucial for machine learning algorithms.	
![[Pasted image 20250623113501.png]]