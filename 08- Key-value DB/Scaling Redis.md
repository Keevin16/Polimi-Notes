### Persistence

- [[🟥 cap 8- Redis]] keeps **volatile data**, by design will **lose data** after a **shutdown**, in any case it's **possible to configure** it in order to be **persistent**.  

There are two main mechanism to save data:
 -  **Redis database snapshot (RDB)** which makes **periodic snapshot** of data and save it on the disk (for instance, every 5 minute)
 - **Append-Only-Files (AOF)** which **logs** every **write operation** on a file on the disk
	 In this way when Redis restart it **replays the file** to **rebuild the dataset**

---
### Replication
It's possible to replicate with different **topologies**
#### [[Master-Slave - topology 1]]-->[[CA]]
It's possible to split up in two different main nodes:
	**Master**: where the **primary copy** of the data is (possible to read and write)
	**Slave**: **replicate** the **Master** to create a copy 
		the Slave can have its own sub-Slave
		There's no automatic failover!
![[Screenshot from 2025-04-17 13-43-22.png]]

---
### [[Partitioning]] 
Could be different types of partitioning:
- **Client-side**: decides **which node** to **send the data** (like with hashing) or to query

- **[[Proxy-based - topology 3]]** (**[[Twemproxy]]**): is a middleman between client and Redis instance.
	in a nutshell the **client send the request to the proxy** which knows the node/s to query (Smarter way) 

- **Single [[Twemproxy]]**: is connected to multiple master, determines in which one route the data
![[Screenshot from 2025-04-17 13-49-22.png]]

- **Load balance Twemproxy**: load balance distributes the requests to multiple Twemproxy, all of them are connected to all master
	![[Screenshot from 2025-04-17 13-51-16.png]]


- **Query router**: forward the query to the right node, there are several ways
	- Splits-distributes data into **different hash slots** of different subsets of different nodes, by **performing consistent hashing** (hash function on the key of the data).
    - **Multi-key commands** are allowed only if the **requested keys** are in the **same slot**.
	- **Service channel**: **direct communication link between all nodes** (route queries - check nodes)
	- **If master fails, cluster automatically promotes 1 of its slaves** as the new master (**Failover**)
---

### Failover
How to deal and handle master node failure

- **Manual failover**
	**human administrator intervene** and fix it somehow

- **Automatic with [[Redis Sentinel - topology 2]]** (for **master-slave** topology)
	sentinels constantly monitor failover, with a **quorum-based system** decides if there is a failure and promotes one of the slaves to become the new master
	![[Screenshot from 2025-04-17 13-45-23.png]]

- **Automatic failover with [[Redis Cluster - topology 4]]** (Cluster Topology) --> [[AP]]
	cluster consists of **multiple master nodes** and their **associated slave nodes**. **Cluster** **automatically detects failure** and **promotes a slave** to **master**. The new master takes over the failed master's hash slots
		- **Three servers** with **one master** and **two slaves** and **three sentinels**
			in this way **if the master is not working** the **sentinel detect** it and talk to each other ⇒ **decide which slave should replace** the non-working master
	![[Pasted image 20250417135406.png]]

#Redis