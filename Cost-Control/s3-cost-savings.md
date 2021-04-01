# S3 Storage Classes

- Amazon S3 Standard - General Purpose
- Amazon S3 Standard - Infrequent Access (IA)
- Amazon S3 One Zone-Infrequent Access
- Amazon S3 Intelligent Tiering
- Amazon Glacier
- Amazon Glacier Deep Archive

# Other Cost Savings

- S3 Select & Glacier Select: save in network and CPU cost
- S3 Lifecycle Rules: transition objects between tiers
- Compress objects to save space
- S3 Requester Pays:
  - In general, bucket owners pay for all Amazon S3 storage and data transfer costs associated with their bucket
  - With Requester Pays buckets, the requester instead of the bucket owner pays the cost of request and the data download from the bucket
  - The bucket owner always pays the cost of storing data
  - Helpful when you want to share large datasets with other accounts
  - If an IAM role is assumed the owner account of that role pays for the request