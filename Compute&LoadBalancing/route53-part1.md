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