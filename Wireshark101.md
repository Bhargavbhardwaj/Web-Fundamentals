 ## ROOM NAME - WIRESHARK101
 
 Wireshark is one of the most widely used **network packet analysis tools** used by cybersecurity professionals, network engineers, and SOC analysts. It allows users to **capture, inspect, and analyze network packets** in real time or from stored packet capture files (**PCAPs**). 
 
 Packet analysis helps security analysts investigate suspicious traffic, troubleshoot network issues, detect attacks, and understand how protocols behave on a network.In security investigations and incident response, Wireshark is commonly used to **analyze malicious traffic, identify command-and-control communication, detect exploitation attempts, and inspect data exfiltration attempts**.---## Packet Capture and Collection MethodsBefore analyzing traffic, packets must be captured from a network interface. Wireshark can capture packets in **live traffic** or analyze previously saved **PCAP files**.Common packet collection methods include:- **Live Capture** – Capturing packets directly from a network interface.- **PCAP Files** – Analyzing previously captured traffic.- **SPAN / Port Mirroring** – Copying traffic from a switch port for analysis.- **Network TAPs** – Dedicated hardware devices that replicate network traffic.Example PCAP file types:```text.pcap.pcapng   `

These files store detailed packet information including **source IP, destination IP, protocols, payloads, and timestamps**.

Filtering Captures
------------------

Large network captures may contain thousands of packets, so filtering helps analysts quickly identify relevant traffic.

Wireshark provides two main filtering methods:

**Capture Filters** – Applied before packets are captured.

Example capture filter:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   port 80   `

Captures only HTTP traffic.

**Display Filters** – Applied after packets are captured.

Example display filters:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   ip.addr == 192.168.1.10tcp.port == 80dnshttp   `

Display filters are commonly used during investigations to isolate suspicious traffic.

Packet Dissection
-----------------

Wireshark automatically **dissects packets** and breaks them into protocol layers based on the **OSI model**.

Typical packet structure:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Frame  → Ethernet Header      → IP Header          → TCP/UDP Header              → Application Data   `

Each packet provides important details such as:

*   Source and destination IP addresses
    
*   Port numbers
    
*   Protocol type
    
*   Packet payload
    
*   Sequence numbers
    

Packet dissection helps analysts understand **how data flows across networks**.

ARP Traffic
-----------

**Address Resolution Protocol (ARP)** is used to map **IP addresses to MAC addresses** within local networks.

Example ARP request:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Who has 192.168.1.1? Tell 192.168.1.5   `

Example ARP reply:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   192.168.1.1 is at aa:bb:cc:dd:ee:ff   `

Security analysts monitor ARP traffic to detect attacks such as:

*   **ARP spoofing**
    
*   **Man-in-the-Middle attacks**
    

Example Wireshark filter:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   arp   `

ICMP Traffic
------------

**Internet Control Message Protocol (ICMP)** is used for network diagnostics and error messages.

Common ICMP operations include:

*   Ping requests
    
*   Ping replies
    
*   Network reachability tests
    

Example ICMP filter:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   icmp   `

Attackers sometimes use ICMP for:

*   Network reconnaissance
    
*   Covert communication
    
*   Data exfiltration
    

HTTP Traffic
------------

**HTTP (Hypertext Transfer Protocol)** is used for communication between web browsers and web servers.

Example HTTP request:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   GET /index.html HTTP/1.1Host: example.com   `

Example Wireshark filter:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   http   `

Because HTTP traffic is **unencrypted**, analysts can view:

*   URLs visited
    
*   Cookies
    
*   User agents
    
*   Form data
    

This makes HTTP traffic useful for forensic analysis.

DNS Traffic
-----------

**Domain Name System (DNS)** translates domain names into IP addresses.

Example DNS query:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   example.com → 93.184.216.34   `

Example Wireshark filter:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   dns   `

Security analysts monitor DNS traffic to detect:

*   Malware communication
    
*   Data exfiltration through DNS tunneling
    
*   Suspicious domain lookups
    

TCP Traffic
-----------

**Transmission Control Protocol (TCP)** is a reliable transport protocol responsible for ensuring accurate data transmission.

TCP includes mechanisms such as:

*   Three-way handshake
    
*   Sequence numbers
    
*   Acknowledgements
    

Example TCP handshake:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   SYN → SYN/ACK → ACK   `

Example Wireshark filter:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   tcp   `

TCP analysis helps detect:

*   Connection issues
    
*   Network scans
    
*   Suspicious sessions
    

HTTPS Traffic
-------------

**HTTPS (HTTP Secure)** encrypts web traffic using **TLS (Transport Layer Security)**.

Example Wireshark filter:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   tls   `

Unlike HTTP, HTTPS traffic **cannot be directly read** because the payload is encrypted.

However, analysts can still observe:

*   Server IP addresses
    
*   TLS handshake details
    
*   Certificate information
    
*   Session metadata
    

This helps identify suspicious encrypted communications.

Analyzing Exploit PCAPs
-----------------------

In cybersecurity investigations, analysts frequently analyze **malicious PCAP files** to detect attack activity.

Common indicators in exploit PCAPs include:

*   Suspicious DNS queries
    
*   Reverse shell connections
    
*   Exploit payloads
    
*   Data exfiltration attempts
    
*   Malware command-and-control traffic
    

Useful Wireshark techniques include:

*   Filtering suspicious protocols
    
*   Following TCP streams
    
*   Reconstructing HTTP sessions
    

Example:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Follow → TCP Stream   `

This allows analysts to view complete conversations between hosts.

Wireshark is an essential tool for **network monitoring, incident response, and threat detection**. By capturing and analyzing network packets, security analysts can investigate suspicious activity, detect attacks, and understand how different protocols operate. Mastering Wireshark and packet analysis is an important skill for **SOC analysts, penetration testers, and network security professionals**.

Room Completed: Wireshark 101Focus Area: Network Traffic Analysis, Packet Inspection, Network Forensics