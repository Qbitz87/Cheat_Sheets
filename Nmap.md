# Nmap Cheat Sheet

* **Fast Initial Scan:** `nmap -T4 -F <target>`
* **Basic Network Sweep:** `nmap -sn 192.168.1.0/24`
* **Standard Service Scan:** `nmap -sV -sC <target>`
* **Aggressive Full Scan:** `nmap -A -p- -T4 <target>`
* **UDP Scan (Top Ports):** `nmap -sU --top-ports 200 <target>`
* **Scan with Vuln Scripts:** `nmap -sV --script=vuln <target>`

## Target Specification

| SWITCH | EXAMPLE                    | DESCRIPTION                     |
| :----- | :------------------------- | :------------------------------ |
| (none) | `nmap 192.168.1.1`         | Scan single IP                  |
| (none) | `nmap 192.168.1.0/24`      | Scan CIDR block                 |
| (none) | `nmap 192.168.1.1-100`     | Scan IP range                   |
| `-iL`  | `nmap -iL targets.txt`     | Scan targets from file          |
| `-iR`  | `nmap -iR 10`              | Scan 10 random hosts            |

## Host Discovery (Ping Scans)

| SWITCH | EXAMPLE                  | DESCRIPTION                     |
| :----- | :----------------------- | :------------------------------ |
| `-sn`  | `nmap 192.168.1.0/24 -sn`| Ping scan only (no port scan)   |
| `-Pn`  | `nmap 192.168.1.1 -Pn`   | No ping scan (assume host up)   |
| `-n`   | `nmap 192.168.1.1 -n`    | No DNS resolution               |
| `-PS`  | `nmap 192.168.1.1 -PS80` | TCP SYN Ping on port(s)         |
| `-PA`  | `nmap 192.168.1.1 -PA22` | TCP ACK Ping on port(s)         |
| `-PR`  | `nmap 192.168.1.0/24 -PR`| ARP Ping on local network       |

## Scan Techniques

| SWITCH | EXAMPLE                | DESCRIPTION                     |
| :----- | :--------------------- | :------------------------------ |
| `-sS`  | `nmap 192.168.1.1 -sS` | TCP SYN Scan (Stealth, Default) |
| `-sT`  | `nmap 192.168.1.1 -sT` | TCP Connect Scan (No root)      |
| `-sU`  | `nmap 192.168.1.1 -sU` | UDP Scan (Slow)                 |
| `-sA`  | `nmap 192.168.1.1 -sA` | TCP ACK Scan (Firewall check)   |

## Port Specification

| SWITCH       | EXAMPLE                       | DESCRIPTION                     |
| :----------- | :---------------------------- | :------------------------------ |
| `-p`         | `nmap 192.168.1.1 -p 80,443`  | Scan specific ports             |
| `-p`         | `nmap 192.168.1.1 -p 1-1000`  | Scan port range                 |
| `-p-`        | `nmap 192.168.1.1 -p-`        | Scan all ports (1-65535)        |
| `-F`         | `nmap 192.168.1.1 -F`         | Fast scan (Top 100 ports)       |
| `--top-ports`| `nmap 192.168.1.1 --top-ports 1000`| Scan top X ports           |

## Service/Version & OS Detection

| SWITCH | EXAMPLE                | DESCRIPTION                                      |
| :----- | :--------------------- | :----------------------------------------------- |
| `-sV`  | `nmap 192.168.1.1 -sV` | Service/Version detection                        |
| `-O`   | `nmap 192.168.1.1 -O`  | OS detection                                     |
| `-A`   | `nmap 192.168.1.1 -A`  | Aggressive: Enables `-sV`, `-O`, Script Scan (`-sC`), Traceroute |

## Timing & Performance

| SWITCH | EXAMPLE                | DESCRIPTION                     |
| :----- | :--------------------- | :------------------------------ |
| `-T<0-5>`| `nmap 192.168.1.1 -T4` | Set timing template (0=paranoid, 1=sneaky, 2=polite, 3=normal, 4=aggressive, 5=insane) |
| `-T4`  | (Commonly Used)        | Aggressive (Fast, assumes good network) |
| `-T2`  | (Useful for IDS Ev.)   | Polite (Slow, less noisy)       |

## NSE Scripts (Nmap Scripting Engine)

| SWITCH        | EXAMPLE                                  | DESCRIPTION                             |
| :------------ | :--------------------------------------- | :-------------------------------------- |
| `-sC`         | `nmap 192.168.1.1 -sC`                   | Run default safe scripts (equiv `--script default`) |
| `--script`    | `nmap 192.168.1.1 --script=vuln`       | Run scripts by category (e.g., `vuln`, `auth`, `discovery`) |
| `--script`    | `nmap 192.168.1.1 --script=http-title` | Run specific script(s)                  |
| `--script`    | `nmap 192.168.1.1 --script "http*"`    | Run scripts matching wildcard           |
| `--script-args`| `nmap ... --script-args user=admin`    | Provide arguments to scripts            |

## Firewall / IDS Evasion

| SWITCH | EXAMPLE                           | DESCRIPTION                     |
| :----- | :-------------------------------- | :------------------------------ |
| `-f`   | `nmap 192.168.1.1 -f`             | Fragment packets (smaller MTU)  |
| `-D`   | `nmap -D RND:3,ME 192.168.1.1`    | Cloak scan with decoys (ME=you) |
| `-g`/`--source-port` | `nmap -g 53 192.168.1.1` | Use specific source port (e.g., 53 for DNS) |

## Output

| SWITCH | EXAMPLE                       | DESCRIPTION                             |
| :----- | :---------------------------- | :-------------------------------------- |
| `-oN`  | `nmap ... -oN scan.nmap`      | Normal output format                    |
| `-oG`  | `nmap ... -oG scan.gnmap`     | Grepable output format                  |
| `-oX`  | `nmap ... -oX scan.xml`       | XML output format                       |
| `-oA`  | `nmap ... -oA scan_results`   | Output in all 3 major formats           |
| `-v`   | `nmap ... -v`                 | Increase verbosity (`-vv`, `-vvv`)      |
| `--open`| `nmap ... --open`             | Show only open (or possibly open) ports |
