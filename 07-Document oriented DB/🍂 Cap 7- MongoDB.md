>MongoDB is a [[document-oriented database]] that stores data within [[Collections]] as [[Documents]].

Thanks to the automatic data-[[Sharding]],  MongoDB became **faster** and **scalable** reaching
- **Better data locality**, due the fact that the **spatial locality** makes the process faster
- **In-Memory caching** possible for the Json, in this way - reduce need to read from disk and speed up response time
- **Distributed architecture** because is easy to replicate
![[Screenshot from 2025-04-15 17-07-02.png]]

The **security 🔒** is achieved thought:
	- **Security Sockets Layer** which is a cryptographic protocol used to **encrypt** data between two parties — typically between a client and a server.
	- **Intra-Cluster communication**, because is possible to communicate **within a cluster of servers or services**  
	-  **Authorization at the database level** --> Read Only/Read+Write/Administrator


MongoDB has 2 different **components**:
- [[MongoD]]: database instance, is installed in every shard/node/server
- [[MongoS]] 
- [[Config Server]]: A special MongoD, storing metadata about the cluster
![[Screenshot from 2025-04-15 18-24-11.png]]

---
Note: 
	--> Works very **well** with the **web** ( because it works with the Json) 
	--> **Horizontal scaling** due the fact that creates multiple copies of the same item
	-->We have **data replication**, for this reason each [[Shard]] can have from 1 to 3 replication
	--> **No transactions**, since I don't need to modify pieces of different docs at the same time 
	--> Data stored as **[[BSON]]** 
	-->[[BASE]]
	-->[[Open Source]]
	-->[[Schemaless]]
	-----> **[[CP]]** 
		**partition tolerance** because it will handle failure without going offline
		 **Consistent** because it will return the result only if the data is consistent in all the replicas
		 **Availability** is only partial, if something is wrong there's an error message 
#MongoDB
