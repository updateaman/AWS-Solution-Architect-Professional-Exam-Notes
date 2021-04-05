# VPC Basics

- CIDR: Block of IP addressed
  - Example: 192.168.0.0/26: 192.168.0.0 -192.168.0.63 (64 IP)
  - Used for security groups, route tables, VPC, subnets
- Private IP
  - 10.0.0.0 - 10.255.255.255 (10.0.0.0/8) <= in big networks
  - 172.16.0.0 - 172.31.255.255 (172.16.0.0/12) <= default AWS one
  - 192.168.0.0 - 192.168.255.255 (192.168.0.0/16) <= example: home networks
- Public IP
  - All the rest

VPC
- A VPC must have a defined list of CIDR blocks, that cannot be changed
- Each CIDR within VPC: min size is /28, max size is /16 (65536 IP addresses)
- VPC is private, so only Private CIDR ranges are allowed

Subnets
- Within a VPC, defined as a CIDR that is a subset of the VPC CIDR
- All instances within subnets get a private IP
- First 4 IP and last one in every subnet is reserved by AWS

Route Tables
- Used to control where the network traffic is directed to
- Can be associated with specific subnets
- The "most specific" routing rule is always followed (192.168.0.1/24 beats 0.0.0.0/0)

Internet Gateway (IGW)
- Help our VPC connect to the internet, HA, scales horizontally
- Acts as a NAT for instances that have a public IPv4 or public IPv6

Public Subnets
- Has a route table that sends 0.0.0.0/0 to an IGW
- Instances must have public IPv4 to talk to the internet

Private Subnets
- Access internet with a NAT Instance or NAT Gateway setup in a public subnet
- Must edit routes so that 0.0.0.0/0 routes traffic to the NAT

NAT Instance
- EC2 instance you deploy in a public subnet
- Edit the route in your private subnet to route 0.0.0.0/0 to your NAT instance
- Not resilient to failure, limited bandwidth based on instance type, cheap
- Must manage failover yourself

NAT Gateway
- Managed NAT solution, bandwidth scales automatically
- Resilient to failure within a single AZ
- Must deploy multiple NAT Gateways in multiple AZ for HA
- Has an Elastic IP, external services see the IP of the NAT Gateway as the source

Network ACL (NACL)
- Stateless firewall defined at the subnet level, applies to all instances within
- Support for allow and deny rules
- Stateless = return traffic must be explicitly allowed by rules
- Helpful to quickly and cheaply block specific IP addresses

Security Groups
- Applied at the instance level, only support for allow rules, no deny rules
- Stateful = return traffic is automatically allowed, regardless of rules
- Can reference other security groups in the same region (peered VPC, cross-account)

VPC Flow Logs
- Log internet traffic going through your VPC
- Can be defined at the VPC level, Subnet level or ENI-level
- Helpful to capture "denied internet traffic"
- Can be sent to CloudWatch Logs and Amazon S3

Bastion Hosts
- SSH into private EC2 instances through a public EC2 instance (bastion host)
- You must manage these instances yourself (failover, recovery)
- SSM Session Manager is a more secure way to remote control without SSH

IPv6
- All IPv6 addresses are public, total 3.4 x 10-38 addresses (vs 4.3 billion IPv4)
- Example CIDR: 2600:1f18:80c:a900::/56
- Addresses are "random" and can't be scanned online (because too many)

VPC support for IPv6
- Create an IPv6 CIDR for VPC & use an IGW (supports IPv6)
- Public subnet:
  - Create an instance with IPv6 support
  - Create a route table entry to ::/0 (IPv6 "all) to the IGW
- Private subnet (instances cannot be reached by IPv6 but can reach IPv6):
  - Create an Egress-Only Internet Gateway in the public subnet
  - Add a route table entry for the private subnet from ::/0 to the Egress-Only IGW