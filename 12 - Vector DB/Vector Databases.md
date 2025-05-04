Vector Databases are used in AI and ML application, them allows a more efficient and semantically rich data retrieval.

They enable AI system to understand **context and similarity** in large dataset, enhancing search and recommendation system.  

**Data is stored in high-dimensional vector representation**, organized by their semantic similarity,allowing for efficient and meaningful data retrieval based on context.


#### Embedding
[[Embedding]] is a **technique** to **transform text, images, or any other data into vectors**.
To achieve it are used **pre-trained** **models** for textual data map words into a multi-dimensional space.
![[Pasted image 20250427115729.png]]
	For this reason in the same vector space is possible to have text, images, videos, ...


#### Locality-sensitive hashing (LSH)
![[Pasted image 20250502162711.png]]
- **Hashes similar input** items into the **same buckets** (with high probability) 
	similar hash code!

- I apply hash on the query and check in which bucket it belongs 
	then look for similarities in the same bucket

- Is not perfect, other similar objects might be in different buckets or the query could be assigned in non-perfect buckets
    


#### Queries the Database
For queries the databases there're many ways, it could be **Brute Force** with a time complexity O(n), which is really time expensive.

To deal with this problem one good solution could be the **Navigable Small Worlds**, where each datum on the databases is mapped with the most similar datapoints.
![[Pasted image 20250502163637.png]]

Another data structure to use to looking up for a datum is the **Skip Linked List**
As you go down the layers, more detailed points are added. When a query is made, the algorithm first searches for the nearest neighbor in the top layer. Each subsequent layer contains more nodes than the one above.
![[Pasted image 20250502163900.png]]
	In this example looking up for 11

Combining these two it's possible to talk about Hierarchical [[Navigable Small Worlds - HNSW]] with a time complexity O(ln(N))
![[Pasted image 20250502164129.png]]

It's a multi-layer graph structure to quickly find items (vectors) similar to a query
The new points are inserted into the graph in a probabilistic manner 
	points are inserted randomly in one layer and it is connected to the new point closer at that level.

- It's not guarantee an exact **KNN** but instead is focused on the  speed.

### Inverted File with Product Quantization ([[IVFPQ]])
The IVFPQ is a **fast** and **memory-efficient** algorithm for **approximate nearest neighbor** (ANN) **search**.

**Inverted File Index (IVF)**:
Before all the vector space is divided into a number of **coarse clusters** using a clustering algorithm (e.g., k-means).

- **Each vector** is assigned to the **nearest cluster** (also called a "cell").

- **When querying**, the **algorithm searches** only **within the most relevant clusters**, **reducing the search space** significantly.

**Product Quantization (PQ)**:
Within each cluster, vectors are **quantized** to compress them using product quantization.

- The vector is split into sub-vectors, and each sub-vector is quantized separately using its own codebook.

- This allows efficient storage and fast distance computations using precomputed tables.