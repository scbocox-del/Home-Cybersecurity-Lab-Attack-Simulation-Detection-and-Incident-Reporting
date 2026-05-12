# Baseline Connectivity and Reconnaissance

## Objective

- The objective of this phase was to verify communication between the lab machines and perform basic reconnaissance from the red team machine against the blue team endpoint. This step helps confirm that the lab network is working before moving into more advanced attack simulation and detection testing.

## Lab Systems

| Machine | Role | IP Address |
|---|---|---|
| Sentinel | Windows 11 blue team endpoint | 192.168.56.103 |
| Raider | Kali Linux red team testing machine | 192.168.56.104 |

## Connectivity Test

| Test | Source | Destination | Result |
|---|---|---|---|
| Ping Raider from Sentinel | Sentinel | 192.168.56.104 | Successful |
| Ping Sentinel from Raider | Raider | 192.168.56.103 | Failed |

- Raider was unable to ping Sentinel, most likely because Sentinel's Windows Defender Firewall was blocking inbound ICMP traffic. Sentinel was able to ping Raider, which confirmed that both machines were connected to the same Host-only network.

## Reconnaissance Test
- nmap 192.168.56.103
  - The Nmap scan confirmed that Sentinel was online
  - Nmap reported that all 1000 scanned TCP ports were filtered. No open ports were discovered during this baseline scan.
- nmap -sn 192.168.56.0/24
  - The scan confirmed that both lab machines were connected to the same Host-only network. Sentinel and Raider were both visible on the 192.168.56.0/24 network, which means the lab network is ready for    controlled reconnaissance testing.
- nmap -sV 192.168.56.103
  - Nmap reported that all 1000 scanned TCP ports were filtered. This means Sentinel was reachable on the Host-only network, but Windows Defender Firewall or local filtering prevented Nmap from identifying open services.


## Results
- Document whether Sentinel was discovered.
- Document any open ports found.
- Add screenshot names or evidence notes.

## Red Team Notes
- From the attacker perspective, the scan confirmed that the target was active but did not reveal open services. Additional scanning or firewall changes would be needed before testing service-specific activity.

- From the red team perspective, the scan confirmed that the target was online but did not expose common services. Since no open ports were found, there were no obvious services available for follow-on enumeration during this baseline scan.

## Blue Team Notes
- The scan showed that Sentinel was reachable on the Host-only network, but Windows Defender Firewall filtered the scanned TCP ports. This means the system was online, but no common services were openly exposed during the scan.

- From the blue team perspective, this result shows that Sentinel was not openly exposing common TCP services during the scan. The filtered result is consistent with Windows Defender Firewall blocking or filtering inbound traffic.

## Screenshots
- nmap 192.168.56.103
- nmap -sn 192.168.56.0/24
- nmap -sV 192.168.56.103

## Issues Encountered
- Raider was unable to ping Sentinel because inbound ICMP traffic was likely blocked by Windows Defender Firewall. This did not prevent the reconnaissance scans from identifying that Sentinel was online, but it did show that Windows was filtering some inbound traffic by default.

## Lessons Learned
- This phase showed that basic connectivity was working between the virtual machines on the Host-only network. It also showed that Windows Defender Firewall can limit what an attacker sees during basic reconnaissance. Even though Sentinel was online, Nmap did not identify any open services because the scanned TCP ports were filtered.

## Next Steps
- The next step is to improve blue team visibility by enabling or reviewing Windows security logs, firewall logs, and later installing additional monitoring tools.
