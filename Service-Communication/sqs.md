# SQS

Serverless, managed queue, integrated with IAM

Can handle extreme scale, no provisioning required

Used to decouple services

Message size of max 256 KB (use a pointer to S3 for large messages)

Can be read from EC2 (optional ASG), Lambda

SQS could be used as a write buffer for DynamoDB

SQS FIFO:
- receive messages in order they were sent
- 300 messages/s without batching, 3000/s with batching

# Idempotency

Messages can be processed twice by consumer (in case of failures, timeouts, etc)

To hedge against that problem, implement idempotency at the consumer level

Means the same action done twice by the consumer won't duplicate the effect

# Event Source Mapping

Event Source Mapping will poll SQS (Long Polling)

Specify batch size (1-10 messages)

Recommended: Set the queue visibility timeout to 6x the timeout of your Lambda function

To use a DLQ
- set-up on the SQS queue, not Lambda (DLQ for Lambda is only for async invocations)
- Or use a Lambda destination for failures
