# Race Condition

![Platform](https://img.shields.io/badge/Platform-TryHackMe-red)
![Category](https://img.shields.io/badge/Category-Web%20Security-blue)
![Focus](https://img.shields.io/badge/Focus-Race%20Condition%20%7C%20Concurrency%20Exploitation-green)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

Race conditions are a class of vulnerabilities that arise when the **timing or order of execution of multiple operations affects the final result of a program**. These vulnerabilities commonly occur in systems where multiple threads or processes attempt to **access or modify shared resources simultaneously without proper synchronization**. In web applications, race conditions often appear when the backend performs **critical checks and updates separately**, allowing attackers to send multiple requests at nearly the same time to bypass restrictions. This can lead to scenarios where an attacker **redeems a coupon multiple times, withdraws more money than available, bypasses payment checks, or triggers logic flaws in financial systems**.

Understanding race conditions requires familiarity with **threads, multi-threading behavior, application state transitions, and web application architectures**. Attackers exploit the small time window between validation and state update operations, commonly known as the **Time-of-Check to Time-of-Use (TOCTOU)** problem.

---

## Multi-Threading

Multi-threading refers to the ability of a program to execute **multiple sequences of instructions concurrently**. Each thread runs independently but may access shared memory or resources.

Key characteristics of multi-threading include improved performance, the ability to handle multiple user requests simultaneously, efficient CPU utilization, and the potential introduction of synchronization issues when shared resources are accessed incorrectly.

## Example conceptual scenario:

```text
Thread 1: Check account balance
Thread 2: Check account balance
Thread 1: Deduct money
Thread 2: Deduct money

If both threads read the same balance before deduction occurs, the system may incorrectly allow two withdrawals even though the balance only allows one. In web applications this situation commonly occurs when servers process multiple HTTP requests simultaneously

POST /withdraw
POST /withdraw

If the application processes both requests before updating the database, the attacker may successfully withdraw money twice.

## Race Condition Vulnerability

A race condition occurs when two or more operations compete to execute first, and the outcome of the system depends on the order in which they complete. These vulnerabilities are especially dangerous in systems that rely on validation followed by state updates.

Common scenarios where race conditions occur include:
Financial transactions
Discount or coupon redemption
Inventory purchase systems
Password reset mechanisms
API request processing
Token generation workflows

## Web Application Architecture and Race Conditions

Most modern web applications follow a layered architecture where requests move through several components before reaching the database.

Typical structure:

Client (Browser)
       ↓
Web Server
       ↓
Application Logic
       ↓
Database

Race conditions commonly occur between application logic and database operations when multiple requests are processed at the same time.

Example scenario:
User submits payment request
Server checks account balance
Server approves transaction
Database updates the balance

If an attacker sends multiple simultaneous requests, steps 2 and 4 may overlap, resulting in incorrect account states.
Race conditions are also more common in microservices architectures, asynchronous APIs, and distributed systems where services communicate independently.

---- Exploiting Race Conditions

Attackers exploit race conditions by sending multiple simultaneous requests to the same endpoint in order to trigger the vulnerable logic before the system updates its internal state.

Typical targets include:
Coupon redemption systems
Payment APIs
Gift card redemption endpoints
Banking withdrawal functions
Inventory purchase endpoints

>>>>> Exploiting Race Conditions with Burp Suite Repeater

A common technique for testing race conditions involves using Burp Suite Repeater to send multiple requests concurrently.

Typical workflow:
Capture the request using Burp Proxy
Send the request to Burp Repeater
Duplicate the request multiple times
Send the requests simultaneously

If multiple identical requests are executed at the same moment, the backend may process them before updating the user's account balance.
Advanced attackers may use automation tools to generate large numbers of concurrent requests.

import requests
import threading
url = "https://target.com/withdraw"

def send_request():
    requests.post(url, json={"amount":100})

for i in range(20):
    threading.Thread(target=send_request).start()

Detecting Race Conditions

Race conditions can be difficult to detect because they depend heavily on timing and concurrency behavior. Security testers typically identify them through stress testing or concurrent request testing.

Common detection methods include:
Sending parallel requests to critical endpoints
Stress testing API operations
Monitoring inconsistent responses
Reviewing application logs
Performing concurrency testing

Useful tools include:
Burp Suite Repeater
Burp Intruder
Turbo Intruder
Custom scripts
Apache Benchmark    

>>>>Key Security Takeaways

Race condition vulnerabilities occur when systems fail to properly manage concurrent operations on shared resources. Attackers exploit timing gaps between validation and state updates to manipulate application logic. Detecting race conditions involves sending parallel requests to sensitive endpoints and observing unexpected behavior. Effective mitigation requires implementing atomic transactions, proper locking mechanisms, concurrency-safe code, and request validation techniques.

These vulnerabilities are particularly critical in financial systems, payment gateways, coupon redemption platforms, and API-driven applications, where business logic flaws can lead to significant financial loss or system abuse.

Room Completed: Race Condition
Focus Area: Web Application Security, Concurrency Exploitation, Burp Suite Testing