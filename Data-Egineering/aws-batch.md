# AWS Batch

- Run batch jobs as Docker images
- Dynamic provisioning of the instances (EC2 & Spot Instances) - in VPC
- Optimal quantity and type based on volume and requirements
- No need to manage clusters, fully serverless
- You just pay for the underlying EC2 instances
- Example: batch process of images, running thousands of concurrent jobs
- Schedule Batch Jobs using CloudWatch Events
- Orchestrate Batch Jobs using AWS Step Functions

# Batch vs Lambda

Lambda:
- Time limit
- Limited runtimes
- Limited temporary disk space
- Serverless

Batch:
- No time limit
- Any runtime as long as it's packaged as a Docker image
- Rely on EBS/instance store for disk space
- Relies on EC2 (can be managed by AWS)

# AWS Batch - Compute Environments

Managed Compute Environment:
- AWS Batch manages the capacity and instance types within the environment
- You can choose On-Demand or Spot Instances
- You can set a maximum price for Spot Instances
- Launched within you own VPC
  - If you launch within your own private subnet, make sure it has access to the ECS service
  - Either using a NAT gateway/instance or using VPC Endpoints for ECS

Un-managed Compute Environment:
- You control and manage instance configuration, provisioning and scaling

# AWS Batch - Multi Node Mode

- Multi Node: large scale, good for HPC (high performance computing)
  - Leverages multiple EC2/ECS instances at the same time
  - Good for tightly coupled workloads
  - Represents a single job and specified how many nodes to create for the job
  - 1 main node and many child nodes
  - Does not work with Spot Instances
  - Works better if your EC2 launch mode is a placement group "cluster"