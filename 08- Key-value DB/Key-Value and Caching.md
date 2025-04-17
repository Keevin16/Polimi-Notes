>def: **Caching**
	 store smaller, faster and more efficient partial copy of the data located closer to where is needed (to reduce access time of frequently needed data)

**Caches** are **implemented** as **key-value** (constant time access)

**Cache hit** & **cache miss** (ACSO)
- **Cache hit**: data is found in the cache ⇒ fast retrieval 
- **Cache miss**: data not in the cache ⇒ need to grab data from the database (slower)

**Hit ratio** = [hits / (hits + misses)] ⇒ probability of finding the data in the cache 
**Miss ratio** = (1 - hit ratio) ⇒ probability of not finding the data in the cache
⇒ a cache is good if the hit ratio is high

  

#### When to cache

**Cache** are only **efficient** when the **benefits of faster access** **outweigh** the **overload of checking** and **keeping cache up to date**

- Need to check the cache if data is there
- Need to have a low miss ratio
- Avoid to keep rarely access data

Use temporal locality to decide what to keep in the cache and what not
- Data that has been access recently is likely that will be used again very soon