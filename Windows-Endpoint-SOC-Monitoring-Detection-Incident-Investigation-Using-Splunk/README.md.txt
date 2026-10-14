Windows Endpoint SOC Monitoring, Detection & Incident Investigation Using Splunk

Project Overview
This project demonstrates a Windows endpoint security monitoring lab built using Splunk Enterprise, Splunk Universal Forwarder, Windows Event Logs, and Sysmon.

The project focuses on collecting endpoint telemetry, building a monitoring dashboard, and investigating simulated authentication failures and suspicious process activity.

Objectives
- Collect and analyse Windows endpoint logs.
- Develop a Splunk dashboard for security monitoring.
- Investigate failed logons and account-lockout events.
- Analyse Sysmon process-creation events.
- Investigate PowerShell executions containing the `-EncodedCommand` parameter.
- Document investigation findings and SPL queries.

Lab Architecture
- SIEM: Splunk Enterprise on Windows 11
- Endpoint: Windows 10 virtual machine
- Log forwarding: Splunk Universal Forwarder
- Endpoint telemetry: Windows Event Logs and Sysmon
- Testing environment: Controlled lab simulations using Kali Linux

Investigations

1. Authentication Failure Investigation
Investigated simulated SMB authentication failures using Windows Security Event ID 4625 and examined account-lockout activity associated with Event ID 4740 where available.

2. Encoded PowerShell Investigation
Used Sysmon process-creation events and SPL searches to identify PowerShell executions containing the `-EncodedCommand` parameter. Encoded commands require further investigation and are not automatically malicious.

Tools Used
- Splunk Enterprise
- Splunk Universal Forwarder
- Splunk Search Processing Language (SPL)
- Sysmon
- Windows Event Viewer
- Windows 10 and Windows 11
- Kali Linux

Repository Structure
- report/ — Final project report
- screenshots/ — Dashboard and investigation evidence
- spl/ — SPL query documentation

Key Learning Outcomes
- Windows endpoint log collection and analysis
- SIEM dashboard development
- Security event investigation
- Process execution analysis
- Detection query development using SPL
- Security investigation documentation

Disclaimer
All testing was performed in a controlled lab environment for educational and defensive security purposes.