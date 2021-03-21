# RDS - Security

- KMS encryption at rest for underlying EBS volumes/snapshots https://aws.amazon.com/blogs/database/securing-data-in-amazon-rds-using-aws-kms-encryption/
- Transparent Data Encryption (TDE) for [Oracle](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.Oracle.Options.AdvSecurity.html) and [SQL Server](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.SQLServer.Options.TDE.html)
- [SSL encryption to RDS](https://aws.amazon.com/rds/features/security/#Encryption_of_Data_in_Transit) is possible for all DB(in flight)
- [IAM authentication](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.IAMDBAuth.html) for MySQL and PostgreSQL
- Authorizatioin still happens within RDS (not in IAM)
- Can copy an un-encrypted RDS snapshot into an encrypted one
- ClourdTrail cannot be used to track queries made within RDS