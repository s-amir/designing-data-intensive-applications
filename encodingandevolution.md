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
if language native format (like pickle in python ,java.io.Serializable in java ... ) used , the other side should use same langugae  (Not Cross-Language)  
Some serialization formats allow loading arbitrary classes during deserialization, which an attacker can exploit.   
Built-in serializers are often inefficient in both CPU time and encoded data size.    
Use JSON, Protobuf, Avro, or other data formats that don’t allow arbitrary code execution.  


### JSON and BSON :
1. JSON is a text-based, human-readable format used for APIs and web data exchange, but it is larger and slower to parse.   
2. BSON is a binary format optimized for speed and efficiency, used mainly in MongoDB, supporting extra data types like ObjectId and Date.   
3. JSON is readable but slower, while BSON is compact and faster for database operations.

### Apache Thrift and Protocol buffer :  
they are some serialization framework which obey from schema   
##### these protocol has backward and forward compatibility   

### AVRO
AVRO is a binary serialization format developed within the Hadoop ecosystem, commonly used for efficient data storage and transmission. Its key features include:  

Compact and Fast: AVRO is designed to be compact, enabling efficient storage and faster data processing.  
Schema-based: It uses a schema (written in JSON) to define the structure of data, ensuring that both producer and consumer know the format in advance.  
Dynamic Typing: AVRO supports dynamic typing, allowing data to be processed even if the schema evolves over time.  
Cross-language Support: It provides libraries for many programming languages (e.g., Java, Python, C++) for seamless integration.   
Compression: AVRO supports efficient compression techniques like Snappy, making it suitable for large data processing.  


