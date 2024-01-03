## Unit 11 Submission File: Network Security Homework - Jonathan Portela

### Part 1: Review Questions 

#### Security Control Types

The concept of defense in depth can be broken down into three different security control types. Identify the security control type of each set  of defense tactics.

1. Walls, bollards, fences, guard dogs, cameras, and lighting are what type of security control?

    Answer: **Physical**

2. Security awareness programs, BYOD policies, and ethical hiring practices are what type of security control?

    Answer: **Administrative**

3. Encryption, biometric fingerprint readers, firewalls, endpoint security, and intrusion detection systems are what type of security control?

    Answer: **Technical**

#### Intrusion Detection and Attack indicators

1. What's the difference between an IDS and an IPS?

    Answer:  **IDS is for monitoring where IPS is for control**

2. What's the difference between an Indicator of Attack and an Indicator of Compromise?

   Answer:  **An IOC helps indicate if a network has been compromised or breached, while an IOA focuses on what the malicious actor is going after.**

#### The Cyber Kill Chain

Name each of the seven stages for the Cyber Kill chain and provide a brief example of each.

1. Stage 1: **Reconnaissance:**	

2. Stage 2: **Weaponization:**

3. Stage 3: **Delivery:**

4. Stage 4: **Exploitation:**

5. Stage 5: **Installation:**

6. Stage 6: **Command & Control:**

7. Stage 7: **Actions on Objectives:**


#### Snort Rule Analysis

Use the Snort rule to answer the following questions:

Snort Rule #1

```bash
alert tcp $EXTERNAL_NET any -> $HOME_NET 5800:5820 (msg:"ET SCAN Potential VNC Scan 5800-5820"; flags:S,12; threshold: type both, track by_src, count 5, seconds 60; reference:url,doc.emergingthreats.net/2002910; classtype:attempted-recon; sid:2002910; rev:5; metadata:created_at 2010_07_30, updated_at 2010_07_30;)
```

1. Break down the Sort Rule header and explain what is happening.

   Answer:

   ```bash
   Rule Header alert tcp $EXTERNAL_NET any -> $HOME_NET 5800:5820
   
   Message msg: "ET SCAN Potential VNC Scan 5800-5820";
   
   Flow flags:S,12; 
   
   Detection threshold: type both, track by_src, count 5, seconds 60;
   
   References reference: url,doc.emergingthreats.net/2002910; 
   
   Classification classtype: attempted-recon;
   
   Signature ID sid: 2002910; rev:5;
   
   Metadata metadata:created_at 2010_07_30, updated_at 2010_07_30;
   ```

2. What stage of the Cyber Kill Chain does this alert violate?

   Answer: **Recon**

3. What kind of attack is indicated?

   Answer: **a Virtual Network Computing Scan**
   

Snort Rule #2

```bash
alert tcp $EXTERNAL_NET $HTTP_PORTS -> $HOME_NET any (msg:"ET POLICY PE EXE or DLL Windows file download HTTP"; flow:established,to_client; flowbits:isnotset,ET.http.binary; flowbits:isnotset,ET.INFO.WindowsUpdate; file_data; content:"MZ"; within:2; byte_jump:4,58,relative,little; content:"PE|00 00|"; distance:-64; within:4; flowbits:set,ET.http.binary; metadata: former_category POLICY; reference:url,doc.emergingthreats.net/bin/view/Main/2018959; classtype:policy-violation; sid:2018959; rev:4; metadata:created_at 2014_08_19, updated_at 2017_02_01;)
```

1. Break down the Sort Rule header and explain what is happening.

   Answer:

   ```bash
   Rule Header alert tcp $EXTERNAL_NET $HTTP_PORTS -> $HOME_NET any
   
   Message msg:"ET POLICY PE EXE or DLL Windows file download HTTP"
   
   Flow flow:established,to_client; flowbits:isnotset,ET.http.binary; flowbits:isnotset,ET.INFO.WindowsUpdate;
   
   Detection file_data; content:"MZ"; within:2; byte_jump:4,58,relative,little; content:"PE|00 00|"; distance:-64; within:4; flowbits:set,ET.http.binary; 
   
   Metadata metadata: former_category POLICY;
   
   References reference:url,doc.emergingthreats.net/bin/view/Main/2018959;
   
   Classification classtype:policy-violation;
   
   Signature ID sid:2018959; rev:4; 
   
   Metadata metadata:created_at 2014_08_19, updated_at 2017_02_01;
   ```

   

2. What layer of the Defense in Depth model does this alert violate?

   Answer: **Application**

3. What kind of attack is indicated?

   Answer: **An executable file was downloaded from an HTTP source.**

Snort Rule #3

