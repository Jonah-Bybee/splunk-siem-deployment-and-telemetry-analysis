# Splunk SIEM Deployment and Endpoint Telemetry Analysis

## Overview

This project documents the deployment of a Splunk Enterprise Security Information and Event Management (SIEM) environment designed to centralize Windows endpoint telemetry using Sysmon and the Splunk Universal Forwarder.

The objective was to design, build, troubleshoot, and validate an end-to-end monitoring pipeline capable of supporting future detection engineering, threat hunting, alert development, and incident investigation activities.

---

## Architecture

<p align="center">
  <img src="images/architecture-diagram.png" width="100%">
</p>

The environment consists of a Windows 10 endpoint generating native Windows Event Logs and Sysmon telemetry, which is forwarded through the Splunk Universal Forwarder to a centralized Splunk Enterprise server hosted on Ubuntu Server.

### Technologies Used

* Splunk Enterprise 10.4
* Ubuntu Server
* Windows 10
* Sysmon
* Splunk Universal Forwarder
* Oracle VirtualBox
* SPL (Search Processing Language)

---

## Validation

### Endpoint Registration Validation

<p align="center">
  <img src="images/endpoint-registration-validation.png" width="90%">
</p>

The following SPL query was used to verify endpoint registration:

```spl
| metadata type=hosts
```

This confirmed that the Windows endpoint was successfully connected and actively forwarding telemetry to Splunk.

---

### Data Source Validation

<p align="center">
  <img src="images/data-source-validation.png" width="90%">
</p>

The following SPL query was used to validate available log sources:

```spl
index=main
| stats count by source
```

Validated sources included:

* WinEventLog:Security
* WinEventLog:System
* WinEventLog:Application
* XmlWinEventLog:Microsoft-Windows-Sysmon/Operational

This confirmed successful ingestion of both native Windows logs and enhanced Sysmon telemetry.

---

## Endpoint Telemetry Analysis

### Process Creation Investigation (Sysmon Event ID 1)

<p align="center">
  <img src="images/process-creation-investigation.png" width="90%">
</p>

Controlled activity was generated using:

* whoami
* ipconfig
* hostname
* notepad
* calc

The resulting Sysmon Event ID 1 telemetry was used to investigate:

* Process execution
* Command-line arguments
* Parent-child process relationships
* User attribution

---

### DNS Query Investigation (Sysmon Event ID 22)

<p align="center">
  <img src="images/dns-query-investigation.png" width="90%">
</p>

Controlled DNS activity was generated using:

```powershell
nslookup github.com
```

This demonstrated process-level DNS visibility and validated Sysmon Event ID 22 collection.

---

### Network Connection Investigation (Sysmon Event ID 3)

<p align="center">
  <img src="images/network-connection-investigation.png" width="90%">
</p>

Controlled network activity was generated using:

```powershell
curl https://github.com
```

This demonstrated visibility into outbound network connections and validated Sysmon Event ID 3 collection.

---

## Challenges Solved

Throughout deployment and validation, several issues required troubleshooting and root-cause analysis:

* Incorrect EVTX collection method resulting in binary data ingestion
* Sysmon forwarding permissions issues
* XML rendering configuration challenges
* Structured field extraction from Sysmon telemetry
* Historical telemetry cleanup and validation

Resolving these issues provided practical experience troubleshooting log collection, parsing, permissions, and data normalization within a SIEM environment.

---

## Skills Demonstrated

* Splunk Enterprise Deployment
* SIEM Administration
* Sysmon Configuration
* Splunk Universal Forwarder
* Windows Event Logging
* Endpoint Telemetry Analysis
* SPL Query Development
* Log Source Validation
* Root Cause Analysis
* Security Monitoring
* Detection Engineering Fundamentals
* VirtualBox Networking
* Ubuntu Server Administration

---

## Full Technical Documentation

The complete technical report is available here:

📄 [Splunk SIEM Deployment and Endpoint Telemetry Analysis](report/Splunk_SIEM_Deployment_and_Endpoint_Telemetry_Analysis.pdf)

---

## Author

**Jonah Bybee**

* LinkedIn: https://linkedin.com/in/jonah-bybee-1ab829333
* GitHub: https://github.com/Jonah-Bybee
