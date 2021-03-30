# AWS SAM

- SAM = Serverless Application Model
- Framework for developing and deploying serverless applications
- All the configuration is YAML code
  - Lambda Functions (AWS:Serverless:Function)
  - DynamoDB tables (AWS:Serverless:SimpleTable)
  - API Gateway (AWS:Serverless:API)
  - Cognito User Pools


SAM can help you run Lambda, API Gateway, DynamoDB locally

SAM can use CodeDeploy to deploy Lambda functions (traffic shifting)

Leverages CloudFormation in the backend

# CI/CD SAM

When deploying lambda function it internally uses CodeDeploy to deploy the Lambda Function and applies traffic shifting with alias