# Hyper-V Reporting Script (Powershell & HTML) #

It can be difficult to monitor and assess resources in large Hyper-V environments. This Powershell based script helps you to understand virtualization inventory, capacity and general resource availability in your Standalone or Clustered Hyper-V Environment.


 ![](Images/get-hypervreport-ps.png?raw=true)


## Highlights ##


* Creates a plain but detailed and user-friendly HTML report which is compatible with all modern browsers.
* Has an Overview section which shows momentary cluster resource usage.
* Storage Overcommitment (see details below)
* Shows alerts in the report for certain situations (utilizations, vm checkpoints, replication status, etc.)
* Provides more detailed information via tooltips in the HTML report. (cells with asteriks and highlighted)
* Includes a mode that reports only alerts in the Hyper-V environment. (aka HighlightsOnly mode)
* Collects information by using standard Hyper-V and Clustering PowerShell cmdlets and custom WMI queries.
* Checks and installs required runtime environment prerequisites like Hyper-V and Clustering Powershells.
* Can be used directly from command-line or as a scheduled Windows task.
* Supports report delivery via e-mail with advanced options. (authentication, TLS/SSL, multiple recipients)
* Advanced error handling and logging. (Console messages and log file) 


## Version History and Change Log ##

[x] Version 1.5 - 15.March.2016
 
* Added
 * Windows 8 and 8.1 OS support for script runtime environment
 * New Cluster Overview section
 * Storage Overcommitment
 * Supports for Extended Replica reporting
 * Hyper-V host information extended
 * VM Virtual Network information
 * $ReportFileNameTimeStamp parameter
   
* Removed
 * $ReportIsBodyHTML parameter is no longer available
 
## Report Details ##
 
**Cluster Overview** (Applicable on clusters only)

* Physical Resources
 * Node
 * Processor
 * Memory
 * Storage
 
* Physical Resources
 * vMachine
 * vProcessor
 * vMemory
 * vStorage
 

 ![](Images/get-hypervreport-cluster-overview.PNG?raw=true)
 
 
**Hyper-V Host Table** (Clustered or Standalone)

* Hostname
 *Computer Manufacturer, Model
* Operating System Version
* State
* Uptime
* Domain Name
* Total and Running VM Count
 * Detailed as Clustered and Non-clustered
* Processor Count
 * Logical processor count
 * Physical processor socket count
 * Processor Manufacturer, Model, Ghz
 * Hyper-Threading state for Intel processor (shown as tooltip)
 * Virtual Processors per Logical Processor ratio 
* Physical RAM capacity
 * Used, Free, Total


 ![](Images/get-hypervreport-cluster-nodes.png?raw=true)
 
 
**Disk/Volume Table** (Clustered or Local)

* Volume
 * Name (Local Volume, Clustered Volume, Cluster Shared Volume)
 * Label or CSV path (shown as tooltip)
 * Disk name (Physical Disk, Clustered Disk)
 * Total/Allocated/Unallocated physical disk size (shown as tooltip) 
* Disk/Volume State
* Usage (Logical Partition, Cluster Volume, Cluster Shared Volume, Quorum, System Volume)
* Owner
* Physical Disk Bus Type
* Volume File System
* Active VHD (storage overcommitment)
* Disk and volume capacity
 * Used, Free, Total
 

 ![](Images/get-hypervreport-cluster-disk.PNG?raw=true)
 

**Virtual Machine Table**

* Instance
 * VM name
 * Configuration XML path (shown as tooltip)
 * Generation
 * Version 
* State
* Uptime
* Owner
* Virtual Processor
 * Counts 
* Virtual RAM
 * Startup, Minimum, Maximum, Assigned 
* Integration Services
 * State like UpToDate, UpdateRequired, MayBeRequired, NotDetected
 * Version number (shown as tooltip) 
* Checkpoint
 * Checkpoint state
 * Checkpoint count (if exists, shown as tooltip)
 * Checkpoint chain (if exists) 
* Replica
 * Replication State and Health
 * Primary, Replica and Extended modes
 * Replica Server or Primary Server (shown as tooltip)
 * Replication Frequency (shown as tooltip)
 * Last Replication Time (shown as tooltip) 
* Disk
 * VHD Name
 * VHD File Path (shown as tooltip)
 * Current VHD file size
 * Maximum VHD disk size
 * VHD Type
 * Controller Type
 * VHD fragmentation percent
 * Including pass-trough disks (if exists)
 * Including differencing virtual disk chain (if exists) 
* Network Adapter
 * Device type
 * Connection status
 * Virtual switch name
 * IP address
 * VLAN ID
 * Advanced - MAC Address, MAC Type, DHCP Guard, Raouter Guard, Port Mirroring, Protected Network
* Can detects missing VHD files
* Can detects clustered VM configuration resource problems like offline
* Can detects clustered VM failed state


![](Images/get-hypervreport-vms.png?raw=true)


## Requirements ##

**Hyper-V Targets** (Clustered or Standalone)

* Active Directory domain membership
* Supported Operating Systems
 * Windows Server 2012
 * Windows Server 2012 R2
 * Hyper-V Server 2012
 * Hyper-V Server 2012 R2
 
**Script Runtime Operating System** (Directly on a Hyper-V target or remote Windows operating system)

* Same or trusted Active Directory domain membership with Hyper-V target
* Supported Operating Systems
 * Windows Server 2012
 * Windows Server 2012 R2
 * Windows 8
 * Windows 8.1
* Windows PowerShell 3.0 or 4.0 (installed by default on supported server operating systems)
* Sets the Windows PowerShell execution policy to RemoteSigned or Unrestricted
* Hyper-V PowerShell (if not, automatically installed by the Get-HyperVReport.ps1 for server oses)
* Failover Clustering PowerShell (if not, automatically installed by the Get-HyperVReport.ps1 for server os')
* The script requires administrative privileges on the target Hyper-V server(s)


## Usage ##

**1) Creates a Hyper-V Cluster report in the working directory.**

.\Get-HyperVReport.ps1 -Cluster Hvcluster1

**2) Creates a Hyper-V Cluster report that shown only highlighted events and alerts in the working directory.**

.\Get-HyperVReport.ps1 -Cluster Hvcluster1 -HighlightsOnly $true

**3) Creates one or more standalone Hyper-V Host(s) report in the working directory.**

.\Get-HyperVReport.ps1 -VMHost Host1,Host2,Host3

**4) Creates a Hyper-V Cluster report and sends it to multiple recipients as attachment without smtp authentication.**

.\Get-HyperVReport.ps1 -Cluster Hvcluster1 -SendMail $true -SMTPServer 10.29.0.50 -MailFrom sender@hyperv.com -MailTo recepient1@hyperv.com,recepient2@hyperv.com

**5) Creates a Hyper-V Cluster report and sends it to multiple recipients as attachment with smtp authentication and TLS/SSL communication. -SMTPServerTLSorSSL is optional and used if forced by the smtp server.**

.\Get-HyperVReport.ps1 -Cluster Hvcluster1 -SendMail $true -SMTPServer smtp.mailserver.com -SMTPPort 587 -MailFrom sender@hyperv.com -MailFromPassword P@ssw0rd -SMTPServerTLSorSSL $true -MailTo recepient1@hyperv.com,recepient2@hyperv.com

