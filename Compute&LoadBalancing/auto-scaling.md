# Auto Scaling

- [Simple / Step Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scaling-simple-step.html): increase or decrease instances based on two CW alarms
- [Target Tracking](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scaling-target-tracking.html): select a metric and a target value, ASG will smartly adjust
  - Keep average CPU at 40%
  - Keep request count per target at 1000
- To scale based on RAM, you must use a [Custom CloudWatch Metric](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/publishingMetrics.html)

# Good to know

- [Spot Fleet](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-fleet.html) support (mix of Spot and On-Demand instances)

- To upgrade an AMI, must update the [Launch Configuration](https://docs.aws.amazon.com/autoscaling/ec2/userguide/LaunchConfiguration.html) (legacy) or [Launch Templates](https://docs.aws.amazon.com/autoscaling/ec2/userguide/LaunchTemplates.html)
  - You must terminate instances manually
  - CloudFormation can help with that step

- [Scheduled scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/schedule_time.html) actions:
    - Modify the ASG settings (min/max/desired) at pre-defined time
    - Helpful when patterns are known in advance - out of hours jobs

- [Lifecycle Hooks](https://docs.aws.amazon.com/autoscaling/ec2/userguide/lifecycle-hooks.html):
  - Perform actions before an instance is in service, or before it is terminated
  - Examples: cleanup, log extraction, special health checks

# [Scaling processes](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-suspend-resume-processes.html#process-types)

- Launch: Add a new EC2 instance to the group, increases the capacity
- Terminate: Removes an EC2 instance from the group, decreases the capacity
- HealthCheck: Checks the health of the instances
- ReplaceUnhealthy: Terminate unhealthy instances and re-create them
- AZRebalance: Balance the number of EC2 instances across AZ
- AlarmNotification: Accept notification from CloudWatch
- ScheduledActions: Performs scheduled actions that you create
- AddToLoadBalancer: Adds instances to the load balancer or target group

- We can suspend these processes

# Health Checks

- Health checks available:
  - [EC2 Status Checks](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-system-instance-status-check.html)
  - [ELB Health Checks (HTTP)](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-add-elb-healthcheck.html)