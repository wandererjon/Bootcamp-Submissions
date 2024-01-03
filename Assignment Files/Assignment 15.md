## Unit 15 Submission File: Web Vulnerabilities and Hardening 
Jonathan Portela




### Part 1: Q&A


#### The URL Cruise Missile


The URL is the gateway to the web, providing the user with unrestricted access to all available online resources. In the wrong hands can be used as a weapon to launch attacks.


Use the graphic below to answer the following questions:


| Protocol         | Host Name                 | Path                   | Parameters               |
| ---------------- | :-----------------------: | ---------------------- | ------------------------ |
| **http://**      | **`www.buyitnow.tv`**     | **/add.asp**           | **?item=price#1999**     |




1. Which part of the URL can be manipulated by an attacker to exploit a vulnerable back-end database system? 


Answer: the Parameters ?item=price#1999


2. Which part of the URL can be manipulated by an attacker to cause a vulnerable web server to dump the `/etc/passwd` file? Also, name the attack used to exploit this vulnerability.


Answer: The path, an attack that can be used is the directory traversing attack.
   
3. Name three threat agents that can pose a risk to your organization.


Answer: A hacktivist, a nation state, or an organized group of malicious actors.


4. What kinds of sources can act as an attack vector for injection attacks?


Answer: Any source if it’s able to.


5. Injection attacks exploit which part of the CIA triad?


Answer: Injection attacks exploit the Confidentiality.


6. Which two mitigation methods can be used to thwart injection attacks?


____


#### Web Server Infrastructure


Web application infrastructure includes  sub-components and external applications that provide  efficiency, scalability, reliability, robustness, and most critically, security.


- The same advancements made in web applications that provide users these conveniences are the same components that criminal hackers use to exploit them. Prudent security administrators need to be aware of how to harden such systems.




Use the graphic below to answer the following questions:


| Stage 1        | Stage 2             | Stage 3                 | Stage 4              | Stage 5          |
| :------------: | :-----------------: | :---------------------: | :------------------: | :--------------: |
| **Client**     | **Firewall**        | **Web Server**          | **Web Application**  | **Database**     |
   
   
1. What stage is the most inner part of the web architecture where data such as, customer names, addresses, account numbers, and credit card info, is stored?


Answer: 5


2. Which stage includes online forms, word processors, shopping carts, video and photo editing, spreadsheets, file scanning, file conversion, and email programs such as Gmail, Yahoo and AOL.


Answer: 4


3. What stage is the component that stores files (e.g. HTML documents, images, CSS stylesheets, and JavaScript files) that's connected to the Internet and provides support for physical data interactions between other devices connected to the web?


Answer: 3


4. What stage is where the end user interacts with the World Wide Web through the use of a web browser?


Answer: 1 


5. Which stage is designed to prevent unauthorized access to and from protected web server resources?


Answer: 2


----




#### Server Side Attacks


In today’s globally connected cyber community, network and OS level attacks are well defended through the proper deployment of technical security controls such as, firewalls, IDS, Data Loss Prevention, EndPoint and security. However, web servers are accessible from anywhere on the web, making them vulnerable to attack.


1. What is the process called that cleans and scrubs user input in order to prevent it from exploiting security holes by proactively modifying user input.


Answer: Input sanitization


2. Name the process that tests user and application-supplied input. The process is designed to prevent malformed data from entering a data information system by verifying user input meets a specific set of criteria (i.e. a string that does not contain standalone single quotation marks).


Answer: Input validation


3. **Secure SDLC** is the process of ensuring security is built into web applications throughout the entire software development life cycle. Name three reasons why organization might fail at producing secure web applications.


Answer: Lack of funds, use of non updated software, lack of knowledge.


4. How might an attacker exploit the `robots.txt` file on a web server?


Answer: Through the server information provided with it.


5. What steps can an organization take to obscure or obfuscate their contact information on domain registry web sites?


Answer: By using some sort of private registration service.
   
6. True or False: As a network defender, `Client-Side` validation is preferred over `Server-Side` validation because it's easier to defend against attacks.


   - Explain why you chose the answer that you did. 


Answer: False, anything client side could possibly be manipulated much easier than anything on the server side.


____


#### Web Application Firewalls


WAFs are designed to defend against different types of HTTP attacks and various query types such as SQLi and XSS.


WAFs are typically present on web sites that use strict transport security mechanisms such as online banking or e-commerce websites.


1. Which layer of the OSI model do WAFs operate at?


Answer: Application layer


2. A WAF helps protect web applications by filtering and monitoring what?


Answer: by analyzing GET & POST requests sent through HTTP(S) 


3. True or False: A WAF based on the negative security model (Blacklisting) protects against known attacks, and a WAF based on the positive security model (Whitelisting) allows pre-approved traffic to pass.


Answer: False
____


#### Authentication and Access Controls


Security enhancements designed to require users to present two or more pieces of evidence or credentials when logging into an account is called multi-factor authentication.


- Legislation and regulations such as The Payment Card Industry (PCI) Data Security Standard requires the use of MFAs for all network access to a Card Data Environment (CDE).


- Security administrators should have a comprehensive understanding of the basic underlying principles of how MFA works.


1. Define all four factors of multifactor authentication and give examples of each:


   - Factor 1: What the user has; a key, faub, card, badge


   
   - Factor 2: What the user knows; password, pin, pattern
   
   
   - Factor 3: Who the user is; fingerprint, eye scanner, facial recognition


   
   - Factor 4: Where the user is; gps location


   
2. True or False: A password and pin is an example of 2-factor authentication.


Answer: False
   
3. True or False: A password and `google authenticator app` is an example of 2-factor authentication.


Answer: True
   
4. What is a constrained user interface? 


Answer: Almost like a parental control, where it blocks and limits what the "child" can see.


----
____


### Part 2: The Challenge 


In this activity, you will assume the role of a pen tester hired by a bank to test the security of the bank’s authentication scheme, sensitive financial data, and website interface.




#### Challenge #1


Please include a screenshot here of the hidden JavaScript:

![15a](https://github.com/wandererjon/Bootcamp-Submissions/assets/69092248/beda313b-d022-4ebb-a745-f1844d5bf015)



#### Challenge #2


Please include a screenshot here of all the credit card numbers from the database: 

![15b](https://github.com/wandererjon/Bootcamp-Submissions/assets/69092248/dec08d75-9918-4ebe-9516-9a962d0f0bf7)



#### Challenge #3


Please include a screenshot of the defaced website:

 ![15c](https://github.com/wandererjon/Bootcamp-Submissions/assets/69092248/08b34bee-2612-4bc9-a638-799a046364d7)



---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.  