- Your turn! Write a Snort rule that alerts when traffic is detected inbound on port 4444 to the local network on any port. Be sure to include the `msg` in the Rule Option.

    Answer:
    
    ```bash
    Rule Header alert tcp $EXTERNAL_NET any -> $HOME_NET 4444
    
    Message msg:"external entry to $HOME_NET port 4444"
    ```
    
    

### Part 2: "Drop Zone" Lab

#### Log into the Azure `firewalld` machine

Log in using the following credentials:

- Username: `sysadmin`
- Password: `cybersecurity`

#### Uninstall `ufw`

Before getting started, you should verify that you do not have any instances of `ufw` running. This will avoid conflicts with your `firewalld` service. This also ensures that `firewalld` will be your default firewall.

- Run the command that removes any running instance of `ufw`.

    ```bash
    sudo apt-get --purge remove ufw
    ```

#### Enable and start `firewalld`

By default, these service should be running. If not, then run the following commands:

- Run the commands that enable and start `firewalld` upon boots and reboots.

    ```bash
    $ sudo systemctl enable firewalld 
    $ sudo systemctl start firewalld 
    ```

  Note: This will ensure that `firewalld` remains active after each reboot.

#### Confirm that the service is running.

- Run the command that checks whether or not the `firewalld` service is up and running.

    ```bash
    $ sudo systemctl status firewalld 
    ```


#### List all firewall rules currently configured.

Next, lists all currently configured firewall rules. This will give you a good idea of what's currently configured and save you time in the long run by not doing double work.

- Run the command that lists all currently configured firewall rules:

    ```bash
    $ sudo firewall-cmd --list-all-zones
    ```

- Take note of what Zones and settings are configured. You many need to remove unneeded services and settings.

#### List all supported service types that can be enabled.

- Run the command that lists all currently supported services to see if the service you need is available

    ```bash
    $ sudo firewall-cmd --get-services
    ```

- We can see that the `Home` and `Drop` Zones are created by default.


#### Zone Views

- Run the command that lists all currently configured zones.

    ```bash
    $ firewall-cmd --get-active-zones
    ```

- We can see that the `Public` and `Drop` Zones are created by default. Therefore, we will need to create Zones for `Web`, `Sales`, and `Mail`.

#### Create Zones for `Web`, `Sales` and `Mail`.

- Run the commands that creates Web, Sales and Mail zones.

    ```bash
    $ sudo firewall-cmd --permanent --new-zone=WEB
    $ sudo firewall-cmd --permanent --new-zone=SALES
    $ sudo firewall-cmd --permanent --new-zone=MAIL
    ```

#### Set the zones to their designated interfaces:

- Run the command that sets your `eth0` interface to your zones.

    ```bash
    $ sudo firewall-cmd --zone=public --change-interface=eth0 --permanent
    $ sudo firewall-cmd --zone=WEB --change-interface=eth1 --permanent
    $ sudo firewall-cmd --zone=SALES --change-interface=eth2 --permanent
    $ sudo firewall-cmd --zone=MAIL --change-interface=eth3 --permanent
    ```

#### Add services to the active zones:

- Run the commands that add services to the **public** zone, the **web** zone, the **sales** zone, and the **mail** zone.

- Public:

    ```bash
    $ sudo firewall-cmd --zone=public --add-service=http --permanent
    $ sudo firewall-cmd --zone=public --add-service=https --permanent
    $ sudo firewall-cmd --zone=public --add-service=pop3 --permanent
    $ sudo firewall-cmd --zone=public --add-service=smtp --permanent
    ```

- Web:

    ```bash
    $ sudo firewall-cmd --zone=WEB --add-service=http --permanent
    ```

- Sales

    ```bash
    $ sudo firewall-cmd --zone=SALES --add-service=https --permanent
    ```

- Mail

    ```bash
    $ sudo firewall-cmd --zone=MAIL --add-service=smtp --permanent
    $ sudo firewall-cmd --zone=MAIL --add-service=pop3 --permanent
    ```

- What is the status of `http`, `https`, `smtp` and `pop3`?

#### Add your adversaries to the Drop Zone.

- Run the command that will add all current and any future blacklisted IPs to the Drop Zone.

     ```bash
    $ sudo firewall-cmd --zone=drop --permanent --add-source=10.208.56.23
    $ sudo firewall-cmd --zone=drop --permanent --add-source=135.95.103.76
    $ sudo firewall-cmd --zone=drop --permanent --add-source=76.34.169.118
    ```

#### Make rules permanent then reload them:

It's good practice to ensure that your `firewalld` installation remains nailed up and retains its services across reboots. This ensure that the network remains secured after unplanned outages such as power failures.

