# Task 3: Web Application Security

## Overview
- **Timeline:** Days 25-36
- **Objective:** Identify and exploit OWASP Top 10 vulnerabilities in a controlled lab environment (DVWA).

---

## 1. SQL Injection (SQLi)
- **Target:** DVWA SQL Injection module.
- **Exploitation:** Extracted database version, table names, and user credentials using payload injection (' OR '1'='1).
- **Mitigation:** Implemented Parameterized Queries / Prepared Statements.

---

## 2. Cross-Site Scripting (XSS)
- **Stored XSS:** Injected persistent JavaScript payloads into comment fields executing code on page load[cite: 1].
- **Reflected XSS:** Passed malicious scripts via URL query parameters[cite: 1].
- **Mitigation:** Applied strict input sanitization, output encoding, and Content Security Policy (CSP) headers[cite: 1].

---

## 3. Cross-Site Request Forgery (CSRF) & File Inclusion
- **CSRF:** Simulated password modification attacks without user consent and enforced anti-CSRF tokens[cite: 1].
- **File Inclusion:** Tested Local File Inclusion (LFI) to read /etc/passwd and explored Remote File Inclusion vectors[cite: 1].

---

## 4. Burp Suite & Security Headers
- **Burp Suite:** Captured, intercepted, and modified HTTP login requests; used Intruder for parameter fuzzing[cite: 1].
- **Security Headers:** Evaluated test applications using securityheaders.com and hardened Apache configuration[cite: 1].
