# EC2 Instance Launch Types

- On Demand Instances: short workload, predictable pricing, reliable
- Spot Instances: short workloads, for cheap, can lose instances (not reliable)
- Reserved: (MINIMUM 1 year)
  - Reserved Instances: long workloads
  - Convertible Reserved Instances: long workloads with flexible instances
  - Scheduled Reserved Instances: example - every Thursday between 3 and 6 pm
- Dedicated Instances: no other customers will share your hardware
- Dedicated Hosts: book an entire physical server, control instance placement
  - Great for software licenses that operate at the core or socket level
  - Can define host affinity so that instance reboots are kept on the same host

# AWS Savings Plan

- New pricing model to get a discount based on long-term usage
- Commit to a certain type of usage: ex $10 per hour for 1 to 3 years
- Any usage beyond the savings plan is billed at the on-demand price
- EC2 Instance Savings plan (up to 72% - same discount as Standard RIs)
  - Select instance family (e.g. M5, C5) and locked to a specific region
  - Flexible across size (m5.large to m5.4xlarge), OS (Windows to Linux), tenancy (dedicated or default)
- Compute Savings plan (up to 66% - same discount as Convertible RIs)
  - Ability to move between instance family (move from C5 to M5), region (Ireland to US), compute type (EC2, Fargate, Lambda), OS & tenancy