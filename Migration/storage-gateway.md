# AWS Storage Gateway

- Bridge between on-premise data and cloud data in S3
- Use cases: disaster recovery, backup & restore, tiered storage
- 3 types of Storage Gateway:
  - File Gateway
  - Volume Gateway
  - Tape Gateway

Exam Tip: You need to know the differences between all 3

# File Gateway
- File Gateway appliance is a virtual machine to bridge between your NFS and S3
- Metadata and directory structure are preserved
- Configured S3 buckets are accessible using the NFS and SMB protocol
- Each File Gateway should have an IAM role to access S3
- Most recently used data is cached in the file gateway
- Can be mounted on many servers

# File Architectures:

Amazon S3 Object Versioning
- Ability to store multiple object versions as they are modified
- Helpful to restore a file to a previous version
- Could restore an entire file system to a previous version
- Must use the "RefreshCache" API on the Gateway to be notified of restore

Amazon S3 Object Lock
- Enables to have the File Gateway for Write Once Read Many (WORM) data
- If there are file modifications or renames in the file share clients, the file gateway creates a new version of the object without affecting the prior versions and the original locked version will remain unchanged


# Volume Gateway

- Block storage using iSCSI protocol backed by S3
- Cached volumes: low latency access to most recent data, full data on S3
- Stored volumes: entire dataset is on premise, scheduled backups to S3
- Stored volumes: entire dataset is on premise, scheduled backups to S3
- Can create EBS snapshots from the volumes and restore as EBS
- Up to 32 volumes per gateway
  - Each volume up to 32TB in a cached mode (1PB per Gateway)
  - Each volume up to 16TB in stored mode (512TB per Gateway)

# Tape Gateway

- Some companies have backup processes using physical tapes
- With Tape Gateway, companies use the same processes but in the cloud
- Virtual Tape Library (VTL) backed by Amazon S3 and Glacier
- Back up data using existing tape-based processes (and iSCSI interface)
- Works with leading backup software vendors
- You can't access single file within tapes. You need to restore the tape entirely
