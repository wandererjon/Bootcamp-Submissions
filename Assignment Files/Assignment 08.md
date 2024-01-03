**Phase 1**

```bash
sysadmin@UbuntuDesktop:~$ fping -g 15.199.95.91/28
15.199.95.81 is unreachable
15.199.95.82 is unreachable
15.199.95.83 is unreachable
15.199.95.84 is unreachable
15.199.95.85 is unreachable
15.199.95.86 is unreachable
15.199.95.87 is unreachable
15.199.95.88 is unreachable
15.199.95.89 is unreachable
15.199.95.90 is unreachable
15.199.95.91 is unreachable
15.199.95.92 is unreachable
15.199.95.93 is unreachable
15.199.95.94 is unreachable

sysadmin@UbuntuDesktop:~$ fping -g 15.199.94.91/28
15.199.94.81 is unreachable
15.199.94.82 is unreachable
15.199.94.83 is unreachable
15.199.94.84 is unreachable
15.199.94.85 is unreachable
15.199.94.86 is unreachable
15.199.94.87 is unreachable
15.199.94.88 is unreachable
15.199.94.89 is unreachable
15.199.94.90 is unreachable
15.199.94.91 is unreachable
15.199.94.92 is unreachable
15.199.94.93 is unreachable
15.199.94.94 is unreachable

sysadmin@UbuntuDesktop:~$ fping -g 11.199.158.91/28
11.199.158.81 is unreachable
11.199.158.82 is unreachable
11.199.158.83 is unreachable
11.199.158.84 is unreachable
11.199.158.85 is unreachable
11.199.158.86 is unreachable
11.199.158.87 is unreachable
11.199.158.88 is unreachable
11.199.158.89 is unreachable
11.199.158.90 is unreachable
11.199.158.91 is unreachable
11.199.158.92 is unreachable
11.199.158.93 is unreachable
11.199.158.94 is unreachable

sysadmin@UbuntuDesktop:~$ fping -g 167.172.144.11/32
167.172.144.11 is alive

sysadmin@UbuntuDesktop:~$ fping -g 11.199.141.91/28
11.199.141.81 is unreachable
11.199.141.82 is unreachable
11.199.141.83 is unreachable
11.199.141.84 is unreachable
11.199.141.85 is unreachable
11.199.141.86 is unreachable
11.199.141.87 is unreachable
11.199.141.88 is unreachable
11.199.141.89 is unreachable
11.199.141.90 is unreachable
11.199.141.91 is unreachable
11.199.141.92 is unreachable
11.199.141.93 is unreachable
11.199.141.94 is unreachable

```

First step was to open up the Rock Star Sever List and grab the IP addresses for the Hollywood location, Afterwards I would use `fping `on each address range to determine which one was alive [167.172.144.11/32]. RockStar Corp doesn't want any of their servers, even if they are up, indicating that they are accepting connections. This would indicate a vulnerability, and occurred on the network layer as `fping`is used with IP addresses, which commonly reside in the network layer of the OSI model.


**Phase 2**

```bash
sysadmin@UbuntuDesktop:~$ sudo nmap -sS 167.172.144.11/32
[sudo] password for sysadmin: 

Starting Nmap 7.60 ( https://nmap.org ) at 2020-10-20 20:16 EDT
Nmap scan report for 167.172.144.11
Host is up (0.073s latency).
Not shown: 994 closed ports
PORT    STATE    SERVICE
22/tcp  open     ssh
25/tcp  filtered smtp
135/tcp filtered msrpc
139/tcp filtered netbios-ssn
445/tcp filtered microsoft-ds
646/tcp filtered ldp

Nmap done: 1 IP address (1 host up) scanned in 267.93 seconds

```

The `nmap` shows there being only one open port, SSH port 22, which falls under the application layer in the OSI model. This presents itself as a vulnerability because with SSH, a criminal could use SSH to gain unauthorized access to higher profile accounts.
*the `nmap` results would fall under the Networking layer of the OSI Model.
 

**Phase 3**

```bash
sysadmin@UbuntuDesktop:~$ sudo ssh jimi@167.172.144.11
The authenticity of host '167.172.144.11 (167.172.144.11)' can't be established.
ECDSA key fingerprint is SHA256:mDZ8+Ud+K3Y6XNWvtyAR4Q2ti1+/V3p0Bm83hF6Ua4w.
Are you sure you want to continue connecting (yes/no)? y
Please type 'yes' or 'no': y
Please type 'yes' or 'no': yes
Warning: Permanently added '167.172.144.11' (ECDSA) to the list of known hosts.
jimi@167.172.144.11's password: 
Linux GTscavengerHunt 4.9.0-11-amd64 #1 SMP Debian 4.9.189-3+deb9u1 (2019-09-20) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Wed Oct 21 00:43:13 2020 from 72.208.73.30
________________________________________________________________________________________
#logged into jimi

$ cd /etc
$ nano hosts
	#inside of nano hosts
# Your system has configured 'manage_etc_hosts' as True.
# As a result, if you wish for changes to this file to persist
# then you will need to either
# a.) make changes to the master file in /etc/cloud/templates/hosts.tmpl
# b.) change or remove the value of 'manage_etc_hosts' in
#     /etc/cloud/cloud.cfg or cloud-config from user-data
#
127.0.1.1 GTscavengerHunt.localdomain GTscavengerHunt
127.0.0.1 localhost
98.137.246.8 rollingstone.com

oooooooollowing lines are desirable for IPv6 capable hosts
::1 ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
ff02::3 ip6-allhosts

```

