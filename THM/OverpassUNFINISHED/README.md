# Overpass TryHackMe

> David 13/04/2022

----------------------------

## Encryption type - ROT13

  <!--Yeah right, just because the Romans used it doesn't make it military grade, change this?-->
  Implies ceaser cypher

# Ports open
```
22, 80
```

# Gobuster results
```
gobuster dir -u http://10.10.135.145/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt

===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.135.145/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2022/04/13 16:25:42 Starting gobuster in directory enumeration mode
===============================================================
/img                  (Status: 301) [Size: 0] [--> img/]
/downloads            (Status: 301) [Size: 0] [--> downloads/]
/aboutus              (Status: 301) [Size: 0] [--> aboutus/]  
/admin                (Status: 301) [Size: 42] [--> /admin/]  
/css                  (Status: 301) [Size: 0] [--> css/]      
Progress: 5655 / 207644 (2.72%)                              ^C
[!] Keyboard interrupt detected, terminating.                                                                       
                                                                                                                    
===============================================================                                                     
2022/04/13 16:26:11 Finished                                                                                        
===============================================================  
```