# Direct Connect

- Provides a dedicated private connection from a remote network to your VPC
- Dedicated connection must be setup between your DC and AWS Direct Connect Locations
- More expensive than running a VPN solution
- Private access to AWS services through VIF
- Bypass ISP, reduce network cost, increase bandwidth and stability
- Not redundant by default (must setup a failover DX or VPN)

# Direct Connect Virtual Interfaces (VIF)

- Public VIF: Connect to Public AWS Endpoints (S3 buckets, EC2 service, anything AWS)
- Private VIF: To connect to resources in your VPC (EC2 instances, ALB etc)
- Transit Virtual Interface: To connect to resources in a VPC using a Transit Gateway

VPC endpoints cannot be accessed through Private VIF (you don't need them)

# Connection Types

Dedicated Connections: 1 Gbps and 10 Gbps capacity
- Physical ethernet port dedicated to a customer
- Request made to AWS first, then completed by AWS Direct Connect Partners

Hosted Connections: 50Mbps, 500Mbps to 10 Gbps
- Connection requests are made via  AWS Direct Connect Partners
- Capacity can be added or removed on demand
- 1,2,5,10 Gbps available at select AWS Direct Connect Partners

Lead times are often longer than 1 month to establish a new connection

# Encryption

- Data in transit is not encrypted but is private
- AWS Direct Connect + VPN provides an IPsec-encrypted private connection
- Good for an extra level of security but slightly more complex to put in place

# Direct Connect Link Aggregation Groups (LAG)

- Get increased speed and failover by summing up  existing Direct Connect connections into a logical one
- Can aggregate up to 4 (active active mode)
- Can add connections over time to the LAG
- All connections in LAG must have the same bandwidth
- All connections in the LAG must terminate at the same AWS Direct Connect Endpoint
- Can set a minimum number of connections for the LAG to function

# Direct Connect Gateways

- If you want to setup a Direct Connect to one or more VPC in many different regions (same account, cross account) you must use a Direct Connect Gateway