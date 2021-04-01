# Cloud Migration: The 6R

Re-hosting: "lift and shift"
- Simple migrations by re-hosting on AWS (applications, database, data)
- No cloud optimizations being done, application is migrated as is
- Could save as much as 30% on cost
- Example: Migrate using AWS VM Import/Export, AWS Server Migration Service


Re-platforming:
- Example: migrate your database to RDS
- Example: migrate your application to Elastic Beanstalk (Java with Tomcat)
- Not changing the core architecture, but leverage some cloud optimizations


Repurchase: "drop and shop"
- Moving to a different product while moving to the cloud
- Often you move to SaaS platform
- Expensive in the short term, but quick to deploy
- Example: CRM to Salesforce.com, HR to Workday, CMS to Drupal


Refactoring/Re-architecting:
- Re-imagining how the application is architected using Cloud Native features
- Driven by the need of the business to add features, scale, performance
- Example: move an application to Serverless architectures, use AWS S3


Retire
- Turn off things you don't need (maybe as a result of Re-architecting)
- Helps with reducing the surface areas for attacks (more security)
- Save cost, maybe up to 10% to 20%
- Focus your attention on resources that must be maintained


Retain
- Do nothing for now (for simplicity, cost reason, importance)
- It's still a decision to make in a Cloud Migration