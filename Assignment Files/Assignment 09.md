Jonathan Portela Homework 9
Mission 1:
sysadmin@UbuntuDesktop:~$ nslookup -type=MX starwars.com
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
starwars.com	mail exchanger = 1 aspmx.l.google.com.
starwars.com	mail exchanger = 5 alt2.aspmx.l.google.com.
starwars.com	mail exchanger = 5 alt1.aspx.l.google.com.
starwars.com	mail exchanger = 10 aspmx3.googlemail.com.
starwars.com	mail exchanger = 10 aspmx2.googlemail.com.

Authoritative answers can be found from:

#edited below


sysadmin@UbuntuDesktop:~$ nslookup -type=MX starwars.com
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
starwars.com	mail exchanger = 1 asltx.l.google.com.
starwars.com	mail exchanger = 5 asltx.2.google.com.
starwars.com	mail exchanger = 5 alt1.aspx.l.google.com.
starwars.com	mail exchanger = 10 aspmx3.googlemail.com.
starwars.com	mail exchanger = 10 aspmx2.googlemail.com.

Authoritative answers can be found from:



*I believe the Resistance is not receiving emails due to switching their DNS and mail servers. It would be like moving from your apartment into a new house, but not updating your mailing address.











Mission 2:

sysadmin@UbuntuDesktop:~$ nslookup -type=txt theforce.net
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
theforce.net	text = "google-site-verification=ycgY7mtk2oUZMagcffhFL_Qaf8Lc9tMRkZZSuig0d6w"
theforce.net	text = "v=spf1 a mx mx:smtp.secureserver.net include:aspmx.googlemail.com ip4:104.156.250.80 ip4:45.63.15.159 ip4:45.63.4.215"
theforce.net	text = "google-site-verification=XTU_We07Cux-6WCSOItl0c_WS29hzo92jPE341ckbOQ"

Authoritative answers can be found from:

theforce.net	text = "v=spf1 a mx mx:smtp.secureserver.net include:aspmx.googlemail.com ip4:45.23.176.21 ip4:104.156.250.80 ip4:45.63.15.159 ip4:45.63.4.215"


*The Force’s e-mails are getting sent to spam from their new IP address of their mail server not being added to the list. It would be similar to moving into a house with roommates, except your last name isn’t on the mailbox, so the mail continues to pile up in collection at the post office.


Mission 3:

sysadmin@UbuntuDesktop:~$ nslookup -type=cname www.theforce.net
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
www.theforce.net	canonical name = theforce.net.

Authoritative answers can be found from:

Non-authoritative answer:
www.theforce.net	canonical name = resistance.theforce.net.

*The website isn’t redirecting because the canonical name needs to become resistance.theforce.net.



Mission 4:

sysadmin@UbuntuDesktop:~$ nslookup -type=NS princessleia.site
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
princessleia.site	nameserver = ns26.domaincontrol.com.
princessleia.site	nameserver = ns25.domaincontrol.com.
*princessleia.site	nameserver =ns2.galaxybackup.com
Authoritative answers can be found from:

*by adding this nameserver it prevents the issues from recurring. 

Mission 5:

Batuu => D, C, E, F, J, I, L, Q, T, V => Jedha
21 hops

Mission 6:

Address Resolution Protocol (reply)
    Hardware type: Ethernet (1)
    Protocol type: IPv4 (0x0800)
    Hardware size: 6
    Protocol size: 4
    Opcode: reply (2)
    Sender MAC address: Cisco-Li_e3:e4:01 (00:0f:66:e3:e4:01)
    Sender IP address: 172.16.0.1
    Target MAC address: IntelCor_55:98:ef (00:13:ce:55:98:ef)
    Target IP address: 172.16.0.101


Mission 7:

![09a](https://github.com/wandererjon/Bootcamp-Submissions/assets/69092248/51631bf7-3a30-4450-b2d8-ab6de2653d90)

