# Vulnerability Assessment & Exploitation of Metasploitable 2

## About the Project

This project was completed as part of the WSCube Tech Ethical Hacking + Internship Bootcamp.

The main purpose was to perform a vulnerability assessment of the intentionally vulnerable Metasploitable 2 machine using Kali Linux in an isolated VirtualBox lab environment.

## Lab Environment

| Component | Details |
|---|---|
| Virtualization | Oracle VirtualBox |
| Testing Machine | Kali Linux |
| Target Machine | Metasploitable 2 |
| Kali IP | 192.168.56.105 |
| Target IP | 192.168.56.102 |

## Tools Used

- Nmap
- Gobuster
- curl
- FTP Client
- smbclient

## Project Activities

- Initial network scanning and service identification
- FTP anonymous access enumeration
- HTTP and web directory enumeration
- PHP information exposure checks
- phpMyAdmin accessibility checks
- WebDAV configuration checks
- Samba / SMB share enumeration
- Selected vulnerability detection checks

## Key Findings

- Anonymous FTP access was enabled.
- Outdated FTP, Apache and Samba services were identified.
- PHP configuration information was publicly accessible.
- phpMyAdmin login page was reachable.
- WebDAV supported multiple HTTP methods.
- SMB anonymous share enumeration was possible.
- Nmap reported a vsftpd backdoor test result.
- UnrealIRCd backdoor indicators were detected.

Refer to the report for the exact validation results and limitations. Detection indicators do not automatically prove successful exploitation.

## Repository Structure

```text
WSCubeTech_Capstone/
├── README.md
├── Commands_Used.md
├── Report/
├── Scan-Results/
└── Evidence/
```

## Important Note

This project was performed in an isolated and intentionally vulnerable lab environment for educational purposes only. Testing systems without permission is not authorized.

## Author

**Taufique Shaikh**

WSCube Tech - Ethical Hacking + Internship Bootcamp

## Report

The complete project report is included in the Report folder.
