## Database Scaling
Database can scaled vertically(Up) or horizontally(out). 

### Vertial Scaling
It is adding more power to service by increasing CPU, RAM, etc. However, scaling-up has de-merits like single point of failure and increased cost due to higher configurations.

### Horizontal Scaling
Also known as **sharding**, which means adding more servers. It is essentially breaking larger DB into smaller managable parts called shards.
 - Each shard has **same schema** however the data may differ.
 - Choice of **Sharding Key** (Partition Key) is importaint while implementing sharding. It can be combination of one or more columns determing the __even__ distribution of data.

#### Potential Complexities
 1. **Resharding data** when:
     - single shard cannot hold more data due to rapid growth
     - certain shards exausting faster due to uneven distribution of data. Sharding Function need to be updated to move the data around
     - **Celebrity/Hotspot Problem** - Excessive access to a specific shard could cause server overload. Further partitioning would be requred to solve the problem
2. **Joins & denormalization**: performing joins across databases(shards) is difficult. A common workaround is to denormalize the database so that queries can be performed in a single table. 