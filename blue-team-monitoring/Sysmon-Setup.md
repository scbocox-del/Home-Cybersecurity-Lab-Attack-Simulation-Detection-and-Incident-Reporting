# Sysmon Setup

## Objective
- Explain that Sysmon is being added to improve endpoint visibility on Sentinel.

## Download Sysmon
- Download Sysmon from Microsoft Sysinternals.
- Save or extract it on Sentinel.

## Download Sysmon Configuration
- Download a trusted Sysmon configuration file.
- Save it in the same folder as Sysmon.

## Install Sysmon
- Open PowerShell or Command Prompt as Administrator.
- Navigate to the Sysmon folder.
- Install Sysmon using the configuration file.

## Verify Sysmon Installation
- Open Event Viewer.
- Go to Applications and Services Logs.
- Go to Microsoft.
- Go to Windows.
- Go to Sysmon.
- Open Operational.
- Confirm Sysmon events are being recorded.

## Screenshots
- Sysmon folder/files
- Sysmon installation command
- Sysmon Operational log in Event Viewer

## Issues Encountered
- Document any install errors or permission issues.

## Lessons Learned
- Explain what Sysmon adds compared to regular Windows logs.

## Next Steps
- Use Sysmon logs during future attack simulations.
- Later forward Sysmon logs to Wazuh or Splunk.
