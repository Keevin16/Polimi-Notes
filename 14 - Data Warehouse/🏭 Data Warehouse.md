>The Data Warehouse is a **single**, **complete** and **consistent** store of data obtained from a **variety of sources**.
>It's a **big storage facility** for putting all the data together in a compact and organised way
>To helps users make [[Data-Driven]] decision, we use the front-end part of the Data Warehouse, which is the [[DSS]].

**Strict** definition:
 Building a data-store facility that is subject oriented, time-varying and non-volatile  
	 in order to build long term analysis

-->[[Data Warehouse Architecture]]
-->[[Data Warehouse Models]]

-->[[Cloud-Based Data Warehouse]]
![[Pasted image 20250419111953.png]]
>The **Data warehouse layer** is a common space where we **duplicate** all the data and where you **run analytics**.
>In this way there's a **full separation** between **operational systems** - [[OLTP]] and **analytical system**  - [[OLAP]]  avoiding risk!!
>https://www.youtube.com/watch?v=iw-5kFzIdgY

![[Pasted image 20250419112541.png]]
These are the main difference between the standard DB - [[OLTP]] and the Warehouse - [[OLAP]]

| OLTP -  Standard DB                                                             | OLAP - Warehouse                                                               |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| Respect ACID properties (Atomicity, Consistency, Isolation, Durability)         |                                                                                |
| Works with small data per transaction                                           | Works with huge amount of data                                                 |
| Mostly edit data modifications (huge number of small operations) and frequently | Mostly read data (without modify it), run analytics and do not change the data |
| MB/GB of data                                                                   | GB/TB of data                                                                  |
| Typically work on concurrent data (not interested in dating back years ago)     | Look in long-term historical data                                              |
| Use primary keys                                                                | Run scan operations (parcel the data)                                          |
| Huge amount of users                                                            | Number of users is small                                                       |

#DataWarehouse