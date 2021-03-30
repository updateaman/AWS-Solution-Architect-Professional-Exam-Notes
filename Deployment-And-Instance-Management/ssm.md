# AWS Systems Manager Features

- Resource Groups
- Insights:
  - Insights Dashboard
  - Inventory: discover and audit the software installed
  - Compliance
- Parameter Store
- Action:
  - Automation (shutdown EC2, create AMIs)
  - Run Command
  - Session Manager
  - Patch Manager
  - Maintenance Windows
  - State Manager: define and maintaining configuration of OS and applications

# How SSM Works

- We need to install the SSM agent onto the systems we control
- Installed by default on Amazon Linux AMI & some Ubuntu AMI
- If an instance can't be controlled with SSM, it's probably an issue with the SSM agent
- Make sure the EC2 instances have a proper IAM role to allow SSM actions

# Run Command

- Execute a document (=script) or just run a command
- Run command across multiple instances (using resource groups)
- Rate Control/Error Control
- Integrated with IAM & CloudTrail
- No need for SSH
- Results in the console

# Predefined Patch Baselines

- Defines which patches should or shouldn't be installed on your instance

Linux:
  - AWS-AmazonLinux2DefaultPatchBaseline
  - AWS-CentOSDefaultPatchBaseline

Windows: (patches are auto-approved 7 days after the update)
  - AWS-DefaultPatchBaseline: install OS patch CriticalUpdates & SecurityUpdates
  - AWS-WindowsDefaultPatchBaseline-OS: same as "AWS-DefaultPatchBaseline"
  - AWS-WindowsPredefinedPatchBaseline-OS-Applications: also updates Microsoft applications

Can define your own custom patch baselines as well (OS, classification, severity)

# Steps

- Define a patch baseline to use (or multiple if you have multiple environments)
- Define patch groups: defined based on tags, example different environments (dev, test, prod) - use tag Patch Group
- Define Maintenance Windows (schedule, duration, registered targets/patch groups and registered tasks)
- Add the AWS-RunPatchBaseline Run Command as part of the registered tasks of the Maintenance Window (works cross platform Linux & Windows)
- Define Rate Control (concurrency & error threshold) for the task
- Monitor Patch Compliance using SSM Inventory

# AWS Parameter Store

- Secure storage for configuration and secrets
- Optional Seamless Encryption using KMS
- Serverless, scalable, durable, easy SDK, free
- Version tracking of configurations/secrets
- Configuration management using path & IAM
- Notifications with CloudWatch Events
- Integration with CloudFormation
- Can retrieve secrets from Secret Manager using the SSM Parameter Store API

