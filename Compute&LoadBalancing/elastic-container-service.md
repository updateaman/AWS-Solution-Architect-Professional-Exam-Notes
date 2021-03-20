# [AWS ECS - Elastic Container Service](https://aws.amazon.com/ecs/)

- Container orchestration service
- Helps you run [Docker](https://www.docker.com/) containers on EC2 machines
- ECS is complicated and made of:
  - ECS Core: Running ECS on user-provisioned EC2 instances
  - [Fargate](https://aws.amazon.com/fargate): Running ECS tasks on AWS-provisioned compute (serverless)
  - [EKS](https://aws.amazon.com/eks): Running ECS on AWS-powered [Kubernetes](https://kubernetes.io/) (running on EC2)
  - [ECR](https://aws.amazon.com/ecr/): Docker Container Registry hosted by AWS
- ECS & Docker are very popular for microservices

# AWS ECS - Concepts

- ECS cluster: set of EC2 instances
- ECS service: application definitions running on ECS cluster
- ECS tasks + definition: containers running to create the application
- ECS IAM roles: roles assigned to tasks to interact with AWS

# AWS ECS - ALB integration

- Application Load Balancer (ALB) has a direct integration feature with ECS called "port mapping"
- This allows you to run multiple instances of the same application on the same EC2 machine
- Use cases:
  - Increased resiliency even if running on one EC2 instance
  - Ability to perform rolling upgrades without impacting application uptime