# Kinesis Data Firehose

- Fully managed service, no administration, automatic scaling, serverless
- Near Real Time (60 seconds latency minimum for non full batches)
- Load data into Redshift, Amazon S3, ElasticSearch and Splunk
- Supports many data formats, conversions, transformations, compression
- Pay for the amount of data going through Firehose

# Firehose Buffer Sizing

- Firehose accumulates records in a buffer
- The buffer is flushed based on time and size rules


Buffer Size (ex 32 MB): If that buffer size is reached, it's flushed

Buffer Time (ex 1 minute): if that time is reached, it's flushed

Firehose can automatically increase the buffer size to increase throughput

- High throughput => Buffer size limit will be hit
- Low throughput => Buffer time limit will be hit

If real-time flush from Kinesis Data Streams to S3 is needed then use Lambda instead

# Kinesis Data Streams vs Firehose

- Streams
  - Going to write custom code (producer/consumer)
  - Real time (~200 ms latency for classic, ~70 ms latency for enhanced fan-out)
  - Must manage scaling (shard splitting/merging)
  - Data storage for 1 to 7 days, replay capability, multi consumers
  - Use with Lambda to insert data in real-time to ElasticSearch (for example)


- Firehose
  - Fully managed, send to S3, Splunk, Redshift, ElasticSearch
  - Serverless data transformations with Lambda
  - Near real time (lowest buffer time is 1 minute)
  - Automated Scaling
  - No data storage
