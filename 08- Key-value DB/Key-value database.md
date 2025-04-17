>The **Key value databases** (or key value stores), are NoSQL database types where **data is stored** as **key value pairs** and **optimized** for reading and writing that data. 
>The **data is fetched** by a **unique key** or a **number of unique keys** to retrieve the associated value with each key. The values can be simple data types like strings and numbers or complex objects.

---
It's a database focused on the **performance**, it's highly-efficient for use case where rapid **look ups** are **frequent**.

Each **key** act as an **ID** and it **points to the corresponding value**.
The **value** is a "black box", the database don't analyze it, just **retrieve**.

Only three operations: 
	**PUT**: given a **key** and a **value** it writes the data on the database
	**GET / DELETE**:  given a **key** it **retrieves** a value from the database


![[Screenshot from 2025-04-16 17-16-01.png]]
#Redis