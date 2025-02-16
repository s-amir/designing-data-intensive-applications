# designing-data-intensive-applications
__________

This repository contains key insights and notes from Designing Data-Intensive Applications by Martin Kleppmann. The book explores the fundamental principles behind scalable, reliable, and maintainable data systems.

Overview

Modern applications are increasingly data-intensive rather than compute-intensive. The book explores how to design systems that efficiently manage large-scale data while ensuring reliability and maintainability.

Key Concepts

## 1. Data-Intensive vs. Compute-Intensive Applications

CPU is rarely the bottleneck; instead, challenges arise from data volume, complexity, and speed.

Systems are built using a combination of:

### Databases (e.g., PostgreSQL, MongoDB)

### Caches (e.g., Redis, Memcached)

### Search Indexes (e.g., Elasticsearch, Apache Solr)

### Stream Processing Systems (e.g., Apache Kafka, Flink)

### Batch Processing Systems (e.g., Apache Hadoop, Spark)

## 2. Design Goals of Data Systems

A well-designed data system should focus on three core principles:

### Reliability

Ensures the system continues functioning correctly despite faults.

Handling Hardware Failures: Use redundancy (RAID, backups, multi-region deployment).

Mitigating Software Bugs: Implement process isolation, self-checking mechanisms, and failure simulations.

Preventing Human Errors: Design safe defaults, enable rollbacks, and use monitoring tools.

### Scalability

Ensures the system can handle increasing amounts of data and traffic.

Partitioning (Sharding): Splitting data across multiple nodes.

Replication: Keeping multiple copies of data for fault tolerance.

Indexing & Caching: Improving query performance.

### Maintainability

Ensures the system remains easy to modify and extend over time.

Clear Abstractions & APIs: Reduces complexity.

Automation: Prevents human errors.

Observability: Logging and monitoring for troubleshooting.


## How Important Is Reliability?
Reliability is critical in all applications, not just in high-stakes industries like nuclear power or aviation. Business applications with bugs can lead to lost productivity, financial errors, and legal risks. Even in non-critical applications, data loss can severely impact users. While reliability may sometimes be sacrificed for cost-saving purposes, such decisions should be made consciously and carefully.

## Scalability
A system that functions well today may not necessarily perform well under increased load. Scalability refers to a system’s ability to handle growth efficiently. Instead of simply labeling a system as “scalable” or “not scalable,” we should analyze how it copes with growth and what strategies can be employed to manage increased demand.

## Describing Load
To assess scalability, it is essential to define load parameters, such as:

Requests per second on a web server
Read/write ratios in a database
Active users in a chatroom
Cache hit rates
A real-world example is Twitter, which initially stored tweets in a centralized manner, making timeline queries inefficient. To improve performance, Twitter switched to a model where each user has a precomputed timeline cache. However, this introduced challenges when users with millions of followers posted tweets, requiring a balance between real-time computation and storage efficiency.

## Describing Performance
Performance can be evaluated in two ways:

Impact of increased load on performance (keeping resources the same)
Required resource expansion to maintain consistent performance under higher load
### Latency vs. Response Time
Latency: The time a request spends waiting to be processed.
Response Time: The total time taken to process a request, including delays.
Response times vary due to factors such as network congestion, CPU scheduling, garbage collection pauses, and disk reads.

## Approaches for Coping with Load
As load parameters increase, maintaining good performance requires rethinking system architecture. Scaling can be done in two primary ways:

#### Scaling Up (Vertical Scaling) – Moving to a more powerful machine.
#### Scaling Out (Horizontal Scaling) – Distributing the load across multiple smaller machines (shared-nothing architecture).
A single-node system is often simpler, but high-end machines become expensive, making horizontal scaling necessary for intensive workloads. Many modern architectures use a pragmatic combination of both approaches.

### Elastic vs. Manual Scaling:

Elastic systems automatically adjust computing resources based on demand.
Manually scaled systems require human intervention but are often simpler and more predictable.
### Stateful vs. Stateless Systems:

Stateless services are easy to distribute across multiple machines.
Stateful data systems require more complex distributed setups. Traditionally, databases were scaled vertically, but better distributed system tools may make horizontal scaling the default in the future.
Scalability: No One-Size-Fits-All Solution
Different applications require different scalable architectures, depending on factors like:

Read/write volume
Data storage needs
Complexity of data
Response time requirements
For example, a system handling 100,000 requests per second (1 kB each) differs from one handling 3 requests per minute (2 GB each), even if both have the same total data throughput. Scalable architectures must be designed based on expected workload patterns.

### Maintainability: The Cost of Software Is in Its Maintenance
Most software costs come from ongoing maintenance rather than initial development. Legacy systems can be difficult to maintain, so software should be designed for long-term usability. Three key principles help improve maintainability:

Operability – Make it easy for operations teams to keep the system running smoothly.
Simplicity – Reduce unnecessary complexity to make the system easier to understand.
Evolvability – Ensure the system can be easily adapted for new use cases and future changes.
Operability: Helping Operations Teams Manage Systems
Operations teams handle tasks such as monitoring, troubleshooting failures, keeping systems updated, and ensuring security. Good operability makes routine tasks easier and prevents operational surprises.


Key strategies for reducing complexity:

Remove accidental complexity (implementation details that do not contribute to solving the problem).
Use abstractions to simplify interactions and hide unnecessary details (e.g., high-level programming languages hide machine code).
Design reusable components to improve efficiency and software quality.
Evolvability: Designing for Change
Software requirements will inevitably change over time due to business needs, regulations, or system growth. A system designed with evolvability in mind is easier to modify and adapt.

