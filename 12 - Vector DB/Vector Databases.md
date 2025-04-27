Vector Databases are used in AI and ML application, them allows a more efficient and semantically rich data retrieval.

They enable AI system to understand **context and similarity** in large dataset, enhancing search and recommendation system.  

**Data is stored in high-dimensional vector representation**, organized by their semantic similarity,allowing for efficient and meaningful data retrieval based on context.


#### Embedding
Embedding is a **technique** to **transform text, images, or any other data into vectors**.
To achieve it are used **pre-trained** **models** for textual data map words into a multi-dimensional space.
![[Pasted image 20250427115729.png]]
	For this reason in the same vector space is possible to have text, images, videos, ...


#### Locality-sensitive hashing (LSH)

[LSH.8 Locality-sensitive hashing: the idea](https://youtu.be/dgH0NP8Qxa8?si=kvfwpagKBWds6Ffq)

- Hashes similar input items into the same buckets (with high probability) 
    
- I apply hash on the query and check in which bucket it belongs ⇒ then look for similarities in the same bucket
    
- Is not perfect, other similar objects might be in different buckets or the query could be assigned in non-perfect buckets
    

#### Hierarchical Navigable Small World (NHSW)

[Vector Database Search - Hierarchical Navigable Small Worlds (HNSW) Explained](https://youtu.be/77QH0Y2PYKg?si=JyZ7mfdMLogPS3sG) 

- Multi-layer graph structure to quickly find items (vectors) similar to a query
    
- It is composed of two parts:
    

#### Navigable small-world graphs

- Nodes closer to each other in the vector space (aka similar vectors) are connected ⇒ form a graph structure
    
- New points are inserted into HNSW graph in a probabilistic manner ⇒ points are inserted randomly in one layer and it is connected to the new point closer at that level
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfx6QAaNus1NTYMJ16l7ucY5ux7y_OoE2mzCr3ZOxrhH_SfERAInRkz8JF1A0Y8h4sNy1lDchi0zvpHLDTRDMSmta_9zAKyVBL3A8TdA6JrcLBgjYkT5W7xrbjYEs0uU_h3xNdeow?key=DDKEe4jduIwpIlfHpvXbowkY)

#### Hierarchical Structure

- Each layer contains fewer nodes than the layer below
    
- As you going down more detailed points are added 
    
- When a query is made the algorithm search for the nearest neighbor in the top layer 
    
- Each layer contains more nodes than the previous one
    
- When we find a value greater than 11 we go down one layer
    
- By the time you reach a denser layer you are in “the neighborhood” of the correct item ⇒ only search a small subset rather than the entire dataset
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcxZEFs3jJz50kDdEnMRzXKxM_VdNboUTWJgEQpaMng01t6IoY5ru0hBqBfGEMJnaJZ4KDr2Yvyv0P3JE3B4zxdBUrdBmecc92_YjxzTlyiRr6KwSCYHWGDgVMrvEjWvOf6IwGZ?key=DDKEe4jduIwpIlfHpvXbowkY)

### Inverted File with Product Quantization (IVFPQ)

- Cluster vectors into groups
    
- Each vector is assigned to the nearest cluster 
    
- After clustering, each vector in a cluster is compressed using product quantization
    

- Each vector is divided into smaller sub-vectors and each sub-vector is quantized separately (more memory efficient)

to do one day...