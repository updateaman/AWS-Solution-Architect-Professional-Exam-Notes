# API Gateway

- Helps expose Lambda, HTTP & AWS services as an API
- API versioning, authorization, traffic management (API keys, throttles), huge scale, serverless, req/resp transformations, OpenAPI spec, CORS

- Limits to know:
  - 29 seconds timeout
  - 10 MB max payload size

# Deployment Stages

- API changes are deployed to "Stages" (as many as you want)
- Use the naming you like for stages (dev, test, prod)
- Stages can be rolled back as a history of deployment is kept

# Integrations

- Http
  - Expose HTTP endpoints in the backend
  - Example: internal http api on premise, application load balancer
  - Why? add rate limiting, caching, user authentication, api keys, etc

- Lambda Function
  - Invoke Lambda function
  - Easy way to expose REST API backend by AWS Lambda

- AWS Service
  - Expose any AWS API through the API Gateway
  - Example: start an AWS Step Function workflow, post a message to SQS
  - Why? Add authentication, deploy publicly, rate control

# Endpoint Types

- Edge-Optimized (default): For global clients
  - Requests are route through the CloudFront Edge locations (improves latency)
  - The API Gateway still lives in only one region
- Regional:
  - For clients within the same region
  - Could manually combine with CloudFront (more control over the caching strategies and the distribution)
- Private:
  - Can only be accessed from your VPC using an interface VPC endpoint (ENI)
  - Use a resource policy to define access

# Caching API responses

- Caching reduces the number of calls made to the backend
- Default TTL (time to live) is 300 seconds (min: 0s, max:3600s)
- Caches are defined per stage
- Possible to override cache settings per method
- Client can invalidate the cache with header: Cache-Control:max-age=0 (with proper IAM authorization)
- Able to flush the entire cache (invalidate it) immediately
- Cache encryption option
- Cache capacity between 0.5GB to 237GB

# Errors

- 4xx means client errors
  - 400: Bad request
  - 403: Access denied, WAF filtered
  - 429: Quota exceeded, Throttle

- 5xx means server errors
  - 502: Bad gateway exception, usually for an incompatible output returned from a Lambda proxy integration backend and occasionally for out-of-order invocations due to heavy loads
  - 503: Service unavailable exception
  - 504: Integration failure - ex endpoint request timeout exception (API Gateway requests time out after 29 second maximum)

# Security

- Load SSL certificates and use Route53 to define a CNAME
- Resource Policy (~S3 bucket policy):
  - control who can access the API
  - Users from AWS accounts, IP or CIDR blocks, VPC or VPC endpoints
- IAM Execution Roles for API Gateway at the API level
  - To invoke Lambda Function, an AWS service
- CORS (Cross-origin resource sharing):
  - Browser based security
  - Control which domains can call your API

# Authentication

- IAM based access
  - Good for providing access within your own infrastructure
  - Pass IAM credentials in headers through Sig V4

- Lambda Authorizer (formerly Custom Authorizer)
  - Use Lambda to verify a custom OAuth/SAML/3rd party authentication

- Cognito User Pools
  - Client authenticates with Cognito
  - Client passes the token to API Gateway
  - API Gateway knows out-of-box how to verify the token

# Logging, Monitoring, Tracing

- CloudWatch Logs:
  - Enable CloudWatch logging at the Stage level (with Log Level - ERROR, INFO)
  - Can log full requests/response data
  - Can send API Gateway Access Logs (customizable)
  - Can send logs directly into Kinesis Data Firehose (as an alternative to CW logs)
- CloudWatch Metrics:
  - Metrics are by stage, possibility to enable detailed metrics
  - IntegrationLatency, Latency, CacheHitCount, CacheMissCount
- X-Ray:
  - Enable tracing to get extra information about requests in API Gateway
  - X-Ray API Gateway + AWS Lambda give your the full picture