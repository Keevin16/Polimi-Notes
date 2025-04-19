It has the same concept of a traditional **Data Warehouse**, but on the **cloud**.
It's a **Pay-as-you-go** service, for this reason lead to **High scalability, performance, and availability**.

#### Snowflake **Architecture**
![[Pasted image 20250419153845.png]]
It's a **3 layer architecture**
- **Database Storage**
     Stores data in **columnar format** (enables compression + better query performance).

- **Query Processing (Virtual Warehouse)**
    - Executes queries and handles computation.
    - You pay **separately** for:
        - **Storage** (data retention)
        - **Compute** (query execution)

- **Cloud Services Layer**
    - The **coordination hub**.
    - Manages:
        - Authentication
        - Infrastructure scaling and optimization
        - Metadata
        - Query parsing & optimization
        - Everything accessible via **API/cloud**

---
#### Performance optimization 

- Use **dedicated virtual warehouses** for different workloads.
- **Scale up** for known heavy tasks → increase compute power.
- **Auto-scale** for unpredictable workloads → dynamic scaling.
- **Cache-aware workflows** → design jobs to reuse cached results.
- Use **clustering keys** for large tables:
    - Custom partitioning to reduce scanned data.
    - Example: group books by topic to scan only relevant sections.

**Note1**: Snowflake can **auto-replicate virtual warehouses** to meet workload spikes
	it's only important to define the min/max number of cluster for scaling

**Note2**: The caching is fully automatic, there's a 24 -hour retention of results

**Note3**: The file format supported are CSV, JSON, XML, Avro, Parquet, etc.

---
#### Methods

1. **Bulk Load**
    - Classical **import** of **large datasets**.
    - Uses the `COPY` command.
      Steps:
        - Prepare and preprocess data.
        - **Stage the data** (upload to cloud storage like S3/Azure).
        - Use `COPY` from staging area to Snowflake tables.
        - Cloud storage can serve as **cheap long-term raw data**.

2. **Continuous Load**
	- **Real-time** or **incremental streaming data load**.
	- Uses **Snowpipe**:
	    - Automatically loads new data as it becomes available.   
	    - **Does not consume virtual warehouse resources** (compute is handled separately).
	    - Ideal for **real-time data ingestion**.

#DataWarehouse 