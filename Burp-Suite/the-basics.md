  ## Burp Suite - The Basics  
  
  Burp Suiteis one of the most widely used **web application security testing frameworks** used by penetration testers, bug bounty hunters, and security researchers. Developed by PortSwigger, it allows testers to **intercept, inspect, and manipulate HTTP/HTTPS traffic** between a browser and a web server.  
  
  Burp Suite is essential for discovering vulnerabilities such as **SQL Injection, XSS, authentication flaws, and logic vulnerabilities** in web applications.This room focuses on understanding the **basic structure of Burp Suite**, its interface, and how to configure and use the **Burp Proxy**, which is the core component of the framework.---  ## Burp Suite OverviewBurp Suite acts as a **man-in-the-middle (MITM) proxy** between the browser and the web server. 
  This allows security testers to intercept requests, modify them, and analyze responses.Typical traffic flow when using Burp:```textBrowser → Burp Proxy → Web ServerWeb Server → Burp Proxy → Browser   `

This setup allows testers to observe and manipulate all HTTP/HTTPS traffic.

Burp Suite comes in three main editions:

*   **Community Edition** – Free version with basic features
    
*   **Professional Edition** – Advanced features for penetration testing
    
*   **Enterprise Edition** – Automated large-scale security scanning
    

Dashboard
---------

The **Dashboard** provides an overview of Burp activity and scan results. It shows:

*   Active tasks and scans
    
*   Detected vulnerabilities
    
*   Logging information
    
*   Target activity
    

This section helps testers quickly monitor ongoing testing operations.

Navigation
----------

Burp Suite uses a **tab-based interface**, making it easy to move between tools. The main navigation bar provides access to the different components of the framework.

Common tabs include:

*   Dashboard
    
*   Target
    
*   Proxy
    
*   Intruder
    
*   Repeater
    
*   Sequencer
    
*   Decoder
    
*   Comparer
    

Each tab contains specific tools used for different testing purposes.

Options and Configuration
-------------------------

Burp Suite allows users to configure settings such as:

*   Proxy listener settings
    
*   Interception behavior
    
*   SSL/TLS handling
    
*   Network interfaces
    

These settings ensure Burp properly intercepts traffic from the browser.

Example default proxy configuration:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   IP Address: 127.0.0.1Port: 8080   `

The browser must be configured to send traffic through this proxy.

Burp Proxy
----------

The **Burp Proxy** is the most important feature in Burp Suite. It intercepts HTTP/HTTPS requests between the browser and the server.

When interception is enabled, Burp pauses the request so testers can inspect or modify it.

Example intercepted request:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   GET /login HTTP/1.1Host: example.comUser-Agent: Mozilla/5.0   `

Testers can modify parameters before forwarding the request to the server.

Proxy features include:

*   Intercept requests and responses
    
*   Modify parameters
    
*   Analyze application behavior
    

Site Map and Issue Identification
---------------------------------

The **Site Map** within the Target tab displays the structure of the web application discovered during testing.

It organizes:

*   URLs
    
*   Endpoints
    
*   Parameters
    
*   Resources
    

Example structure:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   example.com ├── /login ├── /dashboard ├── /api └── /admin   `

This helps testers understand the application's attack surface and locate possible vulnerabilities.

Burp also highlights discovered **security issues** such as:

*   SQL Injection
    
*   Cross-Site Scripting (XSS)
    
*   Misconfigured security headers
    

The Burp Browser
----------------

Burp Suite includes a built-in browser called the **Burp Browser**, which is preconfigured to work with the Burp Proxy.

Advantages of using the Burp Browser:

*   Automatically routes traffic through Burp
    
*   No manual proxy configuration required
    
*   Simplifies testing setup
    

This makes it easier to start intercepting web traffic immediately.

Scoping
-------

Scoping allows testers to define which websites or domains are included in the testing process.

Benefits of scoping include:

*   Limiting analysis to specific targets
    
*   Reducing unnecessary traffic
    
*   Organizing test results
    

Example scope configuration:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Target Scope:example.com*.example.com   `

Only traffic related to these domains will be analyzed.

Targeting
---------

Targeting refers to identifying and mapping the **attack surface of a web application**.

Using the Target tab and site map, testers can identify:

*   Entry points
    
*   Parameters
    
*   APIs
    
*   Hidden directories
    

This information is used for further testing with tools like **Intruder or Repeater**.

Proxying HTTPS Traffic
----------------------

HTTPS traffic is encrypted, so Burp must install a **CA certificate** in the browser to decrypt and inspect secure traffic.

Steps typically include:

1.  Configure browser proxy settings
    
2.  Install Burp CA certificate
    
3.  Enable interception
    

Once configured, Burp can inspect HTTPS traffic such as:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   POST /login HTTP/1.1Host: example.comContent-Type: application/x-www-form-urlencodedusername=admin&password=admin   `

Without the certificate, HTTPS traffic cannot be intercepted.

Burp Suite is an essential tool for **web application penetration testing**. It allows security testers to intercept and analyze HTTP/HTTPS traffic, map application structures, and identify vulnerabilities. Understanding how to configure the **Burp Proxy, navigate the interface, and analyze site maps** forms the foundation for performing effective web security testing.

Room Completed: Burp Suite: The BasicsFocus Area: Web Application Security Testing, HTTP/HTTPS Traffic Analysis