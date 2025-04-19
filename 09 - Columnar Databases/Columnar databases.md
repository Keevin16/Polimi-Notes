>***Columnar databases*** are those where the data is stored in ***columns** instead of rows as is done in the traditional ***row-based databases** as they offer impressive benefits in certain types of queries and ***data manipulation** operations.
![[Pasted image 20250418183353.png]]

Obtaining better performance for operations that require applications to **read data** such as **data analytics** and **data warehousing**.

---
### Unsolvable problem with Relational Databases
**Problem with today's data** that can not be solved by relational databases:

- Data is **large** and **unstructured** (hard to process with traditional approaches)
- Need to do a **lot reads and writes**
- **Foreign keys** (relational databases) are **rarely** **used**    
- **Store data** in **columns** (instead of rows)
- Used in **OLAP** (OnLine Analytical Processing) 
	analyse **large dataset** and **greatest** for **statistical** **computations**
- Technology meant for **big data** (for small data columnar database is slower than traditional technology)

---
### Pro / Cons Column or row store

| Row store                           | Column store                                 |
| ----------------------------------- | -------------------------------------------- |
| **+** Easy to add / modify a record | **+** Only need to read in relevant data     |
| **-** Might read unnecessary data   | **-** tuple writes require multiple accesses |

---
### Pro of Columnar databases
- **Efficient compression** 
	you can find on the same column many time the same value, you can compress it
- Improve **bandwidth utilization**
	**only relevant data is read** (not the entire rows), reduce data transferred
- **Improve code pipeline**
- **Improve cache locality**

### Downsize of Columnar databases

- If you **want to read an object** (row) you need to **recombine many columns**
- Increase **Disk seek time**
- increase **tuple reconstruction cost**
	![[Pasted image 20250418184935.png]]Read **few columns**--> **Columnar** databases (red) is **better than row databases** (blue)
    Read a **lot of columns**--> **Columnar** database is **worst then row database**

### Compression
The [[Columnar databases]] are based on the Compression of the data, but it may have **downsize**:
- **Reduce** the **size of the data** but requires **CPU** to **compress and decompress data**
	 >Is the **time** you spend **compressing/decompressing** and sending compressed files **smaller than the time** of **transferring the uncompressed data**? 
![[Pasted image 20250418184851.png]]

**Two category of compression**:
- **[[Loss-less]]**: like zip files 
	when **uncompressed** **contains exactly** the compressed file
- **[[Lossy]]**: **lose some details** that **can not be reconstructed** 
	**avoid** this for **database** to not lose data



#Cassandra
