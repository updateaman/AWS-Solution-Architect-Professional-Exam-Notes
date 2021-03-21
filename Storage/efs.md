# EFS

- Use cases: content management, web serving, data sharing, Wordpress
- Compatible with Linux based AMI (not Windows), POSIX-compliant
- Uses NFSv4.1 protocol
- Uses security group to control access to EFS
- Encrypting at rest using KMS
- Can only attach to one VPC, create one ENI (mount target) per AZ

# Performance & Storage Classes

- EFS Scale
  - 1000s of concurrent NFS clients, 10 GB+ /s throughput
  - Grow to Petabyte-scale network file system
- Performance mode (set at EFS creation time)
  - General purpose (default): latency-sensitive use cases (web server, CMS etc)
  - Max I/O - higher latency, higher throughput, highly parallel (big data, media processing)
- Throughput Mode
  - Bursting Mode: common for file systems (intensive work, then almost nothing), linked to FS size
  - Provisioned IO Mode: high throughput to storage ratio (if burst is not enough) - expensive
- Storage Tiers (lifecycle management feature - move file after N days)
  - Standard: for frequently accessed file
  - Infrequent access: higher cost to retrieve the file, lower price to store the file 