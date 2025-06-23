>Sharding is a strategy for **horizontal [[Partitioning]]** (Horizontal Scalability) of data using a [[Shard key]], where each [[Shard]] stores a subset of [[chunks]], ensuring efficient storage and query performance in **distributed databases**.

![[ShardingExample-2257192689.png]]

---
In this way is possible to enable:
	• **[[Scale]]**: needed by Modern applications to support massive
	workloads and data volume.
	• **[[Geo-Locality]]**: to support geographically distributed deployments to
	support optimal UX for customers across vast geographies.
	• **[[Hardware Optimizations]]**: on Performance vs. Cost
	• **[[Lower Recovery Times]]**: to make “Recovery Time Objectives” (RTO)
	feasible.

---
There're several type of [[Sharding]]
	[[Range Sharding]]
	[[Hash Sharding]]
	[[Tag Sharding]]
	[[Random]], which is not optimal because MongoS has to search in **each** **shard** of **each** **document**

#MongoDB