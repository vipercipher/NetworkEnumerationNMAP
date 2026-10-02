# Host and Port Scanning

By default Nmap scans the top 1,000 TCP ports, using a SYN scan as root or a connect scan without root.

```bash
# Default scan of one host
sudo nmap 192.168.1.10

# Top 10 ports, then all 65,535 ports
sudo nmap --top-ports=10 192.168.1.10
sudo nmap -p- 192.168.1.10

# Specific ports or a range
sudo nmap -p 22,80,443 192.168.1.10
sudo nmap -p 1-1024 192.168.1.10

# UDP scan (slow; keep the port list short)
sudo nmap -sU --top-ports=100 192.168.1.10

# Show only open ports
sudo nmap -p- --open 192.168.1.10
```

## Port states

| State | Meaning |
| --- | --- |
| `open` | A service is listening |
| `closed` | Host replied (RST), nothing listening |
| `filtered` | No reply or ICMP error; a firewall is likely dropping it |
| `unfiltered` | Reachable, but open/closed unknown (ACK scan only) |
| `open\|filtered` | No reply; common with UDP |
| `closed\|filtered` | Can't tell (IP ID idle scan only) |

## Scan types

| Option | Scan | Notes |
| --- | --- | --- |
| `-sS` | TCP SYN (half-open) | Default as root; fast, quieter |
| `-sT` | TCP connect | Default without root; full handshake, logged more often |
| `-sU` | UDP | Slow; finds DNS, SNMP, DHCP |
| `-sA` | TCP ACK | Maps firewall rules, not open ports |

## Speed and visibility

| Option | What it does |
| --- | --- |
| `-T0` … `-T5` | Timing templates, slowest to fastest (`-T3` default, `-T4` fine for labs) |
| `--min-rate 300` | Send at least 300 packets per second |
| `-v` / `-vv` | Show open ports as they're found |
| `--stats-every=10s` | Print progress every 10 seconds |
| `--packet-trace` | Show every packet |
| `--reason` | Show why a port has its state |
