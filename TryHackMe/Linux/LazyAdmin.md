> Mon 04 Aug 2025
> al3xx
![[s11.jpeg|350]]
# LazyAdmin [Link](https://tryhackme.com/room/lazyadmin)

## 1. Reconnaissance
### TCP Scan
```bash
nmap -sC -sV -T4 $ip -oN tryhackme/lazy.txt
```

| port | service | version                         |
| ---- | ------- | ------------------------------- |
| 22   | ssh     | OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 |
| 80   | http    | Apache httpd 2.4.18 ((Ubuntu))  |

## 2. Enumeration
### Web enumeration
* Tried found subdirectories 
```bash
gobuster dir -u $ip -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 40 2>/dev/null
```
Resulte:
```Text
/content              (Status: 301) [Size: 316] [--> http://10.10.136.181/content/]
```

* Tried found subdirectories for */content*
```bash
gobuster dir -u $ip/content/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 40 2>/dev/null
```
Resulte:
```TEXT
/images
/js
/inc
/as
/_themes
/attachment
```

After visiting all this subdirectories these something interesting inside /content/inc/
```Text
/content/inc/mysql_backup/mysql_bakup_20191129023059-1.5.1.sql
/content/inc/cache/cache.db
```
the first file contains a user credentials 
```
Admin username: manager
dmin hashed password: 42f749ade7f9e195bf475f37a44cafcb
```

After decrypt password : `Password123`

## 3. Exploitation
- **Vulnerability found:**  
- **Exploit or method used:**  
- **Commands run:**  
- **Output or results:**  

## 4. Post-Exploitation
- **Actions taken:**  
- **Commands run:**  
- **Important files/data found:**  

## 5. Privilege Escalation
- **Techniques tried:**  
- **Commands run:**  
- **Vulnerabilities found:**  
- **Successful method:**  
- **Result:**  


## 6. Lessons Learned / Notes
- **What worked well:**  
- **What didn’t work:**  
- **Tools or techniques to remember:**  
- **Improvements for next time:**  