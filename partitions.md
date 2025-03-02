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


 ### rebalancing 

How not to do it: hash mod N
by changing the number of nodes (N) the partition number changed

### Understanding Fixed Number of Partitions
the fixed number of partitions cause adding and removing node is easy 
by adding more nodes the number of partition of each node reduce and by removing the number of each node rduced
problems:
❌ Choosing the Right Number is Hard: If partitions are too big, rebalancing is expensive; if too small, management overhead increases.
❌ Dataset Growth Issues: If data grows beyond expectations, the fixed number of partitions may limit scalability.

![image](https://github.com/user-attachments/assets/6e3da6c2-39bd-4624-ae1a-5b3123233edb)


### dynamic partitions:
Dynamic Partitioning adjusts the number of partitions automatically based on data size.  
Splitting occurs when a partition exceeds a set size (e.g., 10GB in HBase).  
Merging happens when partitions become too small due to deletions.  
Rebalancing moves split partitions to other nodes for load distribution.  


** pay attention that automatic rebalancing can cause problem:  
False Failure Detection – A temporarily slow node may be wrongly considered failed.  
Unnecessary Data Movement – The system moves large amounts of data, increasing network and disk load.  
Overloading Healthy Nodes – Other nodes take extra load, potentially slowing them down too.  
Cascading Failures – More nodes become overloaded, triggering further rebalancing, risking a full system crash.  
🔹 Key Issue: Overreacting to temporary slowdowns can worsen system performance instead of stabilizing it.  


### Request Routing: which data , where ?!
#### service discovery : connect to which node which port!
1. connect to any node : can connect to each node , if node does not have data request forwarded to appropraite node
2. routing tier first: request firest sent to routing tier and this service act as a partition-aware load balancer. (coordination service such as Zoo‐
Keeper to keep track of this cluster metadata)  
3. client aware of partitioning

   ![image](https://github.com/user-attachments/assets/4693e794-2c39-43c7-b05e-c577c6a4aa92)


