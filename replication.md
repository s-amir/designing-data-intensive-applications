
## multileader configuration:
each node(leader) accept write and then sync with other nodes 
example: couchDB is good for multileader configuration
### How It Works in CouchDB:
1. Document-Based Model: CouchDB uses a schema-free, JSON-based document model, which makes conflict resolution easier.
2. Replication Protocol: CouchDB’s replication is incremental and uses a pull-based approach. Each node independently pulls changes from other nodes.
3. Conflict Handling: When a conflict arises (e.g., the same document updated differently on two nodes), CouchDB retains both versions and marks the document as conflicted. It's up to the application to resolve the conflict.
4. Eventual Consistency: Data might not be immediately consistent across all nodes, but it eventually converges as replication synchronizes changes.
