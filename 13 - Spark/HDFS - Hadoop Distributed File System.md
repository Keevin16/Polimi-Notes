## HDFS
HDFS is a core component of the Hadoop ecosystem, designed for storing very large files across a cluster of commodity hardware.

- **Core Concepts:**    
    - **Write-Once, Read-Many:** Best suited for **files that are written once** and then **read many times**.
    - **Large Files:** Works well with a **few large files** (e.g., 100 MB per file) rather than many small ones
    - **Blocks:** Large files are divided into smaller, fixed-size blocks (default 64MB)
    - **Replication:** **Each block is replicated (typically 3 times)** for fault tolerance
    - **Scalability:** Designed to handle systems with over 10,000 nodes and 100 million files, following a horizontal scalability paradigm (adding more standard servers).
    - **Comparison:** Conceptually similar to Google File System (GFS), written in Java.
#### Data Replication
It's a distributed storage, data are stored across **multiple nodes**.
In order to achieve **fault tolerance** each block is **replicated 3 times**.
![[Pasted image 20250623103204.png]]

## HDFS architecture
![[Pasted image 20250623103719.png]]
There're 2 types of nodes:
- [[Namenode]] (Master Node) 
- [[DataNode]](Slave node)
If a DataNode is **Overloaded**, blocks are asynchronously moved to other servers to ensure balanced disk usage across the cluster, avoiding disruption.


### Read op.s
- Client sends an open request for a file to the Distributed FileSystem API.
- Distributed FileSystem requests block locations from the NameNode.
- NameNode returns the addresses of DataNodes storing the blocks.
- The client (via `FSDataInputStream`) directly reads the required blocks from the DataNodes.
- Communication closes.
![[Pasted image 20250623105827.png]]
### Write op.s
- Client sends a create request for a new file to the Distributed FileSystem API.
- Distributed FileSystem requests the NameNode for block allocation and replica locations.
- The client writes data to `FSDataOutputStream`.
- Data is saved in a pipeline of DataNodes (one writes, then passes to the next for replication).
- Information about physical storage location is returned to the client.
- Client closes the stream.
- NameNode's metadata is updated to reflect the new data and its locations.
![[Pasted image 20250623110025.png]]