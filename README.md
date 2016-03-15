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

[x] Version 1.5 - 05.March.2015
 
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