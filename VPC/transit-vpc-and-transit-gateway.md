# Transit VPC (=Software VPN)

- Not an AWS offering, newer managed solution is Transit Gateway
- Uses the public internet with a software VPN solution
- Allows for transitive connectivity between VPC & locations
- More complex routing rules, overlapping CIDR ranges, network-level packet filtering

# Transit Gateway

- For having transitive peering between thousands of VPC and on-premise, hub-and-spoke (star) connection
- Region resource, can work cross-region
- Share cross-account using Resource Access Manager (RAM)
- You can peer Transit Gateway across regions
- Route Tables: limit which VPC can talk with other VPC
- Works with Direct Connect Gateway, VPN connections
- Supports IP Multicast (not supported by any other AWS service)
- Instances in VPC can access a NAT Gateway, NLB, PrivateLink and EFS in others VPCs attached to the AWS Transit Gateway