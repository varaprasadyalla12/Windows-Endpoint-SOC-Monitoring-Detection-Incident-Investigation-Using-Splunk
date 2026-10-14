# Windows Endpoint SOC Monitoring, Detection & Incident Investigation Using Splunk

## Table of Contents
1. Project Overview
2. Objectives
3. Implementation Workflow
4. Lab Architecture
5. Investigations
6. Tools Used
7. Repository Structure
8. Key Learning Outcomes
9. Project Evidence
10. Project Documentation
11. Disclaimer

---

## 1. Project Overview
This project demonstrates a Windows endpoint security monitoring lab built using Splunk Enterprise, Splunk Universal Forwarder, Windows Event Logs, and Sysmon.

The project focuses on collecting endpoint telemetry, building a monitoring dashboard, and investigating simulated authentication failures and suspicious process activity.

## 2. Objectives
- Collect and analyse Windows endpoint logs.
- Develop a Splunk dashboard for security monitoring.
- Investigate failed logons and account-lockout events.
- Analyse Sysmon process-creation events.
- Investigate PowerShell executions containing the `-EncodedCommand` parameter.
- Document investigation findings and SPL queries.

## 3. Implementation Workflow
This section describes the main stages used to build and test the Windows endpoint monitoring lab.

### Step 1: Prepare the Lab Environment
- Set up Splunk Enterprise on a Windows 11 host.
- Create a Windows 10 virtual machine to act as the monitored endpoint.
- Install Splunk Universal Forwarder on the Windows 10 machine.
- Install Sysmon to collect detailed process-creation and other endpoint telemetry.

Purpose: Establish a separate SIEM server and endpoint for security monitoring.

### Step 2: Configure Splunk Event Receiving
- Configure Splunk Enterprise to receive forwarded events on TCP port `9997`.
- Confirm that Splunk Web is accessible.
- Check that the receiving configuration is enabled.

Purpose: Prepare Splunk to receive logs from the monitored endpoint.

### Step 3: Configure Windows Log Forwarding
- Configure the Universal Forwarder to collect Windows Security, System, and Application event logs.
- Configure the forwarding destination to point to the Splunk Enterprise host on port `9997`.
- Restart the Universal Forwarder service after configuration changes.
- Verify that the service is running and that events are reaching Splunk.

Purpose: Send Windows endpoint telemetry to the central SIEM.

### Step 4: Integrate Sysmon Telemetry
- Install and verify Sysmon on the Windows 10 endpoint.
- Confirm that events are generated in the `Microsoft-Windows-Sysmon/Operational` channel.
- Configure the Universal Forwarder to collect Sysmon events.
- Verify that process-creation events are searchable in Splunk.

Purpose: Collect detailed endpoint activity for process investigation.

### Step 5: Validate the Incoming Data
- Search the collected events in Splunk.
- Review fields such as `host`, `source`, `sourcetype`, `EventCode`, and `CommandLine` where available.
- Confirm that Windows event logs and Sysmon events are present.
- Use the results to understand the available telemetry before creating detection searches.

Purpose: Ensure the monitoring data is available and useful for investigation.

### Step 6: Develop the Monitoring Dashboard
- Create a Splunk dashboard using searches over the collected events.
- Organize the panels to display overall event activity and source-level event counts.
- Include monitoring views for failed logons and process activity where data is available.
- Validate the panels against the underlying search results.

Purpose: Provide a central view of endpoint activity for monitoring and triage.

### Step 7: Investigate Authentication Failures
- Search Windows Security events for Event ID `4625`, which records failed logon attempts.
- Examine Event ID `4740` for account-lockout activity where available.
- Review the available event fields and identify patterns in the controlled lab activity.
- Document the evidence and investigation findings.

Purpose: Practice investigating authentication failures and related account-lockout activity.

### Step 8: Investigate PowerShell Process Activity
- Search Sysmon Event ID `1` process-creation events.
- Review PowerShell process command lines and related parent-process information where available.
- Search for command lines containing `-EncodedCommand`.
- Examine the surrounding event details before deciding whether further investigation is warranted.
- Document the findings and supporting evidence.

