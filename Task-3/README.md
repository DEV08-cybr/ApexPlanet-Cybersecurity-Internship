# Task-3: Web Application Security

## Overview
- **Objective:** Identify and exploit OWASP Top 10 vulnerabilities in a controlled lab environment (DVWA).
- **Scope:** SQL Injection, Cross-Site Scripting (XSS), and mitigation strategies.

---

## 1. SQL Injection (SQLi)

### Attack Scenario
* **Target Module:** DVWA SQL Injection
* **Method:** Tested input validation by injecting a single quote (`'`) into the vulnerable user ID parameter.
* **Observation:** The application returned a `500 Internal Server Error`, confirming that the input was concatenated directly into the backend database query without proper sanitization, triggering a database syntax crash.

### Screenshot
<img width="1668" height="998" alt="image" src="https://github.com/user-attachments/assets/eda8d2a5-00c1-4156-8f2c-c80bdc799efe" />

<img width="1668" height="998" alt="image" src="https://github.com/user-attachments/assets/ccc17d05-9a19-4361-9d62-46bda3e8f5dc" />

<img width="1668" height="998" alt="image" src="https://github.com/user-attachments/assets/07f1eeb8-73c1-4842-b937-ebf9463b12f6" />



### Mitigation
* **Prepared Statements (Parameterized Queries):** Ensure user input is treated strictly as data, never as executable code.
* **Input Validation:** Implement strict allow-lists for expected data types.

---

## 2. Cross-Site Scripting (XSS)

# Deep Dive: Cross-Site Scripting (XSS)

Cross-Site Scripting (XSS) is a common web application vulnerability that occurs when an application includes untrusted user input in a web page without proper validation or encoding. This allows attackers to execute malicious scripts (typically JavaScript) in the victim's browser context.

## Types of XSS

* **Reflected (Non-Persistent) XSS:** The malicious script comes from the current HTTP request (often via a URL parameter) and is reflected back immediately by the server in the response[cite: 1].
* **Stored (Persistent) XSS:** The malicious script is permanently saved on the target server (e.g., in a database, comment section, or user profile) and executed automatically whenever a user visits the affected page[cite: 1].
* **DOM-Based XSS:** The vulnerability exists entirely in client-side JavaScript, where untrusted data from the browser environment is written insecurely into the Document Object Model (DOM).

---

## Lab Demonstration (DVWA)

In your internship security testing, XSS is explored within a controlled lab environment using DVWA[cite: 1]:
* **Test Payload:** `<script>alert('XSS Test')</script>`
* **Behavior:** Instead of treating the input as plain text, a vulnerable application renders and executes the script, triggering an alert pop-up box in the user's browser.
---
### screenshots

<img width="1668" height="998" alt="image" src="https://github.com/user-attachments/assets/c3c850a4-2047-4832-9c43-de45772e182d" />

<img width="1668" height="998" alt="image" src="https://github.com/user-attachments/assets/972aa321-6d81-49bb-8163-9ed561cef042" />

---


## Mitigation & Prevention Strategies

* **Input Validation:** Implement strict allow-lists and check user inputs against expected formats before processing.
* **Output Encoding:** Convert special characters (such as `<`, `>`, `&`, and quotation marks) into safe HTML entities so the browser displays them as text rather than running them as code.
* **Content Security Policy (CSP):** Deploy strong HTTP response headers to restrict the sources from which scripts can be loaded and block unauthorized inline script execution[cite: 1].

### Attack Scenario
* **Target Module:** DVWA Reflected XSS
* **Payload Used:** 
  ```html
  <script>alert('XSS Test')</script>
  ---

