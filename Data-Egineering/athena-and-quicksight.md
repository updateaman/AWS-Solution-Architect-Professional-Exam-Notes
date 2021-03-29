# Athena & Quicksight

Athena:
- Serverless SQL queries on top of your data in S3, pay per query, output to S3
- Supports CSV, JSON, Parquet, ORC
- Queries are logged in CloudTrail (which can be chained with CloudWatch logs)]
- Great for sporadic queries
- Ready-to-use queries for VPC Flow Logs, CloudTrail, ALB Access Logs, Cost and Usage reports (billing), etc

Quicksight:
- Business Intelligence tool for data visualization, creating dashboards
- Integrates with Athena, Redshift, EMR, RDS