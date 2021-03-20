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