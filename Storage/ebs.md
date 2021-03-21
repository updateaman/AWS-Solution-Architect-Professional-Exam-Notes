# EBS

- Network drive you attach to one instance only
- Linked to a specific availability zone (transfer: snapshot => restore)
- Volumes can be resized
- Make sure you choose an instance type that is EBS optimized to enjoy maximum throughput

# Volume Types

- gp2: General Purpose Volumes (cheap)
  - 3 IOPS/GiB, minimum 100 IOPS, burst to 3000 IOPS, max 16000 IOPS
  - 1 GiB - 16 TiB, +1 TB = +3000 IOPS
- io1: Provisioned IOPS (expensive)
  - Min 100 IOPS, Max 64000 IOPS (Nitro) or 320000 (other)
  - 4 GiB - 16 TiB. Size of volume and IOPS are independent
- st1: Throughput Optimized HDD
  - 500 GiB - 16 TiB, 500 MiB/s throughput
- sc1: Cold HDD, Infrequently accessed data
  - 250 GiB - 16 TiB, 250 MiB/s throughput

# RAID Configurations

- RAID 0 (add)
  - Used to increase throughput of the system
- RAID 1 (mirror)
  - Used to protect data in case of disaster recovery

# EBS Snapshots

- Incremental - only backup changed blocks
- EBS backups use IO and you shouldn't run them while your application is handling a lot of traffic
- Snapshots will be stored in S3 (but you can't directly see them)
- Not necessary to detach volume to do snapshot, but recommended
- Can copy snapshots across region (for DR)
- Can make image (AMI) from snapshot
- EBS volumes restored by snapshots need to be pre-warmed (using fio or dd command to read the entire volume)
- Snapshots can be automated using Amazon Data Lifecycle Manager

# Local EC2 Instance Store

- Physical disk attached to the physical server where your EC2 is
- Very High IOPS (because physical)
- Disks up to 7.5 TiB (can change over time), stripped to reach 30 TiB (can change over time)
- Block storage (just like EBS)
- Cannot be increased in size
- Risk of data loss if hardware failure

# EBS vs Instance Store

- Some instance do not come with Root EBS volumes
- Instead, they come with "Instance Store" (= ephemeral storage)
- Instance store is physically attached to the machine (EBS is a network drive)
- Pros:
  - Better I/O performance (EBS gp2 has max IOPS of 16000, io1 of 64000)
  - Good for buffer/cache/scratch data/temporary content
  - Data survives reboots
- Cons:
  - On stop or termination, the instance store is lost
  - You can't resize the instance store
  - Backups must be operated by the user