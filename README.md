# honeynetsoc
# Building a SOC + Honeynet in Azure (Live Traffic)
![honeynetsoc](https://github.com/mar7inb/honeynetsoc/assets/90795866/c5078a2a-3a54-4f65-b242-09bf538fe54d)


## Introduction

In this project, I constructed a small-scale imitation network to attract potential cyber threats within the Azure platform. I collected data from various sources and funneled it into a central workspace called Log Analytics. Microsoft Sentinel, a security tool, and utilized this data to visualize attack patterns, generate notifications for suspicious activities, and establish records of security breaches.

I followed a two-day process: initially, I observed security-related measurements in an unsecured environment for a day. Then, I implemented security measures to strengthen the system, observed measurements for another day, and compared the outcomes. The metrics I'm presenting include:

1.SecurityEvent (Windows Event Logs)
2.Syslog (Linux Event Logs)
3.SecurityAlert (Notifications generated by Log Analytics)
4.SecurityIncident (Confirmed security breaches recorded by Sentinel)
5.AzureNetworkAnalytics_CL (Identified malicious network flows that penetrated the imitation network)

## Architecture Before Hardening / Security Controls
![beforehardeningsoc](https://github.com/mar7inb/honeynetsoc/assets/90795866/8c7069cd-aeb4-4460-adca-fe0ec81b85eb)


## Architecture After Hardening / Security Controls
![afterhardeningsoc](https://github.com/mar7inb/honeynetsoc/assets/90795866/5616acd9-0eac-4e08-8cd4-9ab8ffd07702)


The design of the mini honeynet in Azure involves the following main parts:

-Virtual Network (VNet): This creates a segmented network environment.

-Network Security Group (NSG): It manages inbound and outbound traffic.

-Virtual Machines (2 Windows and 1 Linux): These are the operating systems running in the network.

-Log Analytics Workspace: It centralizes and manages log data.

-Azure Key Vault: This securely stores sensitive information.

-Azure Storage Account: It stores various types of data.

-Microsoft Sentinel: A tool for advanced threat detection and response.

For the "BEFORE" measurements, all resources were initially set up and made accessible from the internet. The Virtual Machines had unrestricted Network Security Groups and open firewalls, and other resources also had -public endpoints exposed to the internet. Private Endpoints weren't utilized.

For the "AFTER" measurements, Network Security Groups were made more secure by blocking all traffic except for that originating from my admin workstation. Additionally, other resources were safeguarded by their built-in firewalls and Private Endpoints were utilized.

## Attack Maps Before Hardening / Security Controls
![windows24insec](https://github.com/mar7inb/honeynetsoc/assets/90795866/951d8285-cb99-4414-9df4-2eca726ce551)
![nsg24insec](https://github.com/mar7inb/honeynetsoc/assets/90795866/01ccbe82-cccc-44a3-837e-8f72fd80dc5b)
![syslog24insec](https://github.com/mar7inb/honeynetsoc/assets/90795866/7a48098f-f650-441c-bfd0-2d13ff87991d)




## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-08-21 8:30 AM
Stop Time 2023-08-22 8:32 AM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 13136
| Syslog                   | 1088
| SecurityAlert            | 2
| SecurityIncident         | 154
| AzureNetworkAnalytics_CL | 1194

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-08-18 5:30 PM
Stop Time	2023-08-19 5:37 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8372
| Syslog                   | 1
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a small-scale honeynet was set up in Microsoft Azure. This network collected logs and information in a Log Analytics workspace. Microsoft Sentinel, a security tool, was utilized to spot potential issues and create records of these incidents based on the gathered data.

Moreover, the project involved measuring certain metrics in an unsafe environment prior to the implementation of security measures. After these measures were put in place, the metrics were measured again. Notably, there was a significant decrease in the number of security events and incidents, which demonstrated the effectiveness of the security controls.

It's important to mention that if the network's resources were extensively used by regular users, it's likely that there would have been more security events and alerts generated during the 24-hour period after the security controls were implemented.
