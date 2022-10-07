# OSWA
*Work in Progress*

Offensive Security Web Assessor (OSWA) WEB-200 Resources 

This is not meant to be a comprehensive list or resource for the OSWA exam but instead reflects what I found to be useful during my journey with the course and exam. 

# Scripts
* Python HTTP Server w/CORS Headers - [CORServer.py](https://github.com/machevalia/OSWA/blob/main/Scripts/CORServer.py)

# Examples
This folder will contain tool examples and payload examples for discovery.

# Tool Recommendations
* [Dirsearch](https://www.kali.org/tools/dirsearch/)- I prefer dirsearch over other directory and file brute forcing tools.

# Tips & Tricks
* When running into issues with Gopher protocol requests for SSRFs: spin up a server on your machine and send the request to yourself to see how it is formatted. Make sure that your request is formatted in a way that looks the same as what the server is expecting a client to send. Ex. if you can send a request to a page, look at how the request is formatted in your Burp history then try to make your Gopher request to adopt the same formatting. 
* When you believe a CSRF is present, enumerate that possible actions you can get the victim to execute then perform that action yourself, if possible. By performing it yourself you can see how the parameters and values are formatted in your Burp history. Use that data to craft your payload. 
* Seclists - raft series for discovery are your friend, not just in OffSec courses/exams but in the real-world. 
* If you're tools support it, route them through BurpSuite so you have the traffic history as well as so you can see the responses. 
  * Wrote your own script and need to proxy it? I wrote a guide to that [here](https://github.com/machevalia/ProxyPythonBurpSuite)

# Practice Labs/Resources
* [PortSwigger Academy](https://portswigger.net/web-security) IMO, their content is better at building the fundamentals and understand of the vuln classes than OffSec's content. If you get stuck with a concept using OffSec's materials, check these out. Not all of their content is fully built at the moment (late 2022) but they are always adding new stuff. 
  * [SQL Injection](https://portswigger.net/web-security/sql-injection)
  * [Cross-Site Scripting (XSS)](https://portswigger.net/web-security/cross-site-scripting)
  * [Cross-Site Request Forgery (CSRF)](https://portswigger.net/web-security/csrf)
  * [External XML Entities (XXE)](https://portswigger.net/web-security/xxe)
  * [Cross-origin Resource Sharing (CORS)](https://portswigger.net/web-security/cors)
  * [Server-Side Request Forgery (SSRF)](https://portswigger.net/web-security/ssrf)
  * [Command Injection](https://portswigger.net/web-security/os-command-injection)
  * [Server-Side Template Injection (SSTI)](https://portswigger.net/web-security/server-side-template-injection)
  * [Directory Traversal](https://portswigger.net/web-security/file-path-traversal)
  * [Insecure Direct Object References (IDOR)](https://portswigger.net/web-security/access-control/idor)
* Perspective Risk's Practical SQL injection Cheat Sheets. REALLY GOOD. I like their cheatsheets more than any of the others that are out there...sorry pentestmonkey.
  * [MySQL SQL Injection](https://perspectiverisk.com/mysql-sql-injection-practical-cheat-sheet/)
  * [MSSQL SQL Injection](https://perspectiverisk.com/mssql-practical-injection-cheat-sheet/)
* [SQLZoo](https://sqlzoo.net/wiki/SQL_Tutorial) Thorough SQL Tutorial.
* Proving Grounds/VulnHub Boxes - links are to the VulnHub versions if available. 
  * [FunboxEasyEnum](https://www.vulnhub.com/entry/funbox-easyenum,565/)
  * [inclusiveness](https://www.vulnhub.com/entry/inclusiveness-1,422/)
  * [potato](https://www.vulnhub.com/entry/potato-1,529/)
  * [sumo](https://www.vulnhub.com/entry/sumo-1,480/) 
  * shakabra - PG only
  * hawat - PG only
* Do the Challenges from the course. They are probably the best examples of what you will see. 


# Articles
