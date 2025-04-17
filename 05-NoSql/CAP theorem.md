> **In any distributed system, you can only guarantee at most two of these three properties at the same time**:
>
1. [[Consistency]]   
    Every read returns the **most recent write** (i.e., all nodes see the same data at the same time).
2. [[Availability]]   
    Every request gets a **response** (success or failure), even if some nodes are down.
3. [[Partition Tolerance]]   
    The system **continues to work despite network failures**, delays, or message losses.

---

---
It's a complete trade off between [[Consistency]] and [[Availability]]  at operation level!
![[Screenshot from 2025-04-14 12-04-07.png]]>

#NoSql