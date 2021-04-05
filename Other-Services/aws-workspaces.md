# AWS WorkSpaces

- Managed, Secure Cloud Desktop
- Great to eliminate management of on-premise VDI (Virtual Desktop Infrastructure)
- On Demand, pay per by usage
- Secure, Encrypted, Network Isolation
- Integrated with Microsoft Active Directory

WorkSpaces Application Manager (WAM)
- Deploy and Manage applications as virtualized application containers
- Provision at scale and keep the applications updated using WAM

Windows Updates
- By default, Amazon WorkSpaces are configured to install software updates
- Amazon WorkSpaces with Windows will have Windows Update turned on
- You have full control over the Windows Update frequency

Maintenance Windows
- Updates are installed during maintenance windows (you define them)
- Always On WorkSpaces: default is from 000h00 to 04h00 on Sunday morning
- AutoStop WorkSpaces: automatically starts once a month to install updates
- Manual maintenance: you define your windows and perform maintenance

# Amazon AppStream 2.0

- Desktop Application Streaming Service
- Deliver to any computer, without acquiring, provisioning infrastructure
- The application is delivered from within a web browser

# Amazon AppStream 2.0 vs WorkSpaces

- WorkSpaces
  - Fully managed VDI and desktop available
  - The user connect to the VDI and open native or WAM applications
  - Workspaces are on-demand or always on

- AppStream 2.0
  - Stream a desktop application to web browsers (no need to connect to a VDI)
  - Works with any device (that has a web browser)
  - Allow to configure an instance type per application type (CPU, RAM, GPU)


 