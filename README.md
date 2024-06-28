# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Architecture](https://github.com/ryansays/Cloud-SOC/assets/173171546/56cde68c-a542-4e9b-a889-70bf0835c092)


## Project Details

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls

![open_enviornment](https://github.com/ryansays/Cloud-SOC/assets/173171546/61115be6-cd8f-4e60-a531-7a4ad7529c19)

## Architecture After Hardening / Security Controls

![secured_enviornment](https://github.com/ryansays/Cloud-SOC/assets/173171546/924b9dab-f0f6-4c95-8c1b-07ebfc06f035)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
<img width="1164" alt="BEFORE_nsg-malicious-allowed-in" src="https://github.com/ryansays/Cloud-SOC/assets/173171546/f884c398-2629-44d3-a540-d999cdae05b0"><br>
<img width="1150" alt="BEFORE-windows-rdp-smb-auth-fail" src="https://github.com/ryansays/Cloud-SOC/assets/173171546/1db3acfa-b592-4406-958e-49deca3b3bee"><br>
<img width="1283" alt="BEFORE-linux-ssh-auth-fail" src="https://github.com/ryansays/Cloud-SOC/assets/173171546/a5991750-2a21-46d2-82f5-e51b3648c7b5"><br>


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-06-22 13:21
Stop Time 2024-06-23 13:21

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 10392
| Syslog                   | 2438
| SecurityAlert            | 1
| SecurityIncident         | 150
| AzureNetworkAnalytics_CL | 2376

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-06-25 16:08
Stop Time	2024-06-26 16:08

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 9245
| Syslog                   | 1
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.# Cloud-SOC
