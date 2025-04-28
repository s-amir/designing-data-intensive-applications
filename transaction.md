ACID   
Atomicity : one process done completely (commited) or (rollback)  
Consistency : rules that business define applied to database after and before transaction 
Isolation: separate transaction do not affect on each other
Durability : persistence 

2 phase commit:  
in this scenario we have separate commit on multi data store  
(multi transaction)  

How achieve isolation in transactions:  
1. READ COMMITED
1) no dirty read :   
transaction only see commited rows

2) no dirty write:   
transaction only can change rows that are not open to change by another transaction which are not commited
   
2.Snapshot Isolation --> multi version concurrency controls (MVCC)   Do not avoid LostUpdate   
3.serializable isolation (multi models )