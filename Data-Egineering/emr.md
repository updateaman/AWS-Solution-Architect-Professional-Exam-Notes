# Amazon EMR

- EMR stands for "Elastic MapReduce"
- EMR helps creating Hadoop clusters (Big Data) to analyze and process vast amount of data
- The clusters can be made of hundreds of EC2 instances
- Also supports Apache Spark, HBase, Presto, Flink
- EMR takes care of all the provisioning and configuration of EC2
- Auto-scaling with CloudWatch
- Use cases: data processing, machine learning, web indexing, big data

# EMR Integrations

- Launched in your VPC in a single AZ
- EC2 and EBS Volume (HDFS) for temporary storage
- EMRFS (native integration) - uses S3 which gives permanent storage and server side encryption
- Apache Hive can be used to read from DynamoDB

# Node types & purchasing

- Master Node: Manage the cluster, coordinate, manage health
- Core Node: Run tasks and store data
- Task Node (optional): Just to run tasks
- Purchasing options:
  - On-demand: reliable, predictable, won't be terminated
  - Reserved (min 1 year): cost savings (EMR will automatically use if available)
  - Spot Instances: cheaper, can be terminated, less reliable

Can have long-running cluster or transient (temporary) cluster

One big cluster vs many smaller ones? Long running vs transient

# Instance Configuration

- Uniform instance groups: select a single instance type and purchasing option for reach node (has auto scaling)
- Instance fleet: select target capacity, mix instance types and purchasing options (no Auto Scaling)

