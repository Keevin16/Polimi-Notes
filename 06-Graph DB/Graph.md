G is an ordered triple G:=(V, E,f)
	• **V** is a set of nodes, points or vertices
	• **E** is a set, whose elements are known as edges or lines
	• **f** is a function which maps each element of E to an unordered pair of vertices in V
Note: it's an Abstract Data Type (ADT)

---
List of definition for **Graphs**:
	• **Simple Graph** are graphs without multiple edges or self-loops 
	• **Cyclic Graph** if the graph contains a Cycle
	• **Bipartite graph** if V can be partitioned into two set V1 and V2 s. t. $(u,v) \in E$, but there aren't cyclic path!
	• **Connected** if  you can get from any node to any other by following a sequence of edges OR any two nodes are connected by a path.
		• **Strongly connected** if there is a direct path from any node to any other node 
	• **Sparse** |E| = |V| 
	• **Dense**  |E| = |V|^2

There are many other but i reject to do it

---
List of definition for **Paths**:
	• **Path** is a sequence of vertices such that there is an edge from
	each vertex to its successor
		• **Simple path** if each vertex is distinct
		• **Cycle path** if a vertex path to itself

---
**Matrix**
	• **Incidence Matrix** is an E x V matrix. It contains the edge's data.
	• **Adjacency matrix** is a V x V, with boolean values of edge weights.
		If graph is undirected --> the A. matrix will be symmetric 

#Neo4J