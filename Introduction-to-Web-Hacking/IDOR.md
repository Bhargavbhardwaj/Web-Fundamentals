# 🔓 IDOR (Insecure Direct Object Reference) – TryHackMe Notes
# AUTHOR - Bhargav Bhardwaj

## Overview

IDOR (Insecure Direct Object Reference) is a type of **Access Control Vulnerability** where an application exposes a reference to internal objects (files, database records, user accounts, etc.) without properly verifying that the requesting user has permission to access them.

This occurs when applications **trust user-supplied input** such as IDs, filenames, or keys without performing proper **server-side authorization checks**.

Attackers can manipulate these object references to access data belonging to other users.

Example: https://example.com/profile?id=1001

If the application does not verify ownership, changing the ID may expose another user's data:
https://example.com/profile?id=1002

This can lead to **data leakage, account takeover, or exposure of sensitive information**.

---

## Where IDOR Vulnerabilities Are Commonly Found

IDOR vulnerabilities are often present in endpoints that retrieve user-specific data.

Common locations include:

- Profile pages
- Order history pages
- Download endpoints
- API requests
- Document retrieval systems
- Password reset tokens
- File access URLs

Example vulnerable endpoint: /download?file=report_102.pdf


An attacker may try: /download?file=report_103.pdf
If the server does not verify authorization, unauthorized files may be accessible.

---

## Basic IDOR Discovery Methodology

A typical workflow for identifying IDOR vulnerabilities:

1. Identify requests that reference objects using IDs.
2. Capture the request using a proxy (Burp Suite).
3. Modify the identifier value.
4. Observe if the server returns data belonging to another user.

Example intercepted request:

GET /api/user?id=124 HTTP/1.1
Host: target.com
Cookie: session=abc123


Modify the ID: GET /api/user?id=125


If another user's data appears, an **IDOR vulnerability exists**.

---

## IDOR in Encoded IDs

Some applications attempt to hide identifiers by encoding them.

Example encoded ID: user=MTIz

This might be **Base64 encoded**.

Decoding: MTIz → 123


Attackers can decode the value, modify it, then re-encode it.

Example attack process:
Encoded: MTIz
Decoded: 123
Modify: 124
Re-encode: MTI0


Request becomes:
/profile?user=MTI0

If successful, the attacker accesses another account.

---

## IDOR in Hashed IDs

Applications sometimes hash identifiers to prevent enumeration.

Example: /user/5f4dcc3b5aa765d61d8327deb882cf99


These hashes may represent:
- MD5 hashes
- SHA hashes
- predictable tokens

Attackers may attempt:

- Hash cracking
- Hash generation
- Using known wordlists
- Observing patterns between users

If the hash is predictable or reversible, it may still be vulnerable to IDOR.

---

## IDOR in Unpredictable IDs

Some applications use **UUIDs or random tokens**.

Example: /download/7d9c2e98-8d23-4b71-bc54-4f6a2c8b31b1


These are harder to guess, but IDOR may still exist if:

- URLs are leaked
- tokens appear in logs
- predictable generation is used
- APIs expose references

Security should **not rely only on randomness**, but also enforce **authorization checks**.

---

## Identifying IDOR in APIs

Modern applications often expose APIs that reference resources by IDs.

Example API request:
GET /api/orders/4587
Authorization: Bearer <token>


If the user can modify the order ID: GET /api/orders/4588

and access another user's order, the API contains an **IDOR vulnerability**.

APIs are particularly vulnerable because:

- they rely heavily on identifiers
- developers may assume the client will enforce permissions

---

## Tools Useful for Finding IDOR

Common tools used during testing:

- Burp Suite
- OWASP ZAP
- Browser DevTools
- Postman
- FFUF (for endpoint discovery)

Burp Suite is particularly useful for:

- intercepting requests
- modifying parameters
- replaying requests

---

## Impact of IDOR Vulnerabilities

IDOR vulnerabilities can have severe consequences:

- Exposure of personal user data
- Unauthorized file downloads
- Account information leaks
- Financial data exposure
- Privilege escalation
- Regulatory compliance violations

In many real-world breaches, attackers exploited IDOR to **mass scrape user data**.

---

## Prevention & Mitigation

The most important defense is **proper server-side authorization checks**.

Best practices include:

- Validate ownership of requested objects
- Implement strict access control checks
- Avoid exposing direct object references
- Use indirect object references
- Log suspicious access attempts
- Perform regular security testing

+ Example secure validation logic:
if request.user_id != object.owner_id:
deny_access()


Security should **never rely solely on hidden or encoded IDs**.

---

## Key Security Takeaways

IDOR is one of the most common access control vulnerabilities in web applications. It occurs when applications expose direct references to internal objects without verifying user authorization. Attackers exploit this by modifying identifiers in requests to access unauthorized data. Proper server-side validation, strong access control mechanisms, and secure application design are essential to prevent IDOR vulnerabilities.

---

Room Completed: **IDOR (Insecure Direct Object Reference)**  
Focus Area: **Web Application Security | Access Control Vulnerabilities**