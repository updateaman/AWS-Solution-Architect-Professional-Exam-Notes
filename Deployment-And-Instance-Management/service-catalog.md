# AWS Service Catalog

- Users that are new to AWS have too many options and may create stack that are not compliant/in line with the rest of the organization
- Some users just want a quick self-service portal to launch a set of authorized products pre-defined by admins
- Includes: virtual machines, databases, storage options, etc
- Enter AWS Service Catalog!

# AWS Service Catalog

- Create and manage catalogs of IT services that are approved on AWS
- The "products" are CloudFormation templates
- Ex: Virtual machine images, Servers, Software, Databases, Regions, IP address ranges
- CloudFormation helps ensure consistency and standardization by Admins
- They are assigned to Portfolios (teams)
- Teams are presented a self-service portal where they can launch the products
- All the deployed products are centrally managed deployed services
- Helps with governance, compliance and consistency
- Can give user access to launching products without requiring deep AWS knowledge
- Integrations with "self-service portals" such as ServiceNow