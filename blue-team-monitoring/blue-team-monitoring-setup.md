# Blue Team Monitoring Setup

## Objective

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
  - Open **Windows Defender Firewall** with Advanced Security. From the main firewall window, I selected **Properties** on the right side of the screen. In the firewall properties window, I selected the **Public Profile** tab because Public was the active network profile on Sentinel. Under the **Logging** section, I selected **Customize**.

In the logging settings, I changed **Log dropped packets** to **Yes** and left **Log successful connections** set to **No**. The default log file path was left unchanged:

`%systemroot%\system32\LogFiles\Firewall\pfirewall.log`

Dropped packet logging was enabled so blocked traffic from Raider can be recorded during future reconnaissance and attack simulation testing. This will help show when Sentinel filters or blocks inbound traffic.
## Screenshots

- Windows Event Viewer
- Windows Defender Firewall
- Firewall Logging Settings


## Issues Encountered

## Lessons Learned

## Next Steps
