### Partitioning is the process of dividing a large dataset into smaller, more manageable parts (partitions) to improve performance, scalability, and availability in databases and distributed systems.  

### Use Cases:
Faster Queries – Only relevant partitions are scanned, reducing query time.  
Scalability – Data is spread across multiple nodes for better load balancing.  
High Availability – Failure in one partition doesn’t affect the entire system.  
Parallel Processing – Enables efficient data processing in distributed systems.  
Types of Partitioning:  
Range Partitioning – Data is divided based on a range of values (e.g., partitioning orders by date).  
Hash Partitioning – Data is distributed using a hash function (e.g., evenly distributing users across servers).  
List Partitioning – Data is partitioned based on predefined categories (e.g., customers by country).  


### skewed
unfair partitions 

### random partition
Don't know which node contains which data so we must query all nodes and partiotions   
but data may fairly partiotioned!  

### Partitioning by Key Range
selecting key is so important due to avoid hot spot problem (data is unbalanced)

### hash of key :
this method create hash of key and seperate each range of hash to specific partition   
this method is not good for ordered and range query 
not good for range query because ecach record persist in different partition may far from each other!

hashing a key to determine its partition can help reduce hot spots.
However, it can’t avoid them entirely: in the extreme case where all reads and writes
are for the same key, you still end up with all requests being routed to the same parti‐
tion.(for example, on a social media site, a celebrity user with millions of followers , solution is salting )

### Partitioning Secondary Indexes by Document (local index)
in this case each record partitioned based on it's key and also create index on secondary index like (color ,  brand , ..) , this index also called local index because each partition has it's local index   
problem: if i want to search forexample red cars , i must search on all partitions 

![image](https://github.com/user-attachments/assets/9ae4e17e-9348-4b06-9f37-07c6987becd8)


### Partitioning Secondary Indexes by Term (Global Indexing)
 This global index create index of secondary column/field which cause slower write and update but improve read speed.
 A query on "color:red" first checks the global index, then fetches records from the correct partitions (instead of scanning all partitions).  

