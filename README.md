# Building a SOC + Honeynet in Azure (Live Traffic)
![Portfolio FIN](https://github.com/user-attachments/assets/a6bbe2f0-0b75-489e-8617-6617577bc0a5)


## Introduction

In this project, I built a mini honeynet in Azure. I ingested log sources from various resources into a Log Analytics workspace, which Microsoft Sentinel then used to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, applied some security controls to harden the environment, measured metrics for another 24 hours, and then showed the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
<img width="871" alt="Portfolio before ARCH" src="https://github.com/user-attachments/assets/286c47f7-3e74-4994-ae59-867e29780a3c">


## Architecture After Hardening / Security Controls
<img width="871" alt="After ARCH" src="https://github.com/user-attachments/assets/74248170-b9b0-4f1c-b937-0407256a734f">


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 Linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed and exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources were deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
<img width="858" alt="Linux SSH fail 24h before" src="https://github.com/user-attachments/assets/5481237d-67f7-41b0-8ccc-b7f451847b61">
<img width="902" alt="NSG malicous inbound 24h before" src="https://github.com/user-attachments/assets/e18bd4cf-92fe-443d-897a-7e9eb84fad8f">
<img width="891" alt="Windows RDP-SMB auth fail 24h before" src="https://github.com/user-attachments/assets/d67054f0-8ab0-4b5b-9131-44a5c1f821ff">
<img width="896" alt="Screenshot 2024-10-13 150338" src="https://github.com/user-attachments/assets/7d5f9805-6c2a-4e32-8e06-41d16f2bfdb1">



## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:

Start Time 2024-10-12T21:52:48

Stop Time 2024-10-13T21:52:48

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 68210
| Syslog                   | 2845
| SecurityAlert            | 33
| SecurityIncident         | 292
| AzureNetworkAnalytics_CL | 4041

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24-hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:

Start Time 2024-10-14T18:05:39

Stop Time	2024-10-15T18:05:39

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 4387
| Syslog                   | 0
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure, and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied and then again after implementing security measures. It is noteworthy that the number of security events and incidents was drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
