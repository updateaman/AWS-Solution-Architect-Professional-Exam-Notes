# VPC Endpoints

- Endpoints allow you to connect to AWS Services using a private network instead of the public www network
- They scale horizontally and are redundant
- No more IGW, NAT, etc to access AWS Services
- VPC Endpoint Gateway (S3 & DynamoDB)
- VPC Endpoint Interface (the rest)
- In case of issues:
  - Check DNS Setting Resolution in your VPC
  - Check Route Tables

# VPC Endpoint Gateway

- Only works for S3 and DynamoDB, must create one gateway per VPC
- Must update route table entries
- Gateway is identified at the VPC level
- DNS resolution must be enabled in the VPC
- The same public hostname for S3 can be used
- Gateway endpoint cannot be extended out of a VPC (VPN, DX, TGW, peering)

# VPC Endpoint Interface

- Provision and ENI that will have a private endpoint interface hostname
- Leverage Security Groups for security
- Private DNS (setting when you create the endpoint)
  - The public hostname of a service will resolve the private Endpoint Interface hostname
  - VPC Setting: "Enable DNS hostnames" and "Enable DNS Support" must be true
- Interface can be accessed from Direct Connect and Site-to-Site VPN

