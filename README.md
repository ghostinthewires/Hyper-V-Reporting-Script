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


