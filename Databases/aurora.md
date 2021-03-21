# Aurora

DB Engines: PostgreSQL-compatible & MySQL-compatible

Storage: automatically grows up to 64TB (increments of 10GB), 6 copies of data, multi-AZ (default)

Read Replicas: up to 15 RR, read endpoint to access them all

Cross Region RR: entire database is copied (not select tables)

Load/Offload data directly from/to S3: efficient use of resources

Backup, Snapshots & Restore: same as RDS

# High Availability and Read Scaling

6 copies of your data across 3 AZ:
    - 4 copies out of 6 needed for writes
    - 3 copies out of 6 need for reads
    - Self healing with peer-to-peer replication
    - Storage  is striped across 100s volumes

Automated failover for master in less than 30 seconds

Master + up to 15 Aurora Read Replicas server reads

Support for Cross Region Replication

# Aurora Serverless

Automated database instantiation and auto-scaling based on actual usage

Good for infrequent, intermittent or unpredictable workloads

No capacity planning needed

Pay per second, can be more cost-effective

# Global Aurora

Aurora Cross Region Read Replicas:
    - Useful for disaster recovery
    - Simple to put in place

Aurora Global Database (recommended):
    - 1 Primary Region (read/write)
    - Up to 5 secondary (read-only) regions, replication lag is less than 1 seconds
    - Up to 16 Read Replicas per secondary region
    - Helps for decreasing latency
    - Promoting another region (for disaster recovery) has an RTO of <1 minute

# Aurora Multi-Master

In case you want immediate failover for write node (HA)

Every node does R/W - vs promoting a RR as the new master
