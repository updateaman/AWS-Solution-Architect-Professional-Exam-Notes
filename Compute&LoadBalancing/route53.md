# Records

- Route53 is a Managed DNS (Domain Name System)


- A: hostname to IPv4
- AAAA: hostname to IPv6
- CNAME: hostname to hostname
- Alias: hostname to AWS resource
  - Use for: CLB, ALB, NLB, CloudFront, S3 bucket, Elastic Beanstalk
  - Can be used for root apex record (mydomain.com)

# Simple Routing Policy

- Maps a hostname to a single resource
- You can't attach health checks to simple routing policy
- If multiple values are returned, a random one is chosen by the client

# Weighted Routing Policy

- Control the % of the requests that go to specific endpoint
- Helpful to test 1% of traffic on new app version for example
- Helpful to split traffic between two regions - Load Balancing
- Can be associated with Health Checks
- Note: The weights don't need to sum up to 100

# Latency Routing Policy

- Redirect to the server that has the least latency close to us
- Super helpful when latency of users is a priority
- Latency is evaluated in terms of users to designated AWS region
- Germany users may be directed to the US (if that's the lowest latency)
- Has failover capability if you enable health checks

# Geo Location Routing Policy

- Different from Latency based!
- This is routing based on user location
- Here we specify: traffic from the UK should go to this specific IP
- Should create a "default" policy (in case there's no match on location)

# MultiValue Routing Policy

- Use when routing traffic to multiple resources
- Want to associate a Route53 health checks with records
- Up to 8 healthy records are returned for each MultiValue query
- MultiValue is not a substitute for having ELB

# Good to know

- Private DNS:
  - Can use Route53 for internal private DNS
  - Must enable the VPC  settings enableDnsHostNames and enableDnsSupport
- DNSSEC (protect against Man In the Middle attack):
  - Amazon Route53 supports DNSSEC for domain registration
  - Route53 does not support DNSSEC for DNS service
  - To configure DNSSEC for a Route53 domain, use another DNS provider or custom DNS server on Amazon EC2 (Bind, dnsmasq, KnotDNS, PowerDNS)
- 3rd party registrar:
  - You can buy the domain out of AWS and use Route53 as your DNS provider
  - Update the NS records on the 3rd party registrar

# Health Checks

- Health Check => automated DNS fail-overs:
  - Health checks that monitor an endpoint (application, server, other AWS resource)
  - Health checks that monitor other health checks (calculated health checks)
  - Health checks that monitor CloudWatch alarms (full control!!) - e.g. throttles of DynamoDB, alarms on RDS, custom metrics, etc

- Health Checks are integrated with CW metrics

- Health Checks can be setup to pass/fail based on text in the first 5120 bytes of the response
- Health Checks pass only with 2xx and 3xx status response
- Calculated health checks
  - Create separate individual health checks
  - Specify how many of the health checks need to pass to make the parent pass
- Health Checks can trigger CW Alarms

# Health Checks - Private Hosted Zones

- Route53 health checks are outside the VPC
- They can't access private endpoints (private VPC or on-premise resource)

- Options:
  - To check a resource within a VPC, you must assign a public IP address
  - You can configure the health checker to check the health of an external resource the instance relies on, for example a database server
  - You can create a CloudWatch metric and associate an alarm. You then create a health check that checks the alarm itself

# Sharing a Private Zone across VPC

- Having a central private "Shared Services" DNS can ease management
- Other accounts may want to access the central private DNS records
  - Connectivity between VPC must be established (VPC Peering)
  - Must programmatically (CLI) associate the VPC with the central hosted zone
  - One association must be created for each new account