# CloudWatch

- CloudWatch Metrics
  - Provided by many AWS services
  - EC2 standard: 5 minutes, detailed monitoring 1 minute
  - EC2 RAM is not a built-in metric
  - Can create custom metrics: standard resolution 1 minute, high resolution 1 sec
- CloudWatch Alarms
  - Can trigger actions:EC2 action (reboot, stop, terminate, recover), Auto Scaling, SNS
  - Alarm events can be intercepted by CloudWatch Events
- CloudWatch Dashboards
  - Display metrics and alarms
  - Can show metrics of multiple regions

# CloudWatch Events

- Intercept events from AWS services
- Example:EC2 Instance Start, CodeBuild Failure, S3, Trusted Advisor
- Can intercept API call with CloudTrail integration

Notable targets:
- Compute: Lambda, Batch, ECS task
- Orchestration: Step Functions, CodePipeline, CodeBuild
- Integration: SQS, SNS, Kinesis Data Streams, Kinesis Data Firehose
- Maintenance: SSM, EC2 Actions

# AWS CloudWatch Logs - Sources

- SDK, CloudWatch Logs Agent, CloudWatch Unified Agent
- Elastic Beanstalk: collection of logs from application
- ECS: collection from containers
- AWS Lambda: collection from function logs
- VPC Flow Logs: VPC specific logs
- API Gateway
- CloudTrail based on filter
- CloudWatch log  agents: for example on EC2 machines
- Route53: Log DNS queries

# CloudWatch Logs

- Log groups: arbitrary name, usually representing an application
- Log stream: instances within application/log files/containers
- Can define log expiration policies (never expire, 30 days, etc)
- Option KMS encryption
- CloudWatch Logs can send logs to:
- Amazon S3
- Kinesis Data Streams
- Kinesis Data Firehose
- AWS Lambda
- ElasticSearch

# CloudWatch Logs Metric Filter & Insights

- CloudWatch Logs can use filer expressions
  - For example, find a specific IP inside of a log
  - Or count occurrences of "ERROR" in your logs
  - Metric filters can be used to trigger alarms

- CloudWatch Log Insights can be used to query logs and add queries to CloudWatch Dashboards

# CloudWatch Logs - S3 Export

- S3 buckets must be encrypted with AES-256 (SSE-S3), not SSE-KMS
- Log data can take up to 12 hours to become available for export
- The API call is CreateExportTask
- Not near-real time or real-time .. use Logs Subscriptions instead

# CloudWatch Logs Agent & Unified Agent

- For virtual servers (EC2 instances, on-premise servers)
- CloudWatch Logs Agent
  - Old version of the agent
  - Can only send to CloudWatch Logs
- CloudWatch Unified Agent
  - Collect additional system-level metrics such as RAM, processes, etc
  - Collect logs to send to CloudWatch Logs
  - Centralized configuration using SSM Parameter Store
- Batch Sends
  - batch_count: number of log events to send (default 1000, min 1)
  - batch_duration: duration of batching for logs events (default & min is 5000ms)
  - batch_size: max size of log events in a batch (default & max is 1 MB)
- Both agents cannot send logs to Kinesis