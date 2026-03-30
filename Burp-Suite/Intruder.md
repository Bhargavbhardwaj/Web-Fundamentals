## Inruder

   **Burp Suite Intruder** is a powerful module used for **automated attacks on web applications**. It allows testers to send multiple modified requests by injecting different payloads into specific parts of an HTTP request. Intruder is commonly used for **fuzzing, brute-force attacks, parameter testing, and vulnerability discovery**.It builds on concepts from **Proxy and Repeater**, enabling large-scale and customizable testing with minimal manual effort.---## What is Intruder?Intruder automates the process of:- Modifying request parameters  - Sending multiple requests with different inputs  - Analyzing responses to identify anomalies  Typical workflow:```textCapture Request → Send to Intruder → Define Positions → Add Payloads → Start Attack.

Intruder Attack Positions
-------------------------

Positions define **where payloads will be inserted** in a request.

Example request:


`   POST /login HTTP/1.1Host: target.comusername=admin&password=1234   `

Marked positions:

`   username=admin&password=§1234§   `

The § § symbols indicate where payloads will be injected.

Attack Types
------------

Intruder provides multiple attack types depending on use case:

### Sniper

*   Single position attack
    
*   Tests one payload at a time
    
*   Useful for **fuzzing parameters**
    

### Battering Ram

*   Same payload used for all positions
    
*   Useful for testing **shared input fields**
    

### Pitchfork

*   Multiple payload sets used in parallel
    
*   Each position gets a corresponding payload
    
*   Useful for **credential testing**
    

### Cluster Bomb

*   All combinations of payloads
    
*   Most powerful but slower
    
*   Used for **brute-force attacks**
    

Payloads
--------

Payloads are the **input values** used during the attack.

Types of payloads include:

*   Simple list (wordlists)
    
*   Numbers
    
*   Brute-force values
    
*   Custom payloads
    

Example password wordlist:
`   adminpassword123456letmein   `

Fuzzing with Intruder
---------------------

Fuzzing involves sending unexpected or random data to identify vulnerabilities.

Example fuzz payloads:

`   '"alert(1)../../etc/passwd   `

Used to detect:

*   SQL Injection
    
*   XSS
    
*   File inclusion
    
*   Input validation flaws
    

Brute-Forcing
-------------

Intruder is commonly used for **login brute-force attacks**.

Example:

`   username=admin&password=§payload§   `

Payload list contains possible passwords.

Indicators of success:

*   Different response length
    
*   Status code change
    
*   Response content variation
    

Analyzing Results
-----------------

After launching an attack, Intruder provides results such as:

*   Status codes
    
*   Response length
    
*   Response time
    

Testers look for anomalies like:

*   Longer/shorter responses
    
*   Different status codes (200 vs 401)
    
*   Unique response patterns
    

These differences may indicate **successful payload execution**.

Key Takeaways
-------------

Burp Suite Intruder is essential for **automating web attacks and testing input fields at scale**. It enables security testers to efficiently perform **fuzzing, brute-forcing, and parameter manipulation**. By analyzing server responses, testers can identify vulnerabilities such as **authentication flaws, injection points, and weak input validation**.

Room Completed: Burp Suite IntruderFocus Area: Web Application Security, Fuzzing, Automated Attacks