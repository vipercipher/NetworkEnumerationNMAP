# Host Discovery

Find which machines are online before scanning ports. `-sn` checks liveness only, with no port scan.

Document every scan; saved results can be compared and used in reports later.

## Scan a network range

```bash
sudo nmap -sn 192.168.1.0/24 -oA tnet | grep for | cut -d" " -f5
```

| Option | Meaning |
| --- | --- |
| `192.168.1.0/24` | Target network range (CIDR) |
| `-sn` | Disables port scanning |
| `-oA tnet` | Saves results in all formats, named `tnet.*` |
| `grep for \| cut -d" " -f5` | Prints only the live IP addresses |

> This only finds hosts whose firewall allows the probe.

## Scan an IP list

```bash
sudo nmap -sn -oA hosts -iL hosts.lst | grep for | cut -d" " -f5
```

`-iL` reads targets from `hosts.lst` (one IP or range per line).

## Scan multiple IPs

```bash
sudo nmap -sn -oA tnet 192.168.1.1,192.168.1.10,192.168.1.20 | grep for | cut -d" " -f5
# or a range
sudo nmap -sn -oA tnet 192.168.1.1-50 | grep for | cut -d" " -f5
```

## Forcing ICMP echo requests

On a local network, run as root, Nmap uses ARP by default (fastest, not blocked by host firewalls). To force ICMP echo and see why each host is up:

```bash
sudo nmap -sn -PE --disable-arp-ping --packet-trace --reason 192.168.1.10
```

## Discovery options

| Option | What it does |
| --- | --- |
| `-sn` | Host discovery only, no port scan |
| `-PE` | ICMP echo request (ping) |
| `-PS22,80,443` | TCP SYN probe to these ports |
| `-PA80` | TCP ACK probe |
| `-PU53` | UDP probe |
| `--disable-arp-ping` | Skip ARP, use the probes you chose |
| `--packet-trace` | Show every packet sent and received |
| `--reason` | Show why a host is marked up or down |
| `-Pn` | Skip discovery, treat every host as up |

If a host blocks ping it looks offline. Use `-Pn` when port-scanning a host you know is there.
