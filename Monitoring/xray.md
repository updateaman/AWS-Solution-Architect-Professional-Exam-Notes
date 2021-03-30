# X-Ray

- Tracing requests across your microservices (distributed systems)
- Integrations with:
  - EC2 - install the X-Ray agent
  - ECS - install the X-Ray agent or Docker container
  - Lambda
  - Beanstalk - agent is automatically installed
  - API Gateway - helpful to debug errors (such as 504)

The X-Ray agent or services need IAM permissions to X-Ray