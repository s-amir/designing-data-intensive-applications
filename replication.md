
## multileader configuration:
each node(leader) accept write and then sync with other nodes 
example: couchDB is good for multileader configuration
### How It Works in CouchDB:
1. Document-Based Model: CouchDB uses a schema-free, JSON-based document model, which makes conflict resolution easier.
2. Replication Protocol: CouchDB’s replication is incremental and uses a pull-based approach. Each node independently pulls changes from other nodes.
3. Conflict Handling: When a conflict arises (e.g., the same document updated differently on two nodes), CouchDB retains both versions and marks the document as conflicted. It's up to the application to resolve the conflict.
4. Eventual Consistency: Data might not be immediately consistent across all nodes, but it eventually converges as replication synchronizes changes.

one problem in multi-leader replication system is conflict with changes (requiring conflict resolution) :
1. LWW last write wins (may cause data lost)
2. Somehow merge the values together
3. use seperate programe to handle it
4. ![image](https://github.com/user-attachments/assets/262d51d2-b7a8-4da4-ab81-ff956100c438)

### Dynamo-style (like cassandra)
this fashionable architecture is leaderless approach where client send multiple request for write to several replicas (while in others, a coordinator node does this on behalf of the client)
#### Write Request Flow:
When a client sends a write request:
Coordinator Node: The client can connect to any node in the cluster. The chosen node acts as the coordinator, handling the request.     
Replication to Nodes: The coordinator forwards the write to all replicas responsible for the data (based on the partition key and replication factor).    

and also read request is paralle , means a client connect to chosen node which is coordinator and it sends request to other nodes to get data   
if there are multiple value it returns the newest ones   
Cassandra ensures that there is always at least one replica with the latest data  

