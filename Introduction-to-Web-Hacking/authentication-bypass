# 🔐 Authentication Bypass – TryHackMe Notes


**Overview**

Authentication bypass vulnerabilities occur when an attacker gains access to a system without valid credentials. These weaknesses are often caused by poor authentication design, weak validation, or improper session management. Exploiting such vulnerabilities can lead to unauthorized account access, exposure of sensitive customer data, and privilege escalation.

This room covered common authentication bypass techniques including **username enumeration, brute force attacks, logic flaws, and cookie tampering**.

---

**Username Enumeration**

Username enumeration happens when a website reveals whether a username exists in the system. Attackers exploit differences in responses to determine valid accounts before launching password attacks.

Example responses:

If the application returns different messages for invalid usernames and incorrect passwords, attackers can identify valid usernames. Enumeration can also occur through **response timing differences** or **HTTP status codes**.

Attack process:
- Send login requests with many usernames
- Observe server responses
- Identify valid accounts
- Target those accounts in further attacks

Mitigation:
- Use generic authentication error messages
- Implement rate limiting
- Add CAPTCHA protection
- Monitor repeated login attempts

---

**Brute Force Attacks**

Brute forcing is the process of repeatedly trying different passwords until the correct one is found. Attackers usually automate this process using password wordlists.

Example attack attempt:
username: admin
password list:
123456
password
admin123
qwerty

Common tools used for brute forcing include:
- Burp Suite Intruder
- FFUF

Indicators of brute force activity:
- Multiple login failures from the same IP
- Rapid login attempts
- Login attempts using common password lists

Mitigation:
- Account lockout policies
- Rate limiting
- CAPTCHA
- Multi-Factor Authentication (MFA)
- Monitoring authentication logs

---

**Logic Flaws**

Logic flaws occur when the authentication workflow is implemented incorrectly. Instead of exploiting technical vulnerabilities, attackers exploit mistakes in the application's logic.

Example authentication flow:
Step 1 → Enter username
Step 2 → Enter password
Step 3 → Access dashboard


If the application does not properly validate each step, attackers may bypass authentication entirely.

Examples of logic flaws:
- Direct access to restricted pages (`/dashboard`, `/admin`)
- Manipulating request parameters
- Skipping authentication steps
- Improper verification of login states

Mitigation:
- Enforce server-side authentication checks
- Validate sessions on every request
- Implement secure access control
- Perform thorough security testing during development

---

**Cookie Tampering**

Cookies store session information that allows a user to remain authenticated. If cookies are not properly secured, attackers can modify them to gain unauthorized access.

Example cookie value:

user=guest
Modified by attacker:

user=admin


Common weaknesses:
- Storing sensitive information in plaintext cookies
- Predictable session IDs
- Lack of integrity checks
- Missing security flags

Attack methods include editing cookies through browser developer tools or intercepting requests using tools such as Burp Suite.

Secure cookies should include flags such as:

HttpOnly
Secure
SameSite


Mitigation:
- Store only session identifiers in cookies
- Encrypt or sign cookie data
- Validate session tokens server-side
- Implement session expiration and regeneration

---

**Key Security Takeaways**

Authentication mechanisms are critical components of web security and common targets for attackers. Username enumeration allows attackers to identify valid accounts, brute force attacks exploit weak passwords, logic flaws bypass authentication workflows, and cookie tampering targets insecure session management. Implementing strong authentication controls, secure session handling, and proper monitoring significantly reduces the risk of authentication bypass attacks.

---

**Room Completed:** Authentication Bypass  
**Focus Area:** Web Application Security