____
____
## Relational vs. Document Databases Today
#### Document Model Advantages:

Schema flexibility: No rigid table structure; easier schema evolution.
Performance benefits: Locality of related data improves read performance.
Closer alignment with application data structures.
#### Relational Model Advantages:

Better support for joins: Handles many-to-many relationships more efficiently.
Optimized query execution: Automatic selection of best access paths.
Simplicity for interconnected data: Avoids excessive denormalization.
#### Schema-on-Write vs. Schema-on-Read
Relational databases enforce schemas at write time ("schema-on-write"), ensuring data consistency but requiring migrations when structure changes.
Document databases use "schema-on-read", allowing flexible data storage but requiring application logic to handle different formats dynamically.

### Data locality 
Document databases store data as a single continuous string (e.g., JSON, XML, or BSON). This locality of storage can improve performance when applications frequently retrieve entire documents, reducing the need for multiple index lookups and disk seeks.

However, this advantage diminishes when:

Only a small part of a document is needed, as the entire document must still be loaded.
Updates increase the document’s size, requiring a full rewrite instead of an in-place modification.
Thus, keeping documents small and avoiding size-increasing updates is recommended to maintain performance.

#### Locality in Other Database Models
The concept of data locality is not unique to document databases. Other database systems also optimize locality:

1.Google Spanner allows relational tables to be interleaved for better locality.   
2.Oracle supports multi-table index cluster tables.   
3.Bigtable-based databases (Cassandra, HBase) use column families to manage locality.     

#### Declarative languages focus on what the program should accomplish without specifying how it should be done. You describe the desired result, and the system figures out the steps (e.g., SQL, HTML).

#### Imperative languages focus on how to achieve the result. You define the exact sequence of steps to perform (e.g., Python, Java).

Declarative: Easier, more concise, but less control over execution.
Imperative: More control, but requires specifying each step, which can be more complex.

___
____
## Hash Index:
This index creates a hash map (hash table) in memory. When you want to fetch a key, it computes the hash of the key and directly finds the offset of the value in memory.   
The time complexity is O(1) for lookups.   
It is not suitable for range queries (e.g., finding values between a range).    
The hash index must fit entirely in memory, and the storage is append-only. When a value is updated, the new value is appended to the end of the log, and the system periodically performs compaction to remove old versions and reduce storage.   

## binary tree
data persist in tree   
disadvantage: not balanced (unbalanced tree)   

## BTree (Balanced Tree)  
this tree change root automatically to create balanced tree  

## B+ Tree 
B+ Tree is useful for range query (find near data)    
each node point to two node (ochild and next data)  
![image](https://github.com/user-attachments/assets/646337c6-3abf-4f3b-be23-16e0c2ce4a3b)  
B+ Tree is also useful in size because we can persist upper portion of index in memory which is just pointer and downer portion in disk which is larger and has addreess of values  

## clusterd index :
Each table can only maintain one cluster index ,  the cluster index has the same index as the data in the table sort (so we can have only one cluster index per table)  
In cluster index if you change the id (if index is based on id) the index must be change too   
Unlike non-clustered indexes that store references to rows, a clustered index stores the actual row data. When you search using the clustered index, it directly points to the row in the table, not just a reference.

## nonclusterd index
It stores the indexed column(s) and pointers to the actual rows in the table, but does not change the table’s row order.  
You can have multiple non-clustered indexes on different columns.  
The actual data is stored in the table, and the index points to it. This is different from a clustered index, which stores the data in the same order as the index.  
Example: If you have a clustered index on id and create a non-clustered index on name, the non-clustered index stores name values and pointers to where the actual name data is in the table.   
So, non-clustered indexes help speed up queries without changing how the data is stored in the table.   

### summary 
Clustered Index: Best for the primary key, range queries, and when there is a need to keep the data sorted.   
Non-Clustered Index: Useful for speeding up lookups on non-primary key columns, allowing multiple indexes, and maintaining a flexible table structure.   

### Which index is better for frequently changed column ?   
if a column changes a lot (like someone's name), a non-clustered index is better because it just updates the pointer in the index without changing the actual data order. A clustered index would require physically moving rows in the table, which is slower.  

## concatenated index (Multi columns index) : 
we can create index based on multiple column   
for example lat and lon   
if we use first column of index in the query , the index is still useful but if we use second column alone it does not effecient 

## OLAP and OLTP
![image](https://github.com/user-attachments/assets/6c5dc4de-4484-4c84-b616-f1767b1c94e3)


## Star and Snowflake Schema:
A star schema is a data model used in data warehouses with a central fact table surrounded by dimension tables.   
The fact table captures transactional events, like customer purchases or website clicks, and contains foreign keys to dimension tables.   
Dimension tables store descriptive attributes (e.g., product details, store information), answering questions like "who, what, where, when."    
The schema’s name comes from its star-like structure when visualized, with the fact table at the center.   
A snowflake schema is a variation where dimensions are further normalized into sub-dimensions.    
In snowflake schemas, dimension tables are broken into more granular tables (e.g., separate tables for product brands and categories).     
Snowflake schemas are more normalized than star schemas, making them more complex but potentially saving storage.    
Star schemas are often preferred in analytics due to their simplicity and ease of use for analysts.   

  
