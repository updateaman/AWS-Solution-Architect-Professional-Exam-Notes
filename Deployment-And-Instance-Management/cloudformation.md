# AWS CloudFormation

- Infrastructure as code (IaC) in AWS
- Portability of stacks across multiple accounts and regions
- Backbone of the Elastic Beanstalk service
- Backbone of the Service Catalog service
- Backbone of the SAM (Serverless Application Model) framework

# CloudFormation & ASG

- CloudFormation manages the ASG, not the underlying EC2
- You can define "success conditions" for the launch of your EC2 instances using a CreationPolicy
- You can define "update strategies" for the update of your EC2 instances using an UpdatePolicy
- To update the underlying EC2 in an ASG, you have to create a new launch configuration & use an UpdatePolicy

# Retaining Data on Deletes

You can put a DeletionPolicy on any resource to control what happens when the CloudFormation template is deleted

- DeletionPolicy=Retain
  - Specify on resources to preserve/backup in case of CloudFormation deletes
  - To keep a resource, specify Retain (works for any resource/nested stack)
- DeletionPolicy=Snapshot
  - EBS Volume, ElastiCache Cluster, ElastiCache ReplicationGroup
  - RDS DBInstance, RDS DBCluster, Redshift Cluster
- DeletionPolicy=Delete (default behavior)
  - Note: for AWS:RDS:DBCluster resources, the default policy is Snapshot
  - Note: to delete ans S3 bucket, you need to first empty the bucket of its content

# CloudFormation and IAM

When deploying a CloudFormation stack

- It uses the permissions of our own IAM principal
- OR assign an IAM role to the stack that can perform the actions

If you create IAM resources, you need to explicitly provide a "capability" to CloudFormation CAPABILITY_IAM and CAPABILITY_NAMED_IAM

# CloudFormation Custom Resources (Lambda)

- You can define a Custom Resource in CloudFormation to address any of these use cases:
  - An AWS resource is not yet supported (new service for example)
  - An On-Premise resource
  - Emptying an S3 bucket before being deleted
  - Fetch an AMI id
  - Anything you want!

# CloudFormation - Cross vs Nested Stacks

Cross Stacks
- Helpful when stacks have different life-cycles
- Use Outputs Export and Fn:ImportValue
- When you need to pass export values to many stacks (VPC Id, etc)

Nested Stacks
- Helpful when components must be re-used
- Ex:re-use how to properly configure an Application Load Balancer
- The nested stack only is important to the higher level stack (it's not shared)

# CloudFormation - Other Concepts

CloudFormer
- Create an AWS CloudFormation template from existing AWS resources

ChangeSets
- Generate & Previewing the CloudFormation changes before they get applied
  
StackSets
- Deploy a CloudFormation stack across multiple accounts and regions

Stack Policies
- Prevent accidental updates/deletes to stack resources