- Run the command that reloads the `firewalld` configurations and writes it to memory

    ```bash
    $ sudo firewall-cmd --reload
    ```

#### View active Zones

Now, we'll want to provide truncated listings of all currently **active** zones. This a good time to verify your zone settings.

- Run the command that displays all zone services.

    ```bash
    $ sudo firewall-cmd --get-active-zones
    ```


#### Block an IP address

- Use a rich-rule that blocks the IP address `138.138.0.3`.

    ```bash
    $ sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="'138.138.0.3'" reject'
    ```

#### Block Ping/ICMP Requests

Harden your network against `ping` scans by blocking `icmp ehco` replies.

- Run the command that blocks `pings` and `icmp` requests in your `public` zone.

    ```bash
    $ sudo firewall-cmd --zone=public --add-icmp-block=echo-reply --add-icmp-block=echo-request --permanent
    ```

#### Rule Check

Now that you've set up your brand new `firewalld` installation, it's time to verify that all of the settings have taken effect.

- Run the command that lists all  of the rule settings. Do one command at a time for each zone.

    ```bash
    $ sudo firewall-cmd --zone=public --list-all
    $ sudo firewall-cmd --zone=drop --list-all
    $ sudo firewall-cmd --zone=WEB --list-all
    $ sudo firewall-cmd --zone=SALES --list-all
    $ sudo firewall-cmd --zone=MAIL --list-all
    ```

- Are all of our rules in place? If not, then go back and make the necessary modifications before checking again.


Congratulations! You have successfully configured and deployed a fully comprehensive `firewalld` installation.

---

### Part 3: IDS, IPS, DiD and Firewalls

Now, we will work on another lab. Before you start, complete the following review questions.

#### IDS vs. IPS Systems

1. Name and define two ways an IDS connects to a network.

   Answer 1: **A host based connection (HIDS); this IDS is set up on a specific hosting device.**

   Answer 2:  **A network based connection (NIDS); this IDS is set up on a network, allowing it to serve multiple devices.**

2. Describe how an IPS connects to a network.

   Answer:  **An IPS connects to a network in-lined. Sitting between the source and destination.**

3. What type of IDS compares patterns of traffic to predefined signatures and is unable to detect Zero-Day attacks?

   Answer: **Snort**

4. Which type of IDS is beneficial for detecting all suspicious traffic that deviates from the well-known baseline and is excellent at detecting when an attacker probes or sweeps a network?

   Answer: **Host Intrusion Detection System (HIDS)**

#### Defense in Depth

1. For each of the following scenarios, provide the layer of Defense in Depth that applies: 

    1.  A criminal hacker tailgates an employee through an exterior door into a secured facility, explaining that they forgot their badge at home.

        Answer: **Perimeter/Policy, depends who you want to blame and what chart you use.** 

    2. A zero-day goes undetected by antivirus software.

        Answer: **Host**

    3. A criminal successfully gains access to HR’s database.

        Answer: **Application**

    4. A criminal hacker exploits a vulnerability within an operating system.

        Answer: **Host**

    5. A hacktivist organization successfully performs a DDoS attack, taking down a government website.

        Answer: **Application**

    6. Data is classified at the wrong classification level.

        Answer: **Data**

    7. A state sponsored hacker group successfully firewalked an organization to produce a list of active services on an email server.

        Answer: **Network**

2. Name one method of protecting data-at-rest from being readable on hard drive.

    Answer: **Encryption**

3. Name one method to protect data-in-transit.

    Answer:  **DLP**

4. What technology could provide law enforcement with the ability to track and recover a stolen laptop.

   Answer:  **GPS**

5. How could you prevent an attacker from booting a stolen laptop using an external hard drive?

    Answer: **Firmware Passwords**


#### Firewall Architectures and Methodologies

1. Which type of firewall verifies the three-way TCP handshake? TCP handshake checks are designed to ensure that session packets are from legitimate sources.

  Answer: **Circuit Level Firewalls**

2. Which type of firewall considers the connection as a whole? Meaning, instead of looking at only individual packets, these firewalls look at whole streams of packets at one time.

  Answer:  **Stateful Packet Filtering Firewall**

3. Which type of firewall intercepts all traffic prior to being forwarded to its final destination. In a sense, these firewalls act on behalf of the recipient by ensuring the traffic is safe prior to forwarding it?

  Answer: **Application Firewall**


4. Which type of firewall examines data within a packet as it progresses through a network interface by examining source and destination IP address, port number, and packet type- all without opening the packet to inspect its contents?

  Answer:  **UFW**


5. Which type of firewall filters based solely on source and destination MAC address?

  Answer: **MAC Layer Filter**




---

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
