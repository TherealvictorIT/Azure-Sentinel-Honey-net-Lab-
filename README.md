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

For the “Before” metrics, all resources were deployed with exposure to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources were deployed with public endpoints visible to the Internet.  

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of an admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint  


## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://github.com/TherealvictorIT/Azure-Sentinel-Honey-net-Lab-/assets/125538763/c58454a2-5887-43c7-9e92-f6fb0f012f03)<br>
![Linux Syslog Auth Failures](https://github.com/TherealvictorIT/Azure-Sentinel-Honey-net-Lab-/assets/125538763/3594d3bd-9b1c-4796-8572-b9854a04ecfb)<br>
![Windows RDP/SMB Auth Failures](https://github.com/TherealvictorIT/Azure-Sentinel-Honey-net-Lab-/assets/125538763/0187de7a-0249-411c-ba4c-ac235f168848)<br>
![MSSQL Auth Faiures](https://github.com/TherealvictorIT/Azure-Sentinel-Honey-net-Lab-/assets/125538763/1420d52c-54d1-4d20-beac-14bc3c0f3957)<br> 


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-11-21 T15:37
Stop Time 2023-11-22 T15:37

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
Start Time 2023-12-07 19:12
Stop Time	2023-12-08 19:12 

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 171
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a miniature honeynet was built in Microsoft Azure, integrating log sources into a Log Analytics workspace. Microsoft Sentinel was utilized to generate alerts and incidents based on ingested logs. Metrics were assessed in the insecure environment before implementing security controls and measured again afterward. Notably, the implementation of security measures resulted in a significant reduction in security events and incidents, showcasing their effectiveness.

It's important to acknowledge that if the network resources were extensively used by regular users, the 24-hour period following the implementation of security controls might have led to an increased generation of security events and alerts.
