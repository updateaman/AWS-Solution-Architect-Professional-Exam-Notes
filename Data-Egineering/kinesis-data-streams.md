# AWS Kinesis Overview

  Kinesis is a managed "data streaming" service

  Great for application logs, metrics, IoT, click streams

  Great for "real-time" big data

  Great for streaming processing frameworks (Spark, NiFi, etc)

  Data is automatically replicated synchronously to 3 AZ

  - Kinesis Streams: low latency streaming ingest at scale
  - kinesis Analytics: perform real-time analytics on streams using SQL
  - Kinesis Firehose: load streams into S3, Redshift, ElasticSearch & Splunk

# Kinesis Streams Overview

- Streams are divided in ordered Shards/Partitions
- Data retention is 24 hours by default, can go up to 7 days
- Ability to reprocess/replay data
- Multiple applications can consume same stream
- Real-time processing with scale of throughput
- Once data is inserted in Kinesis, it can't be deleted (immutability)

# Kinesis Stream Shards

- One stream is made of many different shards
- Billing is per shard provisioned, can have as many shards as you want
- Batching available or per message calls
- The number of shards can evolve over time (re-shard/merge)
- Records are ordered per shard

# Kinesis Producers

- AWS SDK: simple producer
- Kinesis Producer Library (KPL): batch, compression, retries, C++, Java
- Kinesis Agent:
  - Monitor log files and sends them to Kinesis directly
  - Can write to Kinesis Data Streams AND Kinesis Data Firehose

# Kinesis Consumers

- AWS SDK: simple consumer
- Lambda: through Event source mapping
- KCL: check pointing, coordinated reads

# Kinesis Data Streams limits to know

- Producer:
  - 1 MB/s or 1000 messages/s at write PER SHARD
  - "ProvisionedThroughputException" otherwise
- Consumer Classic:
  - 2 MB/s at read PER SHARD across all consumers
  - 5 API calls per second PER SHARD across all consumers
- Consumer Enhanced Fan -Out:
  - 2 MB/s at read PER SHARD, PER ENHANCED CONSUMER
  - No API calls needed (push model)
- Data Retention:
  - 24 hours data retention by default
  - Can be extended to 7 days