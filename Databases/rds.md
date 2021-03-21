# RDS

- Engines: PostgreSQL, MySQL, MariaDB, Oracle, Microsoft SQL Server
- Managed DB: provisioning, backups, patching, monitoring
- Launched within a VPC, usually in private subnet, control network access using security groups (important when using Lambda)
- Storage by EBS (gp2 or io1), can increase volume size with auto-scaling
- Backups: automated with point-in-time recover. Backups expire
- Snapshots: manual, can make copies of snapshots cross region
- RDS Events: get notified via SNS for events (operations, outages...)


# Multi AZ & Read Replicas

- Multi-AZ: Standby instance for failover in case of outage
- Read Replicas: Increase read throughput. Eventual consistency. Can be cross-region

# Security

- KMS encryption at rest for underlying EBS volumes/snapshots
- Transparent Data Encryption (TDE) for Oracle and SQL Server
- SSL encryption to RDS is possible for all DB (in-flight)
- IAM authentication for MySQL and PostgreSQL
- Authorization still happens within RDS (not in IAM)
- Can copy an un-encrypted RDS snapshot into an encrypted one
- CloudTrail cannot be used to track queries made within RDS

