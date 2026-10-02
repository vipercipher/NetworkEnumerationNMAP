# Network Enumeration with NMAP

Notes and commands for enumerating hosts, ports and services with Nmap.

> **Only scan networks you own or have written permission to test** (home network, VM lab, Hack The Box, TryHackMe).

- **HOST ENUMERATION**
    - [Host Discovery - ICMP Echo Requests (Most Effective Method)](HostDiscovery.md)
    - [Host and Port Scanning](HostAndPortScanning.md)
    - [Saving the Outputs](SavingTheOutputs.md)
    - [Service Enumeration](ServiceEnumeration.md)
    - [Using NMAP Scripts](NmapScripts.md)
    - [Typical Workflow and Quick Reference](Workflow.md)

## Setup

| OS | Install |
| --- | --- |
| Windows | Installer from [nmap.org/download](https://nmap.org/download) (includes Npcap) |
| macOS | `brew install nmap` |
| Debian / Ubuntu / Kali | `sudo apt install nmap` |

Check it works: `nmap --version`

- **Run as root/admin.** SYN scans, OS detection and ARP discovery need raw packets. Use `sudo` on Linux/macOS or an Administrator terminal on Windows.
- **Windows:** `grep` and `cut` aren't available in Command Prompt. Drop everything after the `|`, or use WSL / Git Bash.
- **Find your range:** run `ip a`, `ifconfig` or `ipconfig`. IP `192.168.1.23` with mask `255.255.255.0` means range `192.168.1.0/24`.

Examples use `192.168.1.0/24` as the network and `192.168.1.10` as the target. Replace them with your own.
