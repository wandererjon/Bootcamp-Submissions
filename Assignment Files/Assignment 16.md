## Week 16 Homework Submission File: Penetration Testing 1

#### Step 1: Google Dorking


- Using Google, can you identify who the Chief Executive Officer of Altoro Mutual is:

Karl Fitzgerald

- How can this information be helpful to an attacker:

This provides an attacker a name to their 'whale' they are trying to spear phish; makes tracking easier through social media. This would possibly help them social engineer Karl Fitzgerald.

#### Step 2: DNS and Domain Discovery

Enter the IP address for `demo.testfire.net` into Domain Dossier and answer the following questions based on the results:

 1. Where is the company located:
     Registrant City: Sunnyvale
     Registrant State/Province: CA

 2. What is the NetRange IP address:
     NetRange: 65.61.137.64 - 65.61.137.127

 3. What is the company they use to store their infrastructure:
     Customer: Rackspace Backbone Engineering (C05762718)

 4. What is the IP address of the DNS server:
     65.61.137.117

#### Step 3: Shodan

- What open ports and running services did Shodan find:
   HTTP 80 Server: Apache Tomcat/Coyote JSP engine/Version 1.1
   HTTPS 443 Server: Apache Tomcat/Coyote JSP engine/Version 1.1
   HTTP 8080 Server: Apache Tomcat/Coyote JSP engine/Version 1.1

#### Step 4: Recon-ng

- Install the Recon module `xssed`.
- Set the source to `demo.testfire.net`.
- Run the module.

Is Altoro Mutual vulnerable to XSS: Yes.



### Step 5: Zenmap

Your client has asked that you help identify any vulnerabilities with their file-sharing server. Using the Metasploitable machine to act as your client's server, complete the following:

- Command for Zenmap to run a service scan against the Metasploitable machine:

nmap -sV 192.168.0.10
- Zenmap vulnerability script command:

nmap --script smb-enum-shares 192.168.1.10

- Once you have identified this vulnerability, answer the following questions for your client:
 1. What is the vulnerability:
  Comment: IPC Service (metasploitable server (Samba 3.0.20-Debian))
 Anonymous access: READ/WRITE

 2. Why is it dangerous:

 Any anonymous user has full read/write privilege to the company files.

 3. What mitigation strategies can you recommendations for the client to protect their server:

 Get rid of the option for the anonymous access.

---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved. 


