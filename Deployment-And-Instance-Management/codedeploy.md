# AWS CodeDeploy

- We want to deploy our application automatically to many EC2 instances
- These instances are not managed by Elastic Beanstalk
- There are several ways to handle deployments using open source tools (Ansible, Terraform, Chef, Puppet, etc)
- We can use the managed service AWS CodeDeploy
- CodeDeploy can deploy to: EC2, ASG, ECS & Lambda

# CodeDeploy to EC2

- Define how to deploy the application using appspec.yml + deployment strategy
- Will do in-place update to your fleet of EC2 instances
- Can use hooks to verify the deployment after each deployment phase

# CodeDeploy to ASG

- In place updates:
  - Updates current existing EC2 instances
  - Instances newly created by an ASG will also get automated deployments
- Blue/green deployment:
  - A new auto-scaling group is created (settings are copied)
  - Choose how long to keep the old instances
  - Must be using an ELB

# CodeDeploy to AWS Lambda

- Traffic Shifting feature
- Pre and Post traffic hooks features to validate deployment (before the traffic shift starts and after it ends)
- Easy & automated rollback using CloudWatch Alarms
- SAM framework natively uses CodeDeploy

# CodeDeploy to ECS

- Support for Blue/Green deployments for Amazon ECS and AWS Fargate
- Setup is done within the ECS service definition
- A new task set is created and the traffic is re-routed to the new task test
- Then if everything is stable for X minutes, the old task set is terminated (so you have time to notice issues)