# future--cs-01-

Web Application Vulnerability Assessment Lab
---------------------------------------------

The goal of this project is to understand how common web application vulnerabilities work and how they can be identified during a vulnerability assessment.


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

Steps to Reproduce
------------------
 Navigate to /login
   

 Enter the following payload in the username field:
   admin' OR '1'=' 1'
   
  
Leave password blank
   
 Click Login
  
 Authentication bypass occurs


<img width="771" height="408" alt="image" src="https://github.com/user-attachments/assets/8dd47b18-290f-417d-91a2-34afe7c23117" />


<img width="738" height="420" alt="image" src="https://github.com/user-attachments/assets/e5fc9a41-8546-46f0-a3ab-f733433f8273" />


<img width="633" height="438" alt="image" src="https://github.com/user-attachments/assets/e53f44ac-cd0e-4019-87ad-b8bd792ce557" />


Impact:
-------

Successful exploitation allows attackers to:

• Bypass authentication
• Access sensitive user data
• Perform unauthorized actions

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

<img width="613" height="400" alt="image" src="https://github.com/user-attachments/assets/43ca91d1-5227-4339-a1b2-f74d5d84919f" />


<img width="558" height="420" alt="image" src="https://github.com/user-attachments/assets/0180a27c-3ceb-45ef-b034-34dfc45f8208" />


Impact
--------
Session hijacking

Cookie theft

User impersonation


Prevention
-----------

Output encoding

Input sanitization

Content Security Policy (CSP)


Insecure Direct Object Reference (IDOR)
--------------------------------------

Severity: Medium

Description
------------

The application exposes internal object identifiers (such as user IDs or product IDs) in the URL without proper authorization checks. An attacker can manipulate these IDs to access data belonging to other users.

proof of concept :
------------------

Identify a Parameter in the URL
-------------------------------


Navigate through the application and observe the URL parameters.

Example:
--------

http://testphp.vulnweb.com/cart.php?id=1

The parameter id=1 is used to retrieve a specific item from the server.

<img width="623" height="383" alt="image" src="https://github.com/user-attachments/assets/f0360659-b1f3-4521-93d2-24c72f2930c8" />

Intercept the Request
----------------------

Use a proxy tool such as:

Burp Suite

OWASP ZAP

 I use burp suite to ntercept the HTTP request when accessing the page.

 
Intercept the Request

<img width="945" height="495" alt="image" src="https://github.com/user-attachments/assets/660b2fa1-8366-4a7d-91a4-2799469af20a" />


<img width="1920" height="1080" alt="Screenshot 2026-03-09 192530" src="https://github.com/user-attachments/assets/9f7a36a4-9f9d-46cf-8f0f-5dcd704403f5" />





send the intercept to the repeater


<img width="943" height="469" alt="image" src="https://github.com/user-attachments/assets/293ae466-7179-4e1b-9ab5-4034477bb2f3" />



now change the GET /artists.php?artist=1 HTTP/1.1 to GET /artists.php?artist=2  HTTP/1.1 



<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0fc89436-db53-440f-aaa6-117eae9f7101"/>


<img width="713" height="443" alt="image" src="https://github.com/user-attachments/assets/221f10d7-f0c9-4055-a9a7-7a68a343c684" />



Observe the Response
---------------------

The application loads information related to another item or resource.

This confirms the IDOR vulnerability because:

The application allowed access to another object

No authorization checks were performed


Impact
---------

An attacker may be able to:

Access other users’ information

Modify or delete resources

Perform unauthorized actions

Extract sensitive application data


Remediation
------------

To prevent IDOR vulnerabilities:

Implement proper authorization checks

Use indirect reference IDs

Validate user permissions before accessing objects

Apply secure access control mechanisms


Server Information Disclosure
----------------------------


Description
------------

During testing, the web server revealed its software and version in the HTTP response headers.
For example, the following header was observed:

Exposing server information may allow attackers to identify known vulnerabilities associated with the specific server version, aiding targeted attacks.


 proof of concept :
 -----------------
 
Step 1 – Intercept HTTP Response

Open the target website in a browser with Burp Suite proxy enabled.

Navigate to any page of the application.


<img width="1920" height="1080" alt="Screenshot 2026-03-09 192253" src="https://github.com/user-attachments/assets/f2bd1b66-b479-456c-89f5-bc7363afd62f" />


Step 2 – Inspect Response Headers


Check the server response 

<img width="863" height="200" alt="Screenshot 2026-03-09 194853" src="https://github.com/user-attachments/assets/1ac030ed-e87f-4fb8-bb61-2de013b0f1c4" />

it shows the server infomation like ther server version

Impact
---------

Reveals web server software and version

Allows attackers to search for version-specific vulnerabilities

Assists in planning more targeted attacks


Remediation
-----------

To prevent server information disclosure:

Disable server version headers in the web server configuration.
For NGINX, add:

server_tokens off;

Remove or obscure HTTP headers that reveal sensitive implementation details.

Regularly update and patch the web server to reduce the risk from disclosed versions




Conclusion
------------ 

This project provided hands-on experience in web application security testing using a safe and authorized environment. Multiple vulnerabilities were identified, including SQL Injection, XSS, IDOR and Server Information Disclosure, demonstrating the importance of input validation, access control, and secure configurations.

The assessment strengthened practical skills in detecting, analyzing, and documenting web vulnerabilities, following ethical security testing practices.









