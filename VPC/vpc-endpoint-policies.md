# VPC Endpoint Policies

- Endpoint Policies are JSON documents to control access to services
- Does not override or replace IAM user policies or service-specific policies (such as S3 bucket policies)
- Note: the IAM user can still use other SQS API from outside the VPC Endpoint
- You could add an SQS queue policy to deny any action not done through the VPC endpoint