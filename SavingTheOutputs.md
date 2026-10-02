# Saving the Outputs

Save every scan. Use `-oA` to get all three formats at once for comparing and reporting later.

| Option | Format | File | Good for |
| --- | --- | --- | --- |
| `-oN name` | Normal | `name.nmap` | Reading; same as screen output |
| `-oG name` | Grepable | `name.gnmap` | `grep`, `awk`, quick filtering |
| `-oX name` | XML | `name.xml` | Tools, reports, importing |
| `-oA name` | All three | all of the above | Default habit |

```bash
sudo nmap -p- -sV 192.168.1.10 -oA target_full

# List open ports from the grepable file
grep "open" target_full.gnmap

# Turn the XML into an HTML report (needs xsltproc)
xsltproc target_full.xml -o target_full.html
```

Install `xsltproc` with `sudo apt install xsltproc` on Linux, then open the `.html` file in a browser for a readable report.
