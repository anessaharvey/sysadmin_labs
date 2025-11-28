Lab 1.1: Domain Controller Installation \& Configuration

Objective: Install and configure a Windows Server 2025 Domain Controller

Tasks:

1\.	Install Windows Server 2025 on DC01 in VMware Workstation 

&nbsp;	Select Windows Server 2025 Standard (Desktop Experience)

&nbsp;	Set Administrator password (complex: Min 14 chars)

2\.	Configure static IP on VMnet2 network: 

&nbsp;	IP Address: 192.168.10.10

&nbsp;	Subnet Mask: 255.255.255.0

&nbsp;	Default Gateway: 192.168.10.1 (leave blank if no router)

&nbsp;	Preferred DNS: 127.0.0.1

&nbsp;	Alternate DNS: 8.8.8.8

3\.	Set hostname to DC01 and restart

4\.	Install Active Directory Domain Services role



powershell

&nbsp;  Install-WindowsFeature AD-Domain-Services -IncludeManagementTools

5\.	Promote server to Domain Controller 

&nbsp;	Create new forest: cyberlabs.local

&nbsp;	Domain/Forest functional level: Windows Server 2016 or higher

&nbsp;	Install DNS Server role (automatically selected)

&nbsp;	Set DSRM password

&nbsp;	Allow server to restart



6\.	After restart, configure DNS forwarders (8.8.8.8, 1.1.1.1)

powershell

&nbsp;  Add-DnsServerForwarder -IPAddress 8.8.8.8

&nbsp;  Add-DnsServerForwarder -IPAddress 1.1.1.1

7\.	Create reverse lookup zone for 192.168.10.0/24 

&nbsp;	DNS Manager → Reverse Lookup Zones → New Zone

&nbsp;	Primary zone, Active Directory integrated

&nbsp;	Network ID: 192.168.10





Verification:

•	Run dcdiag and resolve any errors

•	Verify DNS resolution: nslookup cyberlabs.local

•	Check SYSVOL replication status: Get-SmbShare

•	Test DNS forwarders: nslookup google.com

VMware Snapshot: Create snapshot "DC01-Baseline" after successful configuration

Deliverable: Screenshot of dcdiag output showing passed tests



