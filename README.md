# Azure Sentinel Honeynet Lab (Live Traffic)
![Cloud Honeynet / SOC](https://github.com/TherealvictorIT/Azure-Sentinel-Honey-net-Lab-/assets/125538763/33ad4cc3-33c9-415d-af6f-e9ebd4b1df51)

## Introduction

The primary objective of this lab is to intentionally expose our environment to potential threats, allowing us to observe and analyze the behavior of bad actors on the internet. I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

-SecurityEvent (Windows Event Logs)  
-Syslog (Linux Event Logs)  
-SecurityAlert (Log Analytics Alerts Triggered)  
-SecurityIncident (Incidents created by Sentinel)  
-AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)  


## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://github.com/TherealvictorIT/Azure-Sentinel-Honey-net-Lab-/assets/125538763/d0aac605-677e-492e-b256-16e910db6b25">)


## Architecture After Hardening / Security Controls
![Architecture Diagram](https://github.com/TherealvictorIT/Azure-Sentinel-Honey-net-Lab-/assets/125538763/97899627-2aed-4629-84ab-03ea88a1def0">)

The structure of the honeynet in Azure comprises the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the “Before” metrics, all resources were deployed with exposure to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources were deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.  

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of an admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint  


## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://github.com/TherealvictorIT/Azure-Sentinel-Honey-net-Lab-/assets/125538763/c58454a2-5887-43c7-9e92-f6fb0f012f03)<br>
![Linux Syslog Auth Failures](https://github.com/TherealvictorIT/Azure-Sentinel-Honey-net-Lab-/assets/125538763/3594d3bd-9b1c-4796-8572-b9854a04ecfb)<br>
![Windows RDP/SMB Auth Failures](https://github.com/TherealvictorIT/Azure-Sentinel-Honey-net-Lab-/assets/125538763/0187de7a-0249-411c-ba4c-ac235f168848)<br>
![MSSQL Auth Faiures](https://github.com/TherealvictorIT/Azure-Sentinel-Honey-net-Lab-/assets/125538763/1420d52c-54d1-4d20-beac-14bc3c0f3957)<br> 


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-11-23 T17:31:15.1322298Z
Stop Time 2023-11-23 T17:31:15.1322298Z

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 22476
| Syslog                   | 7747
| SecurityAlert            | 11
| SecurityIncident         | 168
| AzureNetworkAnalytics_CL | 3777

## Attack Maps After Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
