# [Lambda - Synchronous Invocations](https://docs.aws.amazon.com/lambda/latest/dg/invocation-sync.html)

- Synchronous: CLI, SDK, API Gateway
  - Result is returned right away
  - Error handling must happen client side (retries, exponential backoff)

# [Lambda - Asynchronous Invocation](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html)

- S3, SNS, Cloudwatch Events (EventBridge)
- Lambda attempts to retry on errors (3 tries total)
- Make sure the processing is idempotent (in case of retries)
- Can define a DLQ (dead-letter queue) - SNS or SQS - for failed processing

# [Lambda - Event Source Mapping](https://docs.aws.amazon.com/lambda/latest/dg/invocation-eventsourcemapping.html)

- Kinesis Data Streams, SQS, SQS FIFO queue, DynamoDB Streams
- Common denominator: records need to be polled from the source
- All records are processed in order except for SQS standard
- If your function returns an error the entire batch is reprocessed until success
  - Kinesis, DynamoDB stream: stop shard processing
  - SQS FIFO: stop unless a SQS DLQ has been defined
  - Need to make sure your lambda function is idempotent

# [Lambda Destinations](https://aws.amazon.com/blogs/compute/introducing-aws-lambda-destinations/)

- Nov 2019: Can configure to send result to a destination
- Asynchronous invocations - can define destinations for successful and failed event:
  - Amazon SQS
  - Amazon SNS
  - AWS Lambda
  - Amazon EventBridge bus
- Note: AWS recommends you use destinations instead of DLQ now (but both can be used at the same time)
- Event source mapping: for discarded event batches
  - Amazon SQS
  - Amazon SNS
- Note: you can send events to a DLQ directly from SQS

# [AWS Lambda Versions](https://docs.aws.amazon.com/lambda/latest/dg/configuration-versions.html)

- When you work on a Lambda function, we work on $Latest
- When we're ready to publish a Lambda function, we create a version
- Versions are immutable
- Versions have increasing version numbers
- Versions get their own ARN (Amazon Resource Name)
- Version = code + configuration (nothing can be changed - immutable)
- Each version of lambda function can be accessed

# [AWS Lambda Aliases](https://docs.aws.amazon.com/lambda/latest/dg/configuration-aliases.html)

- Aliases are "pointers" to Lambda function versions
- We can define a "dev", "test", "prod" aliases and have them point at different lambda versions
- Aliases are mutable
- Aliases enable Blue/Green deployment by assigning weights to lambda functions
- Aliases enable stable configuration of our event triggers/destinations
- Aliases have their own ARNs

# [Lambda & CodeDeploy](https://aws.amazon.com/blogs/compute/implementing-safe-aws-lambda-deployments-with-aws-codedeploy/)
  
- CodeDeploy can help you automate traffic shift for Lambda aliases
- Feature is integrated within the SAM framework
- Linear: grow traffic every N minuted until 100%
  - Linear10PercentEvery3Minutes
  - Linear10PercentEvery10Minutes
- Canary: try X percent then 100%
  - Canary10Percent5Minutes
  - Canary10Percent30Minutes
- AllAtOnce: immediate
- Can create Pre & Post Traffic hooks to check health of the Lambda function