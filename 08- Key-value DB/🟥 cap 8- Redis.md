>**Redis** which is the name for "**REmote DIrectionary Server**" is an advanced [[Key-value database]],  where **keys** can contain **[[data structures]]** such as **strings**, **hashes**, **lists**, **sets**, and **sorted sets**. Supporting a set of atomic operations on these data types. 

---
Redis **could be used** as: 
	**Database**, because it can persist data to the disk (http://try.redis.io)
	**Caching layer** because is fast
	**Message broker** 

>**Best fit** for rapidly changing data with a foreseeable (predicable) database size

Good when:
	**Speed** is critical
	**More** than just a **key-value** pairs
	**Dataset** **can fit** in **memory**
	**Dataset** is not **critical**


---
Redis **is not**:
	Replacement for **Relational Database** nor **document-oriented database**
		it may be used **complementary** to a Relational!
	Good to achieve **persistency**
		even though it offers configurable mechanism for **persistency**, this will lead to **increase the latency** and **decrease the throughput**. 


**Architecture**:
![[Screenshot from 2025-04-16 17-39-47.png]]


Here is possible to check how to [[Scaling Redis]].
Here how to deal with [[Key-Value and Caching]]

---
NOTE:
	written in **C**
	Single threaded server
		for this reason is possible to do a single action per time!
		Everything is sequential so it's not important to take in account the conflicts
	Every **operation** is **atomic**
	It have O(1) complexity ⇒ take same amount to retrieve 1 MB or 200 TB of data
	[[not Open source]]
#Redis