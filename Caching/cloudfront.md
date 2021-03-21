# AWS CloudFront

- Content Delivery Network (CDN)
- Improves read performance, content is cached at the edge
- 216 Point of Presence globally (edge locations)
- DDoS protection, integration with Shield, AWS Web Application Firewall
- Can expose external HTTPS and can talk to internal HTTPS backends

# Origins

- S3 bucket
  - For distributing files and caching them at the edge
  - Enhanced security with CloudFront Origin Access Identity
  - CloudFront can be used as an ingress (to upload files to S3)
- S3 website
  - Must first be enabled in the bucket as a static S3 website
- Custom Origin (HTTP)
  - Application Load Balancer
  - EC2 instance
  - API Gateway (for more control..otherwise use API Gateway Edge)
  - Any HTTP backend you want
  
  - Possibility to have a primary and secondary origin (HA Failover)

# CloudFront vs S3 Cross Region Replication

- CloudFront:
  - Global Edge network
  - Files are cached for a TTL (maybe a day)
  - Great for static content that must be available everywhere
- S3 Cross Region Replication:
  - Must be setup for each region you want application to happen
  - Files are updated in near real-time
  - Read only
  - Great for dynamic content that needs to be available at low-latency in few regions

# CloudFront Geo Restriction

- You can restrict who can access your distribution
  - Whitelist: Allow your users to access your content only if they're in one of the countries on a list of approved countries.
  - Blacklist: Prevent your users from accessing your content if they're in one of the countries on a blacklist of banned countries

- The "country" is determined using a 3rd party Geo-IP database
- Use case: Copyright Laws to control access to content

# Signed URL / Signed Cookies

- You want to distribute paid shared content to premium users over the world
- We can use CloudFront Signed URL / Cookie. We attach a policy with:
  - Includes URL expiration
  - Includes IP ranges to access the data from
  - Trusted signers (which AWS accounts can create signed URLs)
- How long should the URL be valid for?
  - Shared content (movie, music): make it short (a few minutes)
  - Private content (private to the user): you can make it last for years


- Signed URL = access to individual files (one signed URL per file)
- Signed Cookies = access to multiple files (one signed cookie for many files)


# CloudFront Signed URL vs S3 Pre-Signed URL

- CloudFront Signed URL:
  - Allow access to a path, no matter the origin
  - Account wide key-pair, only the root can manage it
  - Can filter by IP, path, date, expiration
  - Can leverage caching features
- S3 Pre-Signed URL:
  - Issue a request as the person who pre-signed the URL
  - Uses the IAM key of the signing IAM principal
  - Limited lifetime

# Caching

- Cache based on
  - Headers
  - Session Cookies
  - Query String Parameters
- The cache lives at each CloudFront Edge Location
- You want to maximize the cache hit rate to minimize requests on the origin
- Control the TTL (0 seconds to 1 year), can be set by origin using the Cache-Control header, Expires header


# Lambda@Edge

- You have deployed a CDN using CloudFront
- What if you wanted to run a global AWS Lambda alongside
- Or how to implement request filtering before reaching your application?
- For this, you can use Lambda@Edge:
  - Deploy Lambda functions alongside your CloudFront CDN
  - Build more responsive applications
  - You don't manager servers, Lambda is deployed globally
  - Customize the CDN content
  - Pay only for what you use

- You can use Lambda to change CloudFront requests and responses:
  - After CloudFront receives a request from a viewer (viewer request)
  - Before CloudFront forwards the request to the origin (origin request)
  - After CloudFront receives the response from the origin (origin response)
  - Before CloudFront forwards the response to the viewer (viewer response)
- You can also generate responses to viewers without ever sending the request to the origin
- Lambda@Edge does not have any cache. It's only to change requests/responses

# Lambda@Edge: Use Cases

- Website Security and Privacy
- Dynamic Web Application at the Edge
- Search Engine Optimization (SEO)
- Intelligently Route Across Origins and Data Centers
- Bot Mitigation at the Edge
- Real-time Image Transformation
- A/B Testing
- User Authentication and Authorization
- User Prioritization, User Tracking and Analytics
- Increasing the cache hit ration (by modifying headers, normalize user-agent)
