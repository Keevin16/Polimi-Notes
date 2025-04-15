>Data is distributed randomly. Pick an attribute as **hash_shard_key** and apply an hash function on it (like MD5) ⇒ **every value** is **mapped** to a [[Shard]]

- The hash function **ensure** a **uniform distribution** in all the shards
  
DOWNSIDE:
	This have no human-meaning also if you want to look up for all documents with 20<age<30 (choosing before as age as the hash shard key) you need to look in all shards (20 and 21 could be in different shard even if similar in human-meaning)