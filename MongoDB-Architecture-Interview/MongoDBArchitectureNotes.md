https://learning.oreilly.com/library/view/practical-mongodb-architecting/9781484206478/A332296_1_En_7_Chapter.html

MongoDB Architecture

7.1 Core Process

MongoD - Core Database Processor
Mongos - Controller, Queru Router for Shared Clusters
mongos is used in MongoDB sharding. It acts as a routing service that processes queries from the application layer and determines where in the sharded cluster the requested data is located
Mongo - Shell

7.3 Standalone Deployment

![StandaloneDeployment](StandaloneDeployment.png)
 a single mongod and a client connecting to the mongod

7.4 Replication

 7.4.1 Master/Slave Replication
![
    
](image.png)
Here's a concise bullet-point summary of the content regarding Figure 7-2 (Master/Slave Replication):

**Master/Slave Replication System:**
- **Master Node**:
  - Maintains a capped collection called **oplog** (operations log)
  - Stores ordered history of all logical write operations
  - Serves as the single source of truth for data changes

- **Slave Nodes**:
  - Replicate data by reading from master's oplog
  - Apply operations in same order as master recorded them

**Critical Limitation**:
- Oplog is a **capped collection** (fixed size)
- If slave falls too far behind master:
  - Slave's replication stops completely
  - Requires **manual intervention** to resync
  - Automatic recovery not possible in this state

**Two Main Causes of Slave Falling Behind**:
1. **Prolonged Slave Downtime**:
   - When slave is offline longer than oplog can retain history
   - Misses operations that were purged from capped oplog

2. **Slave Processing Delay**:
   - Slave cannot keep up with master's write throughput
   - Eventually falls outside the oplog's retained history window

*(Note: The actual two reasons aren't fully specified in the provided content - these are the most common scenarios implied by the description.)*