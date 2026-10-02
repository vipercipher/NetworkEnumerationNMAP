# Service Enumeration

Once you know the open ports, identify the exact software and version on each. Versions are what you check against known vulnerabilities.

```bash
# Version detection on all ports
sudo nmap -p- -sV 192.168.1.10

# Faster: find open ports first, then version-scan only those
sudo nmap -p- --open -T4 192.168.1.10 -oA ports
sudo nmap -p 22,80,445 -sV -sC 192.168.1.10 -oA services

# OS detection
sudo nmap -O 192.168.1.10

# Aggressive: -sV + -O + default scripts + traceroute
sudo nmap -A 192.168.1.10
```

| Option | What it does |
| --- | --- |
| `-sV` | Detect service name and version |
| `--version-intensity 0-9` | How hard to probe (default 7) |
| `-O` | Guess the operating system |
| `-A` | `-sV`, `-O`, `-sC` and `--traceroute` together |
| `--stats-every=5s` | Progress updates on long scans |

## Manual banner grab

Nmap sometimes misses details a service sends on connect. Connect yourself and read the greeting:

```bash
nc -nv 192.168.1.10 25
```
