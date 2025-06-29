Spark is an **open-source** cluster computing framework designed for **fast and general-purpose** large-scale data processing.

### Key Characteristics & Evolution
- **Origin:** Created by AMPLab at UC Berkeley (Matei Zaharia), released in Feb 2013, later donated to Apache.
- **Performance:** **Significantly faster than Hadoop** (up to 100x faster in memory, 5-10x faster on disk), demonstrated by sorting 1PB in 23 minutes with 207 machines compared to Hadoop's 72 minutes with 2100 machines.
- **Unified Platform:** Not just one technology; it's a platform with combinable components (e.g., Spark Streaming, Spark SQL, MLlib).
- **Language Agnostic:** Supports writing code in various languages (e.g., Python with Pandas API, Scala, Java, R), abstracting distributed computation complexities.
- **In-Memory Storage:** **Prioritizes in-memory computation** to minimize disk I/O, leading to speed improvements.
- **Less Code:** Requires 5-10x less code than Hadoop for similar tasks.

### **Spark Components/Layers:**
- **Spark Core:** The distributed execution engine, **providing in-memory computation** and RDDs.
- **Spark Streaming:** Transforms **continuous data streams into small**, discrete **batches for real-time analytics**, making streaming appear continuous.
- **Spark SQL / Shark:** Enables **running SQL queries on structured data** (JSON, Parquet, CSV), offering 100x speedup for in-memory data.
- **MLlib / MLPipelines:** Libraries for machine learning tasks.
- **GraphX:** For **graph-parallel computation**.
- **Unified Programming Models:** Allows using a **single programming language** for **diverse data processing needs** (streaming, SQL, batch, ML)
![[Pasted image 20250623112506.png]]

#### [[RDDs]] (Resilient Distributed Datasets)

#### [[Spark Architecture]] (Runtime)
- **Spark Operations:**
    - **Transformations:**
        - **Purpose:** Define how data is processed; they transform an RDD into another RDD.
        - **Lazy Evaluation:** _Crucially, they are not executed immediately._ They build a logical plan (DAG) of operations. Execution only happens when an action is called. "The fastest way to do something is not doing it."
        - **Examples:** `filter()`, `map()`, `join()`, `groupBy()`, `select()`, `orderBy()`.
        - **Types of Transformations:**
            - **Narrow Transformations (1-to-1):**
                - **Characteristic:** Data required to compute a record in a single partition resides in at most one partition of the parent RDD. Work locally on data within partitions.
                - **No Shuffle:** Does not require data movement across the network (no "shuffle").
                - **Examples:** `filter()`, `map()`, `drop()`, `coalesce()`.
            - **Wide Transformations (1-to-N / Shuffles):**
                
                - **Characteristic:** Data required to compute a record in a single partition may reside in many partitions of the parent RDD.
                    
                - **Shuffle:** Requires data to be shuffled (moved) across the network between different partitions/nodes, which is a costly operation.
                    
                - **Examples:** `distinct()`, `groupBy()`, `repartition()`, `join()`.
                    
    - **Actions:**
        
        - **Purpose:** Trigger the execution of all preceding transformations in the DAG and return a final result to the driver program or save it to external storage.
            
        - **Eager Execution:** No lazy behavior; they provide concrete output.
            
        - **Examples:** `count()`, `collect()`, `save()`, `show()`.
            
- **Spark Job Execution & Scheduling:**
    
    1. **Code (Driver Program):** User writes code (e.g., in Python/PySpark) defining transformations.
        
    2. **SparkContext:** Initiates the Spark environment.
        
    3. **DAG Generation:** Transformations are chained to build a Directed Acyclic Graph (DAG) of RDD operations.
        
    4. **DAGScheduler:** Splits the DAG into "stages" of tasks. Stages are determined by wide transformations (shuffles). It submits each stage to the TaskScheduler when its dependencies are met.
        
    5. **TaskScheduler:** Launches individual "tasks" (smallest unit of work) to the Cluster Manager. It also handles retrying failed or "straggling" (slow) tasks.
        
    6. **Cluster Manager:** Allocates resources on Worker Nodes.
        
    7. **Worker Nodes:** Executors on Worker Nodes run the assigned tasks on data partitions.
        
    8. **Results:** Worker Nodes return results to the Driver Program.
        
    
    - **Fault Recovery:** Spark maintains a log of execution steps and intermediate results. If a node fails, Spark can recompute lost partitions using the lineage of transformations from previous RDDs, similar to database transactions.
        
- [[DataFrames]]
- **Available File Formats Supported by Spark:**
    
    - **Text/CSV:** Plain text or comma-separated values.
        
    - **JSON:** JavaScript Object Notation.
        
    - **SequenceFile:** Hadoop-specific format for key-value pairs.
        
    - **Avro:**
        
        - **Type:** Row-based binary format with a built-in schema.
            
        - **Key Feature:** Language-neutral serialization system, allowing data written in one language (e.g., Python) to be read in another (e.g., Java) – excellent for cross-language compatibility.
            
        - **Structure:** Has a header (metadata, schema), followed by blocks containing auxiliary data, serialized objects, and sync markers (to separate blocks).
            
    - **Parquet:**
        
        - **Type:** Columnar storage file format.
            
        - **Key Feature:** Stores data column by column, offering significant advantages in terms of data locality (reading only needed columns), compression, and encoding efficiency. Optimized for queries that read a subset of columns.
            
        - **Benefits:** Similar benefits to columnar databases but as a file format. It's a state-of-the-art, open-source format optimized for high compression and scan efficiency, especially for nested data.
            
    - **DataFrames:** (Although a Spark abstraction, it's mentioned as a supported "format" for structured data within Spark).
        
    - **ORC (Optimized Row Columnar):** Another highly optimized columnar format.