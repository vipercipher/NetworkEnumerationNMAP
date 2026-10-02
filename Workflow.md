# Typical Workflow and Quick Reference

Run these in order against an authorised range, saving each step.

1. Find live hosts and save their IPs:
   ```bash
   sudo nmap -sn 192.168.1.0/24 -oA 01_hosts | grep for | cut -d" " -f5 > live.txt
   ```
2. Quick port scan of the live hosts:
   ```bash
   sudo nmap -iL live.txt --top-ports=1000 --open -T4 -oA 02_quick
   ```
3. Full TCP scan of interesting hosts:
   ```bash
   sudo nmap -p- --open -T4 192.168.1.10 -oA 03_full
   ```
4. Versions and default scripts on the open ports:
   ```bash
   sudo nmap -p <ports> -sV -sC 192.168.1.10 -oA 04_services
   ```
5. Targeted scripts per service (HTTP, SMB, SSL):
   ```bash
   sudo nmap -p 80 --script "http-* and safe" 192.168.1.10 -oA 05_http
   ```
6. Short UDP check:
   ```bash
   sudo nmap -sU --top-ports=50 192.168.1.10 -oA 06_udp
   ```
7. Build a report:
   ```bash
   xsltproc 04_services.xml -o report.html
   ```

## Quick reference

| Goal | Command |
| --- | --- |
| Live hosts | `nmap -sn <range>` |
| Skip ping | `nmap -Pn <ip>` |
| All TCP ports | `nmap -p- <ip>` |
| Top N ports | `nmap --top-ports=N <ip>` |
| UDP | `nmap -sU <ip>` |
| Versions | `nmap -sV <ip>` |
| OS | `nmap -O <ip>` |
| Default scripts | `nmap -sC <ip>` |
| Everything | `nmap -A <ip>` |
| Save all formats | `-oA <name>` |
| Faster | `-T4` or `--min-rate 300` |
| Only open ports | `--open` |

Full reference: [Nmap reference guide](https://nmap.org/book/man.html)
