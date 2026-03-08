# future--cs-01-

Web Application Vulnerability Assessment Lab
---------------------------------------------

This project is a simple vulnerable web application created for learning and practicing web application security testing. It demonstrates several common vulnerabilities that are frequently found in web applications.

Purpose
--------

The goal of this project is to help  help me to learn understand how vulnerabilities work and how they can be identified during a web application vulnerability assessment.

This project is intended for educational purposes only.


Scope of Testing
----------------

Application Name: Vulnerable Web Lab

Target URL: http://testphp.vulnweb.com

Testing Type: Web Application Vulnerability Assessment

Testing Methodology: Manual Testing + Automated Scanning

 Tools Used
------------

The following security tools were used during the assessment:

Burp Suite (Web Proxy & Request Interception)

OWASP ZAP (Web Application Scanner)

Nmap (Network Scanning)

SQLmap (SQL Injection Testing)

Web Browser Developer Tools


Testing Methodology
---------------------

The testing process followed standard web application security testing practices:

Information Gathering

Vulnerability Identification

Exploitation

Impact Analysis

Detailed Vulnerability Findings
-------------------------------

SQL Injection
-------------

<h2>Severity:</h2> Critical

Description:
------------
The login functionality is vulnerable to SQL Injection. User input is directly inserted into the SQL query without proper validation or parameterization.

Affected Endpoint:

/login

Proof of Concept:
-----------------
Payload used:

admin' OR '1'='1


<img width="771" height="408" alt="image" src="https://github.com/user-attachments/assets/8dd47b18-290f-417d-91a2-34afe7c23117" />


<img width="738" height="420" alt="image" src="https://github.com/user-attachments/assets/e5fc9a41-8546-46f0-a3ab-f733433f8273" />


<img width="633" height="438" alt="image" src="https://github.com/user-attachments/assets/e53f44ac-cd0e-4019-87ad-b8bd792ce557" />


Impact:
-------

An attacker can bypass authentication and gain unauthorized access to the application.

Remediation:
------------

Use parameterized queries or prepared statements to prevent SQL injection attacks


Cross-Site Scripting (XSS)
-------------------------

<h2>Severity:</h2>High

Description:
------------

User input is reflected directly in the web page without proper sanitization, allowing attackers to inject malicious scripts.

Proof of Concept:
----------------




