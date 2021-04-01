# Trusted Advisor

- No need to install anything - high level AWS account assessment
- Analyze your AWS accounts and provides recommendation:
  - Cost Optimization & Recommendations
  - Performance
  - Security
  - Fault Tolerance
  - Service Limits
- Core Checks and recommendations - all customers
- Can enable weekly email notification from the console
- Full Trusted Advisor - Available for Business & Enterprise support plans
  - Ability to set CloudWatch alarms when reaching limits
  - Programmatic Access using AWS Support API

# Good to know

- Can check if an S3 bucket is made public
  - But cannot check for S3 objects that are public inside your bucket!
  - Use CloudWatch Events/S3 Events/AWS Config instead
- Service Limits
  - Limits can only be monitored in Trusted Advisor (cannot be changed) (Business Plan)
  - Cases have to be created manually in AWS Support Centre to increase limits
  - OR use the new AWS Service Quotas service (new service - has an API)