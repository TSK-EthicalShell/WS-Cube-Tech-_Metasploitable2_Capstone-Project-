# WSCube Tech - Metasploitable 2 Capstone
## Commands Used

**Lab:** Kali Linux to Metasploitable 2  
**Kali IP:** 192.168.56.105  
**Target IP:** 192.168.56.102

> These commands were recorded during the practical lab. Results and limitations are documented in the project report. Run only in an authorized, isolated lab.

## 1. Initial Nmap Scan

```bash
nmap -sV -sC -A -T4 192.168.56.102
nmap -sV -sC -A -T4 -oA ~/metasploitable_initial_scan 192.168.56.102
```

Output files: .nmap, .gnmap, .xml

## 2. FTP Enumeration

```bash
nmap -p 21 -sV --script ftp-anon 192.168.56.102
ftp 192.168.56.102
nmap -p 21 -sV --script ftp-syst 192.168.56.102
```

## 3. HTTP and Web Enumeration

```bash
nmap -p 80,8180 -sV --script http-title,http-server-header 192.168.56.102
gobuster dir -u http://192.168.56.102/ -w /usr/share/wordlists/dirb/common.txt -t 10
```

## 4. PHP Information Page

```bash
curl -s -o /dev/null -w "HTTP Status: %{http_code}\nContent-Type: %{content_type}\nDownloaded Size: %{size_download} bytes\n" http://192.168.56.102/phpinfo.php

curl -s http://192.168.56.102/phpinfo.php | grep -E '<title>|PHP Version|Server API|Loaded Configuration File'
```

## 5. phpMyAdmin Checks

```bash
curl -s -o /dev/null -w "HTTP Status: %{http_code}\nContent-Type: %{content_type}\nRedirect: %{redirect_url}\n" http://192.168.56.102/phpMyAdmin/

curl -sI http://192.168.56.102/phpMyAdmin/
```

## 6. WebDAV Checks

```bash
nmap -p 80 --script http-methods --script-args http-methods.url-path=/dav/ 192.168.56.102
curl -i -X OPTIONS http://192.168.56.102/dav/
```

## 7. Samba / SMB Enumeration

```bash
smbclient -L //192.168.56.102 -N
smbclient //192.168.56.102/tmp -N
smbclient //192.168.56.102/opt -N -c 'ls'
nmap -p 445 --script smb-protocols,smb-security-mode 192.168.56.102
nmap -p 139,445 -sV --script smb-os-discovery 192.168.56.102
```

## 8. Vulnerability Detection Checks

```bash
nmap -p 21 -sV --script ftp-vsftpd-backdoor 192.168.56.102
nmap -p 21 --script ftp-vsftpd-backdoor -oN ~/metasploitable_ftp_backdoor.txt 192.168.56.102

nmap -p 445 --script smb-vuln-cve2007-2447 192.168.56.102

nmap -p 6667 -sV 192.168.56.102
nmap -sV --version-all -p 6667 192.168.56.102
nmap -p 6667 --script irc-unrealircd-backdoor 192.168.56.102
nmap -p 6667 --script irc-unrealircd-backdoor -oN ~/metasploitable_unrealircd_backdoor.txt 192.168.56.102
```

## Notes

- These commands are based on the saved terminal history.
- A command being recorded does not by itself prove successful exploitation.
- The Samba CVE check is recorded, but successful exploitation is not established here.
- The incomplete WebDAV PROPFIND command is intentionally omitted.
- Juice Shop commands are excluded because they belong to a separate project.
- Refer to the PDF report for the recorded findings and limitations.
-
