# Using NMAP Scripts (NSE)

The Nmap Scripting Engine runs Lua scripts that pull extra detail from services: page titles, SMB shares, SSL certificates, known weaknesses.

```bash
# Default safe set (same as --script=default)
sudo nmap -sC -sV 192.168.1.10

# A whole category
sudo nmap --script vuln 192.168.1.10

# Specific scripts on specific ports
sudo nmap -p 80 --script http-title,http-headers 192.168.1.10
sudo nmap -p 445 --script smb-os-discovery 192.168.1.10
sudo nmap -p 443 --script ssl-cert,ssl-enum-ciphers 192.168.1.10

# Combine categories and wildcards
sudo nmap -p 80 --script "http-* and safe" 192.168.1.10

# Read what a script does before running it
nmap --script-help http-title

# Find scripts by name (Linux path)
ls /usr/share/nmap/scripts/ | grep smb

# Refresh the script database after adding scripts
sudo nmap --script-updatedb
```

## Categories

| Category | What's in it |
| --- | --- |
| `default` | Safe, useful scripts run by `-sC` |
| `safe` | Won't crash or disrupt services |
| `discovery` | Learns more about the network and services |
| `version` | Extends `-sV` |
| `vuln` | Checks for known vulnerabilities |
| `auth` | Checks authentication and credentials |
| `brute` | Password guessing; noisy, can lock accounts |
| `intrusive` | May disrupt the target |
| `exploit` / `dos` | Actively attacks; lab use only |

Stick to `default`, `safe`, `discovery` and `version` unless you have explicit permission for more.

Full script list: [nmap.org/nsedoc](https://nmap.org/nsedoc/)
