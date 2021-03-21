# DynamoDB

- NoSQL database, fully managed, massive scale (1,000,000 rps)
- Similar to Apache Cassandra (can migrate to DynamoDB)
- No disk space to provision, max object size is 400KB
- Capacity: provisioned (WCU, RCU & Auto Scaling) or on-demand
- Supports CRUD (Create Read Update Delete)
- Read: eventually or strong consistency
- Supports transactions across multiple tables (ACID support)
- Backups available, point in time recovery
- Integrated with IAM for security


- DynamoDB is made of tables
- Each table has a primary key (must be decided at creation time)
- Each table can have an infinite number of items (=rows)
- Each item has attributes (can be added over time - can be null)
- Maximum size of a item is 400KB
- Data types supported are:
  - Scalar Types: String, Number, Binary, Boolean, Null
  - Document Types: List, Map
  - Set Types: String Set, Number Set, Binary Set

# Primary Keys

- Option 1: Partition key only (HASH)
- Partition key must be unique for each item
- Partition key must be "diverse" so that the data is distributed
- Example: user_id for a users table

- Option 2: Partition key + Sort Key
- The combination must be unique
- Data is grouped by partition key
- Sort key == range key
- Example: users-game table
  - user_id for the partition key
  - game_id for the sort key
- Example good sort key: timestamp

# Indexes

- Object = primary key + optional sort key + attributes
- LSI - Local Secondary Index
  - Keep the same primary key
  - Select an alternative sort key
  - Must be defined at table creation time
- GSI - Global Secondary Index
  - Change the primary key and optional sort key
  - Can be defined after the table is created
- You can only query by PK + sort key on the main table & indexes (!= RDS)

# Important Features

- TTL: automatically expire row after a specified epoch date
- DynamoDB Streams:
  - react to changes to DynamoDB table in real time
  - Can be read by AWS Lambda, EC2..
  - 24 hours retention of data
- Global Tables: (cross region replication)
  - Active Active replication, many regions
  - Must enable DynamoDB Streams
  - Useful for low latency, DR purposes

# DAX

- DAX = DynamoDB Accelerator
- Seamless cache for DynamoDB, no application re-write
- Writes go through DAX to DynamoDB
- Micro second latency for cached reads & queries
- Solves the Hot Key problem (too many reads)
- 5 minutes TTL for cache by default
- Up to 10 nodes in the cluster
- Multi AZ (3 nodes minimum recommended for production)
- Secure (Encryption at rest with KMS, VPC, IAM, CloudTrail...)