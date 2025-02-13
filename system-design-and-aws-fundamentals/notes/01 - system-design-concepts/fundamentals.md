## Designing the Scalable System

### Step 1 - Small scale System
Setup a single user system and scale it to millions of users. 
#### Building Blocks
**Client <=DNS=> Web Server <=> Database**
 - Client (Web/Mobile) **REQUEST**s data via web address.
 - Web address is resolved via DNS to IP address of the server.
 - Server processes the request internally of communicating with database and sends the **RESPONSE** back.
 - Client may recevie __JS,CSS, HTML, JSON__ etc. as the response.

#### Choice of Database
 1. **Relational databases** also called as relational database management system (RDBMS) or SQL database. represent and store data in tables and rows. You can perform join operations using SQL across different database tables. The most popular ones are __MySQL, Oracle database, PostgreSQL__, etc.
 > Relational databases are the best option because of storng and robust historical presence and relational data structure. However, if relational databases are not suitable for your specific use cases.
 2. **Non-Relational databases** are also called *NoSQL* databases. Some popular ones are __CouchDB, Neo4j, Cassandra, HBase, Amazon DynamoDB__, etc. These databases are grouped into four categories: 
     1. Key-value stores
     2. Graph stores
     3. Column stores
     4. Document stores. 
    Join operations are generally **not** supported in non-relational databases.
    Non-relational databases might be the right choice if:
     - Application requires super-low latency.
     - Data are unstructured, or you do not have any relational data.
     - Only need to serialization and deserialization data (JSON, XML, YAML, etc.).
     - Need to store a massive amount of data.

---

### Step 2 - Making the System Available & Reliable
#### Scaling the System
 To make the System relaible and available for increasing number of users and processes, we can either **Scale-up** (Vertically) o **Scale-out** (Horizontally)
 
 | Vertial Scaling | Horizontal Scaling |
 |-----------------|--------------------|
 |Increase the power of machine (CPU, RAM, etc.)|Add more machines/severs to distribure load and increase capacity|
 |Single point of failure. if the server goes down, system is down| Systems is reselient due to distributed load|
 |Limited by hardware in case of high load| No such limitation due to multiple servers|
 |Uses IPC| Uses RPC|
 |Data is consistent|Data consistency needs to be handled explicitly|
 
 > **Horizonal Scaling** is most desirable technique given the shortcomings of vertical scaling

#### Load Balancing 
A load balancer evenly distributes incoming traffic among web servers that are defined in a load-balanced set.
           **Web Server 1**
           **||**
**Client <=DNS=> Load Balancer**
           **||**
           **Web Server 2**

 - Client interacts with public IP address of Load balancer while the web servers are inaccessible directly due to private IP address
 - Load Balancer(LB) intelligently routes the request to available web servers through an effecient algorithm
 - If either of the server goes down, LB routes the request to next available/healthy servers.
 - In case of increased loads, number of servers can be increased in the server pool to balance to load 


#### Database Replication
It is the technique to scale the data layer in order to balance the increasing load.**Master-Slave** mechansim