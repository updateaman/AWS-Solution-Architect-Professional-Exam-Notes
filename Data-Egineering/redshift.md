#  Redshift Overview

- Redshift is based on PostgreSQL but it's not used for OLTP (online transaction processing)
- It's OLAP - online analytical processing (analytics and data warehousing)
- 10x better performance than other data warehouses, scale to PBs of data
- Columnar storage of data (instead of row based)
- Massively Parallel Query Execution (MPP)
- Pay as you go based on the instances provisioned
- Has a SQL interface for performing the queries
- BI tools such as AWS Quicksight or Tableau integrate with it

# Details

- Data is loaded from S3, Kinesis Firehose, DynamoDb, DMS
- From 1 node to 128 nodes, up to 160 GB of space per node
- Can provision multiple nodes, but it's not Multi-AZ (all in one AZ)
- Leader node: for query planning, results aggregation
- Compute node: for performing the queries, send results to leader
- Backup & Restore, Security VPC/IAM/KMS, Monitoring
- Redshift Enhanced VPC Routing: COPY/UNLOAD goes through VPC
- Redshift is provisioned, so it's worth it when you have a sustained usage (use Athena if the queries are sporadic instead)

# Snapshots & DR

- Snapshots are point-in-time backups of a cluster, stored internally in S3
- Snapshots are incremental (only what has changed is saved)
- You can restore a snapshot into a new cluster
- Automated: every 8 hours, every 5 GB, or on a schedule. Set retention
- Manual: snapshot is retained until you delete it

You can configure Amazon Redshift to automatically copy snapshots (automated or manual) of a cluster to another AWS Region

# Redshift Spectrum

- Query data that is already in S3 without loading it
- Must have a Redshift cluster available to start the query
- The query is then submitted to thousands of Redshift Spectrum nodes

