# Types of load balancers on AWS

- 3 kinds of managed load balancers

- Classic Load Balancer (v1 old generation) - 2009
  - Http, Https, TCP
- Application Load Balancer (v2 - new generation) -2016
  - Http, Https, WebSocket
- Network Load Balancer (v2 - new generation) - 2017
  - TCP, TLS (secure TCP) & UDP

- You can setup internal (private) or external (public) ELBs

# Classic Load Balancers (v1)

- Health checks can be http (L7) or TCP (L4)
- Supports only one SSL certificate
  - The SSL certificate can have many SAN (subject alternate name) but the SSL certificate must be changed anytime SAN is added/edited/removed
  - Better to use ALB with SNI (server name indication)
  - Can use multiple CLB if you want distinct SSL certificates

- TCP => TCP passes all the traffic to the EC2 instance
  - Only way to use 2-way SSL authentication

# Application Load Balancer (v2)

- Application load balancer is Layer 7 (http)
- Load balancing to multiple http applications across machines (target groups)
- Load balancing to multiple applications on the same machine (ex: containers)
- Support for HTTP/2 and websocket
- Support redirects (from http to https)

- Routing tables to different target groups:
  - Routing based on path in URL (example.com/user & example.com/posts)
  - Routing based on hostname in URL (one.example.com & other.example.com)
  - Routing based on Query String, Headers (example.com/users?id=123&order=false)

- ALB are a great fit for micro services & container-based application (example: Docker & Amazon ECS)
- Has a port mapping feature to redirect to a dynamic port in ECS
- In comparison, we'd need multiple Classic Load Balancer per application

# Network Load Balancer (v2)

- Network load balancers (Layer 4) allow to do:
  - Forward TCP traffic to your instances (UDP support - Jun 2019)
  - Handle millions of request per seconds
  - NLB has one static IP per AZ, and supports assigning Elastic IP (helpful for whitelisting specific IP)
  - Less latency ~ 100ms (400ms for ALB)
  - Supports TLS
  - Support for WebSockets

- Network Load Balancers are mostly used:
- for extreme performance, TCP or UDP traffic
- with AWS Private Link to expose a service internally

- Target Groups:
  - EC2 instances (can be managed by an ASG) - TCP
  - ECS tasks (managed by ECS itself) - TCP
  - IP addresses - Private IP only, even outside your VPC

- Proxy Protocol:
  - Send additional connection information such as the source and destination
  - The load balancer prepends a proxy protocol header to the TCP data
  - Helpful when you have the "IP addresses" target group type
    - You can retrieve the source IP addresses of the originating client

# Cross-Zone Load Balancing

- With Cross Zone Load Balancing: each load balancer instance distributes evenly across all the registered instances in all AZ

- Classic Load Balancer
  - Disabled by default
  - No charges for inter AZ data if enabled
- Application Load Balancer
  - Always on (can't be disabled)
  - No charges for inter AZ data
- Network Load Balancer
  - Disabled by default
  - You pay charges ($) for inter AZ data if enabled

# Load Balancer Stickiness

 - It is possible to implement stickiness so that the same client is always redirected to the same instance behind a load balancer
 - This works for Classic Load Balancer & Application Load Balancer
 - The "cookie" used for stickiness has an expiration date you control
 - Use case: make sure the user doesn't lose their session data
 - Enabling stickiness may bring imbalance to the load over the backend EC2 instances
 - Alternative is to cache session data in ElastiCache, DynamoDB 