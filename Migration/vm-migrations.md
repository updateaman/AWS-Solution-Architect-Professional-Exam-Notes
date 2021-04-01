# Application Discovery Services

- Plan migration projects by gathering information about on-premises data centers
- Server utilization data and dependency mapping are important for migrations
- Agentless discovery (Application Discovery Agentless Connector):
  - Open Virtual Appliance (OVA) package that can be deployed to a VMware host
  - VM inventory, configuration, performance history such as CPU, memory and disk usage
  - OS agnostic
- Agent-based discovery:
  - system configuration, system performance, running processes and details of the network connections between systems
  - Supports Microsoft Server, Amazon Linux, RedHat, CentOS, SUSE
- Resulting data can be exported as CSV or viewed within AWS Migration Hub
- Data can be explored using pre-defined queries in Amazon Athena

# AWS Server Migration Service (SMS)

- Migrate entire VMs to AWS, improvement over EC2 VM Import/Export service
- That means the OS, the data, everything is kept intact
- After loading the VM onto EC2, then you can update the OS, the data, make an AMI
- Therefore SMS is used to Re-host
- Only works with VMware vSphere, Windows Hyper-V and Azure VM
- Every replication creates an EBS snapshot/AMI ready for deployment on EC2
- Every replication is incremental
- "One time migrations" or "replication every interval" option

# On-Premise strategy with AWS

- Ability to download Amazon Linux 2 AMI as a VM (.iso format)
  - VMWare, KVM, VirtualBox (Oracle VM), Microsoft Hyper-V
- AWS Application Discovery Service
  - Gather information about your on-premise servers to plan a migration
  - Server utilization and dependency mappings
  - Track with AWS Migration Hub
- AWS VM Import/Export
  - Migrate existing applications into EC2
  - Create a DR repository strategy for your on-premise VMs
  - Can export back the VMs from EC2 to on-premise
- AWS Server Migration Service (SMS)
  - Incremental replication of on-premise live servers to AWS
  - Migrates the entire VM into AWS
- AWS Database Migration Service (DMS)
  - replicate On-premise => AWS, AWS => AWS, AWS => On-premise
  - Works with various database technologies (Oracle MySQL, DynamoDB)