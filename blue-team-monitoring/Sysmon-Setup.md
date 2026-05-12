# Sysmon Setup

## Objective
- The objective of this phase is to install and configure Sysmon on Sentinel to improve endpoint visibility. Sysmon provides more detailed logging than the default Windows Security logs, including process creation, network connections, file activity, and other system events that can support blue team investigation.

## Download Sysmon

- To download Sysmon:
  - Downloaded Sysmon from Microsoft Learn.
  - Installed the Sysinternals Suite from the Microsoft Store.
  - Confirmed Sysmon was available on Sentinel.

## Download Sysmon Configuration

- To download the Sysmon configuration:
  - Downloaded the configuration file from the **SwiftOnSecurity/sysmon-config** GitHub repository.
  - Extracted the configuration folder to:
    `C:\temp`
  - Confirmed the Sysmon configuration file was available at:
    `C:\temp\sysmon-config-master\sysmonconfig-export.xml`

## Install Sysmon

- To install Sysmon:
  - Opened Command Prompt as Administrator.
  - Changed directories to:
    `C:\temp\sysmon-config-master`
  - Ran the Sysmon install command:
    ```cmd
    sysmon -accepteula -i sysmonconfig-export.xml
    ```
- Sysmon was installed using a prebuilt configuration file so Sentinel can collect more detailed endpoint events during future testing.
  
## Verify Sysmon Installation

Sysmon was verified in Event Viewer to confirm that it was installed correctly and recording endpoint events on Sentinel.

- To verify Sysmon installation:
  - Opened **Event Viewer**.
  - In the left panel, expanded **Applications and Services Logs**.
  - Expanded **Microsoft**.
  - Expanded **Windows**.
  - Expanded **Sysmon**.
  - Selected **Operational**.
  - Confirmed that Sysmon logs were present.

Sysmon is now recording endpoint activity on Sentinel and can be used during future attack simulations to review process creation, network activity, and other system events.

## Basic Sysmon Event Test

A basic test was completed to confirm that Sysmon was recording endpoint activity after installation.

- To generate test activity:
  - Opened Command Prompt on Sentinel.
  - Ran `whoami`.
  - Ran `ipconfig`.
  - Reviewed the Sysmon Operational log in Event Viewer.

Sysmon recorded endpoint activity after installation, confirming that it is ready to support future monitoring and detection testing.

## Screenshots

- Download Sysmon
- Sysmon Configuration
- Install Sysmon
- Sysmon Logs


## Issues Encountered

- No major issues were encountered during Sysmon installation.
  
## Lessons Learned

- I learned that Sysmon adds more detailed endpoint visibility than the default Windows logs. I also learned the value of using a trusted Sysmon configuration file, because the SwiftOnSecurity configuration helps filter and organize the types of events Sysmon records. This setup prepares Sentinel for future attack simulations because Sysmon logs can now be reviewed locally in Event Viewer and later forwarded into tools like Wazuh or Splunk for centralized monitoring.

## Next Steps
- Set up Wazuh
