# 🌐 Intro to SSRF – TryHackMe Notes


Server-Side Request Forgery (SSRF) is a web vulnerability that allows an attacker to make a vulnerable server send HTTP requests to unintended locations. Instead of the attacker directly communicating with internal resources, the vulnerable server performs the request on the attacker’s behalf. This usually occurs when an application fetches remote resources such as images, API responses, files, or web pages using user-supplied input without proper validation.

Example of a normal request where a server retrieves an external resource: https://example.com/fetch?url=https://site.com/image.jpg


If the application does not validate the URL parameter properly, an attacker can modify the request and force the server to access internal resources: https://example.com/fetch?url=http://localhost/admin


In this case the server sends a request to its own internal services and returns the response to the attacker.

There are two major types of SSRF vulnerabilities. The first is **regular SSRF**, where the response from the requested resource is returned directly to the attacker. This allows the attacker to view internal pages, API responses, configuration files, or other sensitive data. The second type is **Blind SSRF**, where the request is executed but the response is not returned to the attacker. In blind SSRF situations, attackers rely on external services such as DNS logging servers or request monitoring tools to confirm that the server performed the request.

SSRF vulnerabilities can have serious impact because attackers can leverage the web server’s internal network access. A successful SSRF attack can allow access to unauthorized internal areas, exposure of sensitive organisational or customer data, discovery of internal services, and extraction of authentication tokens or credentials. SSRF is especially dangerous in cloud environments because attackers can target cloud metadata services to retrieve access credentials.

Typical internal resources targeted in SSRF attacks include:
http://127.0.0.1/admin

http://localhost/internal-api

http://169.254.169.254/latest/meta-data/


The last address is commonly used in cloud environments such as AWS to retrieve instance metadata and credentials.

Finding SSRF vulnerabilities usually involves identifying application functionality that retrieves external resources. Common features where SSRF may appear include URL preview generators, file import functions, webhook integrations, server-side image downloads, PDF generators, and API integrations. When testing, the goal is to identify parameters that accept URLs and attempt to manipulate them.

Example parameter that may be vulnerable: /fetch?url=https://example.com


During testing, attackers modify the parameter to point to internal services such as:
http://127.0.0.1

http://localhost

http://192.168.1.1

http://10.0.0.1


If the server successfully returns responses from these addresses, SSRF may be present. Security testers often intercept requests using tools like Burp Suite to manipulate parameters and observe server responses.

Many applications attempt to block SSRF by filtering certain inputs, but attackers can often bypass these restrictions. One common technique is using alternative representations of IP addresses. For example:
http://127.1

http://2130706433


Both of these values represent the same localhost address (127.0.0.1). Attackers may also encode characters to bypass filters:
http://127.0.0.1%2fadmin


Another bypass technique involves using DNS redirection through attacker-controlled domains that resolve to internal IP addresses.

The general workflow for exploiting SSRF vulnerabilities involves identifying a URL parameter that triggers server-side requests, intercepting the request, modifying the target URL to internal resources, and analyzing the response to discover accessible services. Typical test payloads include:
http://localhost

http://127.0.0.1

http://169.254.169.254


If the application retrieves data from these resources, attackers can map internal infrastructure, access administrative interfaces, or retrieve sensitive information.

The security risks associated with SSRF include internal network reconnaissance, exposure of internal APIs, leakage of sensitive configuration data, cloud credential theft, and possible remote code execution through chained vulnerabilities. SSRF vulnerabilities are particularly dangerous because they allow attackers to pivot from an external web application into internal network environments.

Preventing SSRF requires strict validation of user-supplied URLs and strong network restrictions. Applications should implement allowlists of trusted domains rather than accepting arbitrary URLs. Access to internal IP ranges such as localhost and private network addresses should be blocked. Servers should also restrict access to metadata services and internal APIs through firewall rules and network segmentation. Applications should avoid directly using user input when making server-side requests.

Example of a safer approach:
allowed_domains = ["trusted-api.com"]

if url.domain not in allowed_domains:
deny_request()


Proper logging, input validation, and secure server configurations significantly reduce the risk of SSRF exploitation.

Room Completed: **Intro to SSRF**  
Focus Area: **Web Application Security – Server-Side Request Forgery**