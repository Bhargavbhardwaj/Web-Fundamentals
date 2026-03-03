# TryHackMe – Content Discovery Notes

## 📌 Introduction

In web application security, **content** can include:
- Files
- Images / Videos
- Backup files
- Config files
- Admin panels
- Staff portals
- Old versions of websites

**Content Discovery** = Finding hidden or unlinked resources that are not directly visible and may not be intended for public access.

### Three Main Methods:
1. Manual
2. Automated
3. OSINT (Open-Source Intelligence)

---

## 🧭 Manual Discovery

### 1️⃣ robots.txt
Location: 
- Tells search engines what not to crawl
- Does NOT restrict access
- May expose:
  - `/admin/`
  - `/backup/`
  - `/internal/`

---

### 2️⃣ Favicon
Location:
- Small browser tab icon
- Can be hashed and fingerprinted
- Helps identify:
  - CMS
  - Framework
  - Backend tech

---

### 3️⃣ sitemap.xml
Location:
- Lists site URLs for search engines
- May reveal:
  - Hidden pages
  - Old endpoints
  - Staging URLs
  - Admin paths

---

### 4️⃣ HTTP Headers

View via:
- Browser DevTools → Network
- `curl -I <url>`

Important headers:
- `Server`
- `X-Powered-By`
- `Set-Cookie`
- `Content-Security-Policy`

Used for:
- Tech stack identification
- Detecting misconfigurations

---

### 5️⃣ Framework Stack Identification

Clues:
- `/wp-admin` → WordPress
- `.php` → PHP
- `.aspx` → ASP.NET
- `/static/` → Django

Purpose:
- Identify technologies
- Research known vulnerabilities

---

## 🤖 Automated Discovery

Uses wordlists to brute-force directories/files.

Common Tools:
- gobuster
- dirb
- ffuf
- dirsearch

Finds:
- Hidden directories
- Backup files
- Unlinked endpoints

---

## 🔎 OSINT Techniques

### 1️⃣ Google Dorking

Operators:
- `site:`
- `filetype:`
- `intitle:`
- `inurl:`

Examples:
Finds:
- Exposed files
- Login portals
- Open directories

---

### 2️⃣ Wappalyzer

- Browser extension
- Detects:
  - CMS
  - Frameworks
  - Analytics
  - Programming languages

Used for tech fingerprinting.

---

### 3️⃣ Wayback Machine

Website:
Used to find:
- Old versions
- Removed pages
- Deprecated endpoints
- Previously exposed content

---

### 4️⃣ GitHub OSINT

Search for:
May reveal:
- API keys
- Hardcoded credentials
- Source code leaks
- Config files

---

## 🔐 Key Takeaways

- Always check: `robots.txt`, `sitemap.xml`, headers
- Combine Manual + Automated + OSINT
- Tech fingerprinting improves attack strategy
- Many breaches start with simple content discovery

---

✅ Room Completed: Content Discovery
AUTHOR - Bhargav Bhardwaj