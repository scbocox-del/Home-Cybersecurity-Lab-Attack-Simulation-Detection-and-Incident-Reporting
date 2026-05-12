# Blue Team Monitoring Setup

## Objective

- The objective of this phase is to prepare Sentinel for basic blue team monitoring before running more advanced attack simulations. This includes reviewing Windows Security logs, confirming Windows Defender Firewall status, enabling firewall logging, and verifying that blocked traffic from Raider can be recorded in the Windows firewall log.

## Windows Security Logs

- Windows Event Viewer was reviewed on Sentinel to confirm that security events were being recorded.

  - The Security log contained multiple events, including Event ID 4624, which represents a successful logon. This confirms that 
Sentinel is generating Windows security audit logs that can be used later for monitoring, investigation, and detection testing.

## Windows Defender Firewall Status

- Windows Defender Firewall was checked on Sentinel. The firewall was enabled for the Domain, Private, and Public network profiles. The active profile was Public network.

  - Windows applies stricter rules to public networks by default. This likely explains why Raider was unable to ping Sentinel during the earlier connectivity test.

## Firewall Logging
- Windows Defender Firewall logging was configured on Sentinel. Since the active network profile was Public, the Public Profile logging settings were updated.

- To access the firewall logging settings:
  - Open **Windows Defender Firewall** click Advanced Security.
  - Select **Properties** on the right side of the screen.
  - Select the **Public Profile** tab.
  - Under the **Logging** section, select **Customize**.
  - In the logging settings, change **Log dropped packets** to **Yes** and leave everything else the same.

- Dropped packet logging was enabled so blocked traffic from Raider can be recorded during future reconnaissance and attack simulation testing. This will help show when Sentinel filters or blocks inbound traffic.

## Firewall Log Verification

- Firewall logging was tested after dropped packet logging was enabled on Sentinel. A Nmap scan was run from Raider against Sentinel to generate traffic that could be reviewed in the Windows firewall log.

- To generate traffic:
  - Ran `nmap -Pn -p 135,139,445 192.168.56.103` from Raider.
  - The scan targeted common Windows ports on Sentinel.
  - Raider's Host-only IP address was `192.168.56.105`.
  - Sentinel's Host-only IP address was `192.168.56.103`.

- To review the firewall log:
  - Opened Notepad as administrator on Sentinel.
  - Opened `C:\Windows\System32\LogFiles\Firewall\pfirewall.log`.
  - Searched for Raider's IP address, `192.168.56.105`.
  - Confirmed dropped TCP traffic from Raider to Sentinel.

The firewall log showed dropped TCP traffic from `192.168.56.105` to `192.168.56.103` on ports `135`, `139`, and `445`. This confirmed that Windows Defender Firewall logging is working.

## Screenshots

- Windows Event Viewer
- Windows Defender Firewall
- Firewall Logging Settings
- Firewall Log

## Issues Encountered

- While reviewing the Windows firewall log, the `pfirewall.log` file could not be opened with normal user permissions. This happened because the log is stored in a protected Windows system directory. To resolve this, Notepad was opened as administrator, and the log file was opened from `C:\Windows\System32\LogFiles\Firewall`.

- Another issue encountered was Raider's Host-only adapter losing its IPv4 address. The adapter was active, but it did not show a `192.168.56.104` address at first. This was corrected by running `sudo dhcpcd eth1` in Raider, which gave Raider the Host-only IP address `192.168.56.105`.

## Lessons Learned

- Windows Event Viewer and Windows Defender Firewall provide local monitoring before adding tools like Sysmon, Wazuh, or Splunk. Sentinel was recording Security events, including successful logon events, and Windows Defender Firewall was active on all network profiles.

- I also learned that firewall logging can provide useful evidence of blocked traffic. After enabling dropped packet logging, Sentinel recorded dropped TCP traffic from Raider to Sentinel on ports 135, 139, and 445. This helped connect red team scanning activity to blue team evidence on the Windows endpoint.

## Next Steps

- The next step is to install and configure Sysmon on Sentinel. 
