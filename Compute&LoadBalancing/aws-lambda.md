# AWS Lambda Integrations

- [API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/getting-started-with-lambda-integration.html)
- [Kinesis](https://docs.aws.amazon.com/lambda/latest/dg/with-kinesis.html)
- [DynamoDB](https://docs.aws.amazon.com/lambda/latest/dg/with-ddb.html)
- [S3](https://docs.aws.amazon.com/lambda/latest/dg/with-s3.html)
- [IoT](https://docs.aws.amazon.com/lambda/latest/dg/services-iot.html)
- [CloudWatch Events](https://docs.aws.amazon.com/lambda/latest/dg/services-cloudwatchevents.html)
- [CloudWatch Logs](https://docs.aws.amazon.com/lambda/latest/dg/services-cloudwatchlogs.html)
- [SNS](https://docs.aws.amazon.com/lambda/latest/dg/with-sns.html)
- [Cognito](https://docs.aws.amazon.com/lambda/latest/dg/services-cognito.html)
- [SQS](https://docs.aws.amazon.com/lambda/latest/dg/with-sqs.html)

# Limits

- [RAM](https://docs.aws.amazon.com/lambda/latest/dg/configuration-memory.html): 128 MB to 3G (10G new limit)
- CPU:
  - is linked to RAM (cannot be set manually)
  - 2 vCPU are allocated after 1.5G of RAM
- [Timeout](https://docs.aws.amazon.com/whitepapers/latest/serverless-architectures-lambda/timeout.html): up to 15 minutes
- /tmp storage: 512 MB (can't process big files)
- Deployment package limit: 250 MB including layers
- Concurrency execution: 1000 - soft limit that can be increased

# Latency

- Cold Lambda Invocation: ~100ms
- Warn Lambda Invocation: ~ms
- New feature of [provisioned concurrency](https://aws.amazon.com/blogs/compute/new-for-aws-lambda-predictable-start-up-times-with-provisioned-concurrency/) (Dec 2019) to reduce # of cold starts

# Security

- [IAM Roles for Lambda](https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html) to grant access to other AWS services
- [Resource-based Policies for Lambda](https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html):
  - Allow other accounts to invoke or manage Lambda
  - Allow other services to invoke or manage Lambda

# Logging, Monitoring and Tracing

- CloudWatch:
  - AWS Lambda execution logs are stored in AWS CloudWatch Logs
  - AWS Lambda metrics are displayed in AWS CloudWatch Metrics (successful invocations, error rates, latency, timeouts, etc.)

* At a minimum, Lambda function needs access to Amazon CloudWatch Logs for log streaming

- X-Ray:
  - It's possible to trace Lambda with X-Ray
  - Enable in Lambda configuration (runs the X-Ray daemon for you)
  - Use AWS SDK in code
  - Ensure Lambda Function has correct IAM Execution Role