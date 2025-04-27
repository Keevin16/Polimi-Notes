Cassandra has a [[Ring topology]] for each data center (**Cluster**), as told before it's **masterless**.
![[Pasted image 20250418194956.png]]
### Write
In order to write the **client** sends write command to **one front-end node** in Cassandra **cluster**, which send it to all the **replica node**.
Used the Hinted Handoff principle:
	- If **any replica is down**, the **coordinator writes to all other replicas**, and **keeps** the **write until down replica comes back up**.
	- When **all replicas are down**, the **Coordinator** (front end) **buffers writes** (for up to an hour).

### Read
Possible from each node, it's not important because it's replicated.

### [[Gossip]]
We need to **inform all nodes** about the **other nodes conditions**
	(working, not working, overloaded…)	

![[Pasted image 20250419095356.png]]
**HOW IT WORKS?**
**Each node** picks up to **3 nodes to gossip with**. For each nodes it want to gossip with:
1. **Node X** sends a **synchronization message** to node **Y**. Tells what it knows about the status of other nodes

2. **Y tells to X** that **it receives** the gossip

3. **Node X** tells to **Y** that he **received the confirmation** 

The gossip lead to an **anti-entropy** property
	gossip reconciles and synchronizes inconsistent and out-of-date data between nodes in a distributed system. It ensure that eventually all nodes converge to the same state (eventual consistency)
  



#Cassandra 