Purpose: Practice investigating potentially suspicious process execution without assuming that encoded commands are automatically malicious.

### Step 9: Document and Organize the Project
- Save screenshots of the lab configuration, dashboard, and investigations.
- Store the final project report in the `report/` directory.
- Store the investigation searches in the `spl/` directory.
- Organize the screenshots into folders by setup, dashboard, authentication investigation, and PowerShell investigation.
- Publish the documentation and supporting evidence in the GitHub repository.

Purpose:Make the project reproducible, understandable, and easy to review.

### End-to-End Data Flow

Windows 10 Endpoint
        |
        v
Windows Event Logs and Sysmon
        |
        v
Splunk Universal Forwarder
        |
        v
TCP Port 9997
        |
        v
Splunk Enterprise on Windows 11
        |
        v
SPL Searches and Analysis
        |
        v
Monitoring Dashboard and Investigation Findings


### Validation Notes
- Event availability depends on the activity generated and the endpoint configuration.
- Account-lockout events may not appear unless the relevant lockout conditions are met.
- Encoded PowerShell commands require contextual investigation; encoding alone does not establish malicious intent.
- Search field names and results should be verified against the events collected in the lab.

## 4. Lab Architecture
- SIEM: Splunk Enterprise on Windows 11
- Endpoint: Windows 10 virtual machine
- Log forwarding: Splunk Universal Forwarder
- Endpoint telemetry: Windows Event Logs and Sysmon
- Testing environment: Controlled lab simulations using Kali Linux

## 5. Investigations
### 5.1 Authentication Failure Investigation
Investigated simulated SMB authentication failures using Windows Security Event ID `4625` and examined account-lockout activity associated with Event ID `4740` where available.

### 5.2 Encoded PowerShell Investigation
Used Sysmon process-creation events and SPL searches to identify PowerShell executions containing the `-EncodedCommand` parameter. Encoded commands require further investigation and are not automatically malicious.

## 6. Tools Used
- Splunk Enterprise
- Splunk Universal Forwarder
- Splunk Search Processing Language (SPL)
- Sysmon
- Windows Event Viewer
- Windows 10 and Windows 11
- Kali Linux

## 7. Repository Structure
Windows-Endpoint-SOC-Monitoring-Detection-Incident-Investigation-Using-Splunk/
|
|-- README.md
|-- report/
|   `-- Windows Endpoint SOC Monitoring - Project Report.pdf
|-- screenshots/
|   |-- 01-lab-setup/
|   |-- 02-splunk-dashboard/
|   |-- 03-authentication-investigation/
|   `-- 04-powershell-investigation/
`-- spl/
    `-- Splunk_SOC_Investigation_Queries.txt


## 8. Key Learning Outcomes
- Windows endpoint log collection and analysis
- SIEM dashboard development
- Security event investigation
- Process execution analysis
- Detection query development using SPL
- Security investigation documentation

## 9. Project Evidence
### 9.1 Splunk SOC Dashboard
Screenshots of the Splunk monitoring dashboard and its event-monitoring panels are stored in `screenshots/02-splunk-dashboard/`.

### 9.2 Authentication Failure Investigation
Screenshots of failed logon events, account-lockout activity where available, and authentication investigation results are stored in `screenshots/03-authentication-investigation/`.

### 9.3 PowerShell Investigation
Screenshots of Sysmon process-creation events, PowerShell command-line analysis, and encoded PowerShell investigation results are stored in `screenshots/04-powershell-investigation/`.

## 10. Project Documentation
- Final Project Report:Windows Endpoint SOC Monitoring - Project Report.pdf
- SPL Investigation Queries:Splunk_SOC_Investigation_Queries.txt

The report documents the project, while the SPL query collection provides the searches used for monitoring and investigation.

## 11. Disclaimer
All testing was performed in a controlled lab environment for educational and defensive security purposes.
