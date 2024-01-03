
GoodSecurity Penetration Test Report 

jonathanportela@GoodSecurity.com

02/18/2021


    1.0 High-Level Summary

GoodSecurity was tasked with performing an internal penetration test on GoodCorp’s CEO, Hans Gruber. An internal penetration test is a dedicated attack against internally connected systems. The focus of this test is to perform attacks, similar to those of a hacker and attempt to infiltrate Hans’ computer and determine if it is at risk. GoodSecurity’s overall objective was to exploit any vulnerable software and find the secret recipe file on Hans’ computer, while reporting the findings back to GoodCorp.
When performing the internal penetration test, there were several alarming vulnerabilities that were
identified on Hans’ desktop. When performing the attacks, GoodSecurity was able to gain access to his machine and find the secret recipe file by exploit two programs that had major vulnerabilities. The details of the attack can be found in the ‘Findings’ category.
    2.0 Findings

Machine IP:
192.168.0.20
Hostname:
Host: MSEDGEWIN10; OS: Windows; CPE: cpe:/o:microsoft:windows
Vulnerability Exploited:
exploit/windows/http/icecast_header
Vulnerability Explanation:
This vulnerability is one of the buffer overflow varieties. It accomplishes its goal by sending 32 HTTP headers carrying a write one past the end of a pointer array.
Severity:
High severity, gained read/write access with this vulnerability.
Proof of Concept:




Recommendations

My recommendation would be to update IceCast so it is not susceptible to this vulnerability, they released a fix for this with Version 2.02 which would be available at: 

http://www.icecast.org/download.php







