# EC2

## EC2 Instance Types

R: applications that needs a lot of RAM - in-memory caches

C: applications that need good CPU - compute /databases

M: applications that are balanced - general/web app

I: applications that need good local I/O (instance storage) - databases

G: applications that need a GPU - video  rendering / machine learning

T2/T3: burstable instances (up to a capacity)

T2/T3 - unlimited: unlimited burst

[https://aws.amazon.com/ec2/instance-types/](https://aws.amazon.com/ec2/instance-types/)

## EC2 Placement Groups

- [Cluster](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html#placement-groups-cluster): low-latency group in a single Availability Zone - high performance computing (HPC)
    - Pros: Low latency 10 Gbps bandwith between instances
    - Cons: If the rack fails, all instances fail at the same time
    - Note: choose an instance type that has Enhanced Networking
    - Use cases: 
        - Big Data job that needs to complete fast
        - Application that need extremely low latency and high network throughput

- [Spread](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html#placement-groups-spread): spread instances on different hardware (max 7 instances per group per AZ) - critical applications
    - Pros:
        - Can span across Availability Zones (AZ)
        - Reduced risk is simultaneous failure
        - EC2 Instances are on different physical hardware
    - Cons:
        - Limited to 7 instances per AZ per placement group
    - Use cases:
        - Application that need maximum high availability
        - Critical applications where each instance must be isolated from failure from each other

- [Partition](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html#placement-groups-partition): spreads instances across many different partitions and ensures that each partition within a placement group has its own set of racks within an AZ. Scales to 100s of EC2 instances per group - Hadoop, Cassandra, Kafka
    - Up to 7 partitiions per AZ
    - Up to 100s of EC2 instances
    - The instances in a paritition do not share racks with the instances in the other partitions
    - A partition failure can affect many EC2 instances but won't affect other partitions
    - EC2 instances get access to the partition information as metadata
    - Use cases: HDFS, HBase, Cassandra, Kafka