# DMS - Database Migration Service

- Quickly and securely migrate databases to AWS, resilient, self healing
- The source database remains available during the migration
- Supports:
  - Homogenous migrations: ex Oracle to Oracle
  - Heterogeneous migrations: ex Microsoft SQL Server to Aurora
- Continuous Data Replication using CDC
- You must create an EC2 instance to perform the replication tasks

# DMS Sources and Targets

Sources:
- On-Premise and EC2 instance databases: Oracle, MS SQL  Server, MySQL, MariaDB, PostgreSQL, MongoDB, SAP, DB2
- Azure: Azure SQL Database
- Amazon RDS: all including Aurora
- Amazon S3

Targets:
- On-Premise and EC2 instance databases: Oracle, MS SQL  Server, MySQL, MariaDB, PostgreSQL, SAP
- Amazon RDS
- Amazon Redshift
- Amazon DynamoDB
- Amazon S3
- ElasticSearch Service
- Kinesis Data Streams
- DocumentDB

# AWS Schema Conversion Tool (SCT)

- Convert your Database's Schema from one engine to another
- Example OLTP: (SQL Server or Oracle) to MySQL, PostgreSQL, Aurora
- Example OLAP: (Teradata or Oracle) to Amazon Redshift
- You do not need to use SCT if you are migrating the same DB engine
  - Ex: On-Premise PostgreSQL => RDS PostgreSQL
  - The DB engine is still PostgreSQL (RDS is the platform)

# DMS - Good things to know

- Works over VPC peering, VPN (site to site, software), Direct Connect
- Support Full Load, Full Load + CDC, or CDC only
- Oracle:
  - Source: Supports TDE for the source using "Binary Reader"
  - Target: Supports BLOBs in tables that have primary key and TDE
- ElasticSearch:
  - Source: does not exist
  - Target: possible to migrate DMS from a relational database
  - Therefore DMS cannot be used to replicate ElasticSearch data

# Snowball + Database Migration Service (DMS)

- Larger data migrations can include many terabytes of information
- Can be limited due to network bandwidth or size of data
- AWS DMS can use Snowball Edge & Amazon S3 to speed up migration
- Following stages:
  - You use the AWS Schema Conversion Tool (AWS SCT) to extract the data locally and move it to an Edge device
  - You ship the Edge device or devices back to AWS
  - After AWS receives your shipment, the Edge device automatically loads its data into an Amazon S3 bucket
  - AWS DMS takes the files and migrates the data to the target data store. If you are using change data capture (CDC), those updates are written to the Amazon S3 bucket and then applied to the target data store