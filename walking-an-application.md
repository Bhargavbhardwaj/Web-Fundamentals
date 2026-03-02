# 🔍 Manual Web Application Security Review Using Browser Developer Tools
**Platform:** TryHackMe  
**Track:** Web Application Security  
**Learning Log:** Day Update  

---

## 📌 Introduction

Today I learned how to manually review a web application for security issues using only the built-in tools available in modern web browsers.

This is an important skill because automated scanners often miss:
- Business logic vulnerabilities
- Hidden endpoints
- Client-side weaknesses
- Sensitive information exposed in source code

Manual testing strengthens foundational penetration testing skills and improves understanding of how web applications function internally.

---

# 🛠 Browser Tools Used in Manual Security Testing

---

## 1️⃣ View Source

### 🔎 Purpose
Displays the raw HTML source code of the webpage.

### 🎯 Security Relevance
- Identify exposed comments
- Detect hidden input fields
- Discover internal paths or endpoints
- Locate JavaScript files
- Sometimes find exposed credentials (misconfiguration)

🔎 What It Does

Allows you to view the raw HTML source code of a webpage.

🎯 Why It’s Important in Security Testing
Detects exposed comments left by developers.
Finds hidden input fields.
Identifies API endpoints or internal paths.
Reveals JavaScript files.
Sometimes exposes credentials (bad practice but happens).

🧠 What to Look For
<!-- TODO: Remove test credentials -->
<input type="hidden" name="admin" value="true">
<script src="/js/debug.js"></script>
🔐 Security Insights

Sensitive information should never be exposed in client-side code.
Hidden fields are not secure — they can be modified.

### 🧠 Example Findings

```html
<!-- TODO: Remove test credentials -->
<input type="hidden" name="admin" value="true">
<script src="/js/debug.js"></script>

2️⃣ Inspector (Developer Tools → Elements Tab)
🔎 What It Does
Allows live inspection and modification of HTML and CSS.

🎯 Why It’s Important
Modify page elements in real time.
Remove “disabled” attributes.
Reveal hidden content.
Bypass client-side restrictions.

🧠 Practical Example
Changing:
<input type="text" disabled>

To:
<input type="text">

Or modifying:
<button style="display:none;">Admin Panel</button>
🚨 Security Insight

Client-side validation is not secure.
All critical validation must be enforced server-side.

3️⃣ Debugger (Sources Tab)
🔎 What It Does

Allows you to:
View JavaScript files
Set breakpoints
Control execution flow
Analyze logic

🎯 Why It’s Important
Understand how authentication works.
Detect client-side validation logic.
Identify API endpoints.
Reverse engineer application behavior.

🧠 Things to Look For
Hardcoded API keys
Secret tokens
Obfuscated but readable logic
Role-based access checks done only in JavaScript

Example:
if(userRole == "admin"){
    showAdminPanel();
}

⚠️ If access control is handled only in JavaScript, it’s vulnerable.

4️⃣ Network Tab
🔎 What It Does
Monitors all network requests made by the webpage.

🎯 Why It’s Critical in Security Testing
View API calls.
Inspect request headers.
See cookies and session tokens.
Identify hidden endpoints.
Analyze response codes (200, 403, 500, etc.)

🧠 What to Analyze
GET vs POST requests
JSON responses
Authentication tokens
Session cookies
Error messages leaking information

Example findings:
/api/admin/users
JWT tokens in headers
Internal server error responses revealing stack traces

📖 Reflection

This session strengthened my understanding of how web applications operate behind the scenes.
Learning to use browser developer tools effectively is a fundamental skill for web application security testing and ethical hacking.