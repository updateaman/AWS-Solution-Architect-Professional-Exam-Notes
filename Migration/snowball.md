# Snowball

- Physical data transport solution that helps moving TBs or PBs of data in or out of AWS
- Alternative to moving data over the network (and paying network fees)
- Secure, tamper resistant, uses KMS 256 bit encryption
- Tracking using SNS and text messages, E-ink shipping label
- Snowball size: 50TB and 80TB
- Use cases: large data cloud migrations, DC decommission, disaster recovery
- If it takes more than a week to transfer over the network, use Snowball devices

# Snowball Process

- Request snowball devices from the AWS console for delivery
- Install the snowball client on your servers
- Connect the snowball to your servers and copy files using the client
- Ship back the device when you're done (goes to the right AWS facility)
- Data will be loaded into an S3 bucket
- Snowball is completely wiped
- Tracking is done using SNS, text messages and the AWS console

# Snowball Edge

- Snowball Edges add computational capability to the device
- 100 TB capacity with either:
  - Storage optimized - 24 vCPU
  - Compute optimized - 52 vCPU & optional GPU
- Supports a custom EC2 AMI so you can perform processing on the go
- Supports custom Lambda functions
- Very useful to pre-process the data while moving
- Use case: data migration, image collation, IoT capture, machine learning

# AWS Snowmobile

- Transfer exabytes of data (1 EB= 1000PB = 1,000,000TBs)
- Each Snowmobile has 100PB of capacity (use multiple in parallel)
- Better than Snowball if you transfer more than 10PB