Using RockStar Corp's typical default credentials I was able to `ssh` into their open Hollywood server. I then used `nano` to get into `/etc/hosts` . Once there I was able to locate the source of Rockstar's problem; they are unable to access `rollingstone.com` in the Hollywood office, when they try to access the website, a different, unusual website comes up. This would indicate that there is indeed a malicious actor, as these results of `/etc/hosts` are abnormal. As the way into the server is SSH, that would fall once again under the Application layer of the OSI model.

**Phase 4**

```bash
$ cd /etc
$ ls

    packetcaptureinfo.txt  rc2.d	
    
$ cat packetcaptureinfo.txt
 Captured Packets are here:
 https://drive.google.com/file/d/1ic-CFFGrbruloYrWaw3PvT71elTkh3eF/view?usp=sharing
$ 

```





Frame 5: 42 bytes on wire (336 bits), 42 bytes captured (336 bits) on interface unknown, id 1
Ethernet II, Src: VMware_1d:b3:b1 (00:0c:29:1d:b3:b1), Dst: VMware_fd:2f:16 (00:50:56:fd:2f:16)
Address Resolution Protocol (reply)
[Duplicate IP address detected for 192.168.47.200 (00:0c:29:1d:b3:b1) - also in use by 00:0c:29:0f:71:a3 (frame 4)]

Frame 16: 1876 bytes on wire (15008 bits), 1876 bytes captured (15008 bits) on interface any, id 0
Linux cooked capture
Internet Protocol Version 4, Src: 10.0.2.15, Dst: 104.18.126.89
Transmission Control Protocol, Src Port: 33546, Dst Port: 80, Seq: 1, Ack: 1, Len: 1820
Hypertext Transfer Protocol
HTML Form URL Encoded: application/x-www-form-urlencoded

```bash
Form item: "0<text>" = "Mr Hacker"
Form item: "0<label>" = "Name"
Form item: "1<text>" = "Hacker@rockstarcorp.com"
Form item: "1<label>" = "Email"
Form item: "2<text>" = ""
Form item: "2<label>" = "Phone"
Form item: "3<textarea>" = "Hi Got The Blues Corp!  This is a hacker that works at Rock Star Corp.  Rock Star has left port 22, SSH open if you want to hack in.  For 1 Milliion Dollars I will provide you the user and password!"
Form item: "3<label>" = "Message"
Form item: "redirect" = "http://www.gottheblues.yolasite.com/contact-us.php?formI660593e583e747f1a91a77ad0d3195e3Posted=true"
Form item: "locale" = "en"
Form item: "redirect_fail" = "http://www.gottheblues.yolasite.com/contact-us.php?formI660593e583e747f1a91a77ad0d3195e3Posted=false"
Form item: "form_name" = ""
Form item: "site_name" = "GottheBlues"
Form item: "wl_site" = "0"
Form item: "destination" = "DQvFymnIKN6oNo284nIPnKyVFSVKDX7O5wpnyGVYZ_YSkg==:3gjpzwPaByJLFcA2ouelFsQG6ZzGkhh31_Gl2mb5PGk="
Form item: "g-recaptcha-response" = "03AOLTBLQA9oZg2Lh3adsE0c7OrYkMw1hwPof8xGnYIsZh8cz5TtLwl8uDMZuVOls6duzyYq2MTzsVHYzKda77dqzzNUwpa6F5Tu6b9875yKU1wZHpfOQmV8D7OTcx2rnGD6I8s-6qvyDAjCuS6vA78-iNLNUtWZXFJwleNj3hPquVMu-yzcSOX60Y-deZC8zXn8hu4c6u
```
Looking inside `/etc/` I was able to locate a packet capture left behind from the hacker, and through analyzing it I found incriminating evidence against the hacker. 

```bash
"Hi Got The Blues Corp!  This is a hacker that works at Rock Star Corp.  Rock Star has left port 22, SSH open if you want to hack in.  For 1 Milliion Dollars I will provide you the user and password!" -Hacker@rockstarcorp.com

```

The evidence was found in the transport layer, via email, in the transport layer of the OSI model.