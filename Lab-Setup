# Lab Environment

## Objective

The objective of this step was to set up the base virtual machines for the cybersecurity home lab. 
This project uses a Windows 11 VM as the blue team endpoint and a Kali Linux VM as the red team testing machine.

## Virtual Machines

| VM Name | Operating System | Role | CPU | RAM | Storage |
|---|---|---|---|---|---|
| Sentinel | Windows 11 | Blue team endpoint | 4 CPUs | 5000 MB | 80 GB |
| Raider | Kali Linux | Red team testing machine | 4 CPUs | 5000 MB | 20 GB |

## Windows VM Setup

The Windows 11 VM was created first and named **Sentinel**. 
This system will be used as the blue team endpoint for monitoring, log collection, and later attack simulation testing.

## Steps Completed

- Downloaded the Windows ISO.
- Created a new virtual machine in VirtualBox.
- Named the VM **Sentinel**.
- Mounted the Windows ISO during VM creation.
- Verified the operating system type and version.
- Configured the VM user account and password.
- Assigned 4 CPUs, 5000 MB of RAM, and 80 GB of storage.
- Booted the VM successfully after installation.

## Kali Linux VM Setup

The Kali Linux VM was created and named **Raider**. 
This system will be used as the red team testing machine for reconnaissance and controlled attack simulation inside the lab.

## Steps Completed

- Downloaded the Kali Linux ISO from kali.org.
- Created a new virtual machine in VirtualBox.
- Named the VM **Raider**.
- Mounted the Kali Linux ISO during VM creation.
- Selected Debian as the operating system type and Debian 64-bit as the version.
- Started the VM and selected the graphical installation option.
- Configured the language, country, keyboard layout, hostname, domain name, user account, password, and clock.
- Set the hostname as **Raider**.
- Set the domain name as **lab.local**.
- Created the user account **raider**.
- Selected guided disk partitioning using the entire disk.
- Selected the Xfce desktop environment.
- Selected the top 10 and default Kali tool collections.
- Installed the GRUB boot loader.
- Booted Kali Linux successfully after installation.

## Initial Network Setup

During initial setup, both VMs were configured using VirtualBox NAT networking.

| Machine | IPv4 Address | Subnet Mask | Default Gateway | Network Mode |
|---|---|---|---|---|
| Sentinel | 10.0.2.15 | 255.255.255.0 | 10.0.2.2 | NAT |
| Raider | 10.0.2.15 | 255.255.255.0 | 10.0.2.2 | NAT |

Both machines received the same NAT IP address because VirtualBox NAT places each VM behind its own isolated NAT network.
This was acceptable for initial setup, but it was not ideal for attack simulation because the VMs needed to communicate directly with each other.

## Updated Network Setup

To correct the networking issue, both VMs were configured with a second adapter using a Host-only Adapter. Adapter 1 was left on NAT for internet access, and Adapter 2 was added for private lab communication.

| Machine | Adapter | IPv4 Address | Network Mode | Purpose |
|---|---|---|---|---|
| Sentinel | Adapter 1 | 10.0.2.15 | NAT | Internet access |
| Sentinel | Adapter 2 | 192.168.56.103 | Host-only Adapter | Private lab communication |
| Raider | Adapter 1 | No IPv4 assigned at time of screenshot | NAT | Internet access |
| Raider | Adapter 2 | 192.168.56.104 | Host-only Adapter | Private lab communication |

The Host-only Adapter allows **Sentinel** and **Raider** to communicate directly on the same private lab network while keeping the NAT adapter available for internet access.

## Connectivity Test

After the network correction, connectivity was tested between the two virtual machines. 
Windows was able to successfully ping Kali using the Host-only network address.

| Test | Source | Destination | Result |
|---|---|---|---|
| Ping test | Sentinel | Raider, 192.168.56.104 | Successful |
| Ping test | Raider | Sentinel, 192.168.56.103 | Blocked by Windows Firewall |

Kali was not able to ping Windows because Windows Defender Firewall blocks inbound ICMP echo requests by default. 
This confirms that the VMs are on the same Host-only network, but Windows is restricting inbound ping traffic.

## Screenshots

The following screenshots were added to the repository as evidence of the VM setup process:

- Windows running
- Windows ipconfig 
- Kali running
- Kali ifconfig
- Updated Windows ipconfig
- Updated Kali ifconfig
- Ping from Windows to Kali

## Issues Encountered

During initial setup, both the Windows and Kali VMs displayed the same IPv4 address because they were both configured with VirtualBox NAT networking. 
This created confusion because both machines showed `10.0.2.15`, but this happened because each VM was behind its own separate NAT network.

This issue was corrected by adding a second network adapter to each VM and setting Adapter 2 to Host-only Adapter. 
This gave each VM a separate private lab IP address on the `192.168.56.0/24` network.

## Lessons Learned

During this setup phase, I learned that VirtualBox NAT networking is useful for basic internet access during installation, but it is not the best option by itself for a cybersecurity lab where VMs need to communicate with each other.
Using both NAT and Host-only Adapter provides a better lab setup. NAT allows the VMs to reach the internet for updates and downloads, while the Host-only Adapter creates an isolated private network for attack simulation, detection testing, and log analysis.

## Corrections

To correct the networking issue, both virtual machines were fully shut down. In VirtualBox, I right-clicked **Sentinel**, opened **Settings**, switched to **Expert** mode, and went to the **Network** section. Under **Adapter 2**, I enabled the network adapter and changed the **Attached to** dropdown to **Host-only Adapter**.
This created a private lab network connection while keeping the NAT adapter available for internet access. I repeated the same configuration change for **Raider**. Both machines were then booted again, and the network settings were verified.
This correction allows **Sentinel** and **Raider** to communicate directly on the isolated Host-only network while still maintaining internet access through NAT.
