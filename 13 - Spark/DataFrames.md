  > **Definition:** A higher-level abstraction built on top of RDDs, representing **immutable**, **distributed collections** of data **organized into named columns** (like tables in a relational database).

- **Advantages:**        
    - **User-Friendly API:** More intuitive and accessible from different programming languages (Python, Scala, Java, R).
    - **Optimized:** Leverages Catalyst Optimizer to build an Abstract Syntax Tree (AST) for queries, leading to highly optimized execution plans.
    - **SQL-like Operations:** Supports direct SQL queries or methods that resemble SQL syntax.