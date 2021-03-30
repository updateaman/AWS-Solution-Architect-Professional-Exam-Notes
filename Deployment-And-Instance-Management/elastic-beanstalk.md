# AWS Elastic Beanstalk Overview

- Elastic Beanstalk is a developer centric view of deploying an application on AWS
- It uses all the components we've seen before: EC2, Auto Scaling Group, Elastic Load Balancers, RDS etc
- But it's all in one view that's easy to make sense of!
- We still have full control over the configuration of each component
- Beanstalk is free but you pay for the underlying instances

# Supported Environments

Support for many platforms:
- Go
- Java SE 
- Java with Tomcat
- .NET on Windows Server with IIS
- Node.js
- PHP
- Python
- Ruby
- Packer Builder
- Single Container Docker
- Multi-container Docker
- Pre-configured Docker

If not supported you can write your custom platform (advanced)

Beanstalk is great to "Re-platform" your application from on-premise to the cloud

# Management

- Managed service
  - Instance configuration/OS is handled by Beanstalk
  - Deployment strategy is configurable but performed by Elastic Beanstalk
- Just the application code is the responsibility of the developer
- Three architecture models:
  - Single Instance deployment: good for dev
  - LB + ASG: great for production or pre-production web applications
  - ASG only: great for non-web apps in production (workers, etc)

# Web Server vs Worker Environment

- If your application performs tasks that long to complete, offload these tasks to a dedicated worker environment
- Decoupling your application into two tiers is common
- Example: processing a video, generating a zip file etc
- You can define periodic tasks in a file cron.yaml

# Deployment: Blue/Green

- Not a "direct feature" of Elastic Beanstalk
- Zero downtime and release facility
- Create a new "stage" environment and deploy v2 there
- The new environment (green) can be validated independently and roll back if issues
- Route53 can be setup using weighted policies to redirect a little bit of traffic to the stage environment
- Using Beanstalk "swap URLs" (DNS swap) when done with the environment test