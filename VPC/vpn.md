# Site to Site VPN (AWS Managed VPN)

- On-premise:
  - Setup a software or hardware VPN appliance to your on-premise network
  - The on-premise VPN should be accessible using a public IP
- AWS-side:
  - Setup a Virtual Private Gateway (VGW) and attach to your VPC
  - Setup a Customer Gateway to point the on-premise VPN appliance
- Two VPN connections (tunnels) are created for redundancy, encrypted using IPSec
- Can optionally accelerate it using Global Accelerator (for worldwide networks)

# Route Propagation in Site-to-Site VPN

- Static Routing:
  - Create static route in corporate data center for 10.0.0.1/24 through the CGW
  - Create static route in AWS for 10.3.0.0/20 through VGW
- Dynamic Routing:
  - Use BGP (Border Gateway Protocol) to share routes automatically (eBGP for internet)
  - We don't need to update the routing tables, it will be done for us dynamically
  - Just need to specify the ASN (Autonomous System Number) of the CGW and VGW

# AWS VPN CloudHub

- Can connect up to 10 Customer-Gateway for reach Virtual Private Gateway (VGW)
- Low cost hub-and-spoke model for primary or secondary network connectivity between locations
- Provide secure communication between sites, if you have multiple VPN connections
- It's a VPN connection so it goes over the public internet
- Can be a failover connection between your on-premise locations

# AWS Client VPN

- Connect from your computer using OpenVPN to your private network in AWS and on-premise

# Software VPN (not AWS managed)

- You can setup your own software VPN but you have to manage everything including bandwidth, redundancy etc
- You would have more control over the setup and routing options

# VPN to multiple VPC

- For VPN-based customers, AWS recommends creating a separate VPN connection for each customer VPC
- Direct Connect is recommended because it has a Direct Connect Gateway

# Shared Services VPC

- Create a VPN Connection on-premise and shared service VPC
- Replicate services, applications, databases between on-premise and the Shared Services VPC or deploy proxies in the shared service VPC
- Do VPC peering between the VPC and the shared service VPC
- VPCs can directly access the Shared Service VPC services and do not need VPN connections to on-premise

