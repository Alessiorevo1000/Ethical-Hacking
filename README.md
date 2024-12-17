# Ethical-Hacking

## Report Overview:
This project explores an ethical hacking scenario involving enumeration, web service exploitation, privilege escalation, and persistence. The target is a vulnerable server referred to as *Dragonbol*. Various penetration testing techniques and tools, such as **nmap**, **gobuster**, **sqlmap**, and **Burp Suite**, were used to gain access to the system and escalate privileges to root.

---

## Table of Contents:
1. [Enumeration](#enumeration)  
2. [Web Service Exploitation](#web-service-exploitation)  
3. [Local Access & User Enumeration](#local-access--user-enumeration)  
4. [Privilege Escalation](#privilege-escalation)  
5. [Persistence](#persistence)  
6. [Tools Used](#tools-used)  
7. [Conclusion](#conclusion)

---

## Enumeration

### Network Scanning:
- Initial **nmap** scans revealed services running on:
  - **Port 80**: Web server  
  - **Port 22**: SSH  
  - **Port 110 & 995**: POP3 services  
- Telnet and DNS enumeration provided minimal information.

### Key Command:
```bash
nmap -P 10.0.2.0/24
```

---

## Web Service Exploitation

### Tools Used:
- **Gobuster**: Directory brute-forcing revealed `about.php`, `register.php`, and `index_beta.php`.  
- **SQL Injection**: `index_beta.php` was vulnerable to SQL Injection.

### SQL Injection Example:
```bash
sqlmap -r beta_req.txt -p category --level 5 --risk 3
```
This enabled retrieval of usernames and hashed passwords from the `saiyans` database table.

---

## Local Access & User Enumeration

### SSH Access:
- Credentials for `ericadminssj24` were obtained:
  - **Username**: `ericadminssj24`  
  - **Password**: `dragonslayer`  

### Post-SSH Enumeration:
- **LinPEAS** script revealed local vulnerabilities and user permissions.  
- Exploited access to `/etc/shadow` using `od` command.

---

## Privilege Escalation

### Steps to Root Access:
1. Exploited `emme_admin`'s `.bash_history` to gain **emme_admin** access.  
2. Analyzed a vulnerable C program (`Stupidor`) to escalate privileges to **root**.  

### Stupidor Exploit:
The `system()` function vulnerability was exploited using a crafted username containing the `&` character.

---

## Persistence

### Root Access Persistence:
- Modified `/etc/cron.d/popularity-contest` to create a reverse shell to attacker’s machine every minute.

### Emme_admin Access Persistence:
- Added reverse shell execution to `.bashrc` and `motd.legal-displayed`.

---

## Tools Used
- **nmap**: Network scanning  
- **gobuster**: Web enumeration  
- **sqlmap**: SQL Injection automation  
- **ZAP / Burp Suite**: Web vulnerability testing  
- **Hydra**: Brute force attacks  
- **LinPEAS**: Privilege escalation script  
- **Hashcat**: Password cracking  
- **Netcat**: Reverse shells  

---

## Conclusion
This report outlines the successful exploitation of a vulnerable system through systematic enumeration, web service exploitation, and privilege escalation techniques. The vulnerabilities found demonstrate the importance of secure coding practices, particularly input validation and secure permissions.

---

## Disclaimer
This project was conducted for educational purposes as part of an Ethical Hacking assignment. Unauthorized testing on systems you do not own is illegal.

---

Feel free to modify or add specific code snippets, images, or references! 🚀
