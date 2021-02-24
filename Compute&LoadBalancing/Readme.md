# Solution Architecture on AWS

- DNS Layer - [Route 53](https://aws.amazon.com/route53/)

- CDN Layer - [CloudFront](https://aws.amazon.com/cloudfront/)

- Storage - [S3](https://aws.amazon.com/s3/), [Glacier](https://aws.amazon.com/glacier/), [EBS](https://aws.amazon.com/ebs/), [EFS](https://aws.amazon.com/efs/), [Instance Store](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html)

- Web Layer - [CLB](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/introduction.html), [ALB](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html), [NLB](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html), [API Gateway](https://aws.amazon.com/api-gateway/), [Elastic IP](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)

- Compute Layer - [EC2](https://aws.amazon.com/ec2/), [ASG](https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html), [Lambda](https://aws.amazon.com/lambda/), [ECS](https://aws.amazon.com/ecs/), [Fargate](https://aws.amazon.com/fargate/), [Batch](https://aws.amazon.com/batch/), [EMR](https://aws.amazon.com/emr/)

- Database Layer - [RDS](https://aws.amazon.com/rds/), [Aurora](https://aws.amazon.com/rds/aurora/), [DynamoDB](https://aws.amazon.com/dynamodb/), [ElasticSearch](https://aws.amazon.com/elasticsearch-service/), [S3](https://aws.amazon.com/s3/), [Redshift](https://aws.amazon.com/redshift/)

- Caching Layer - [ElastiCache](https://aws.amazon.com/elasticache/), [DAX](https://aws.amazon.com/dynamodb/dax/), [DynamoDB](https://aws.amazon.com/dynamodb/), [RDS](https://aws.amazon.com/rds/)

- Messaging Layer - [SQS](https://aws.amazon.com/sqs/), [SNS](https://aws.amazon.com/sns/), [Kinesis](https://aws.amazon.com/kinesis/), [Amazon MQ](https://aws.amazon.com/amazon-mq/), [Step Functions](https://aws.amazon.com/step-functions/)