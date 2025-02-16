### rolling update :
apply updated code to some node and if that's okay  to apply on others (no down time)  

### Backward compatibility:  
Newer code can read data that was written by older code.  
### Forward compatibility:   
Older code can read data that was written by newer code.  

## several format of encoding
Json , XML , Protocol Buffers , Thrift , Avro.

## In memory representation:
When a program is running, data is stored in memory using optimized data structures like:  

Objects (in OOP languages like Java, Python, C++)  
Structs (in C, Go)  
Lists, Arrays (in all languages)  
Hash Tables (Dictionaries in Python, Maps in Java)  
Trees, Graphs, etc.  
These structures use pointers for quick access and modification, making them efficient for CPU operations. But pointers only make sense within a program's memory space—they don't work when sharing data across systems.  


## Data transmission & storage:  
When we need to save data to a file or send it over a network, we must convert it into a self-contained sequence of bytes that doesn't rely on pointers. This process is called serialization or encoding.  

Some common serialization formats:  

JSON (human-readable, text-based, widely used in REST APIs)  
XML (verbose but structured, used in older systems)  
Protocol Buffers (Protobuf) (compact binary format used in gRPC)  
MessagePack, Avro, Thrift (other efficient binary formats)  

#### Example
when we use json(human readable) it make whole json to binary format to transfer contain : , { , } and etc...   
But in protobuf it convert real object to binary without : { } , so it cause less size   
in addition REST use more overheads like metadata of http while gRPC does not contain them.  

### important note :
problem with native language encoding format :   
if language native format (like pickle in python ,java.io.Serializable in java ... ) used , the other side should use same langugae   
