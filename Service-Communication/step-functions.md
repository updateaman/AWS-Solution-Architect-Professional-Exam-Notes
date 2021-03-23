# AWS Step Functions

Build serverless visual workflow to orchestrate your Lambda functions

Represent flow as a JSON state machine

Features: sequence, parallel, conditions, timeouts, error handling

Can also integrate with EC2, ECS, On premise servers, API Gateway

Maximum execution time of 1 year

Possibility to implement human approval feature

If you chain Lambda functions using Step Functions, be mindful of the added latency to pass calls

# Tasks

Lambda Tasks:
- Invoke a Lambda function

Activity Tasks:
- Activity worker (HTTP), EC2 Instances, mobile device, on premise DC
- They poll the Step functions service

Service Tasks:
- Connect to a supported AWS service
- Lambda function, ECS Task, Fargate, DynamoDB, Batch job, SNS topic, SQS queue

Wait Task:
- To wait for a duration or until a timestamp

Note: Step Functions does not integrate natively with AWS Mechanical Turk