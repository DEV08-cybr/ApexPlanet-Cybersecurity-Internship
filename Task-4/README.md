
# Task 4: Local File Inclusion (LFI) Exploitation

## 1. Overview
The objective of this task is to identify and exploit a **Local File Inclusion (LFI)** vulnerability within the Damn Vulnerable Web Application (DVWA) environment. LFI vulnerabilities occur when an application improperly includes user-supplied input without adequate sanitization, allowing an attacker to read sensitive files on the local server.

---

## 2. Environment Setup & Configuration
* **Target Environment**: DVWA (Damn Vulnerable Web Application) hosted locally at `http://127.0.0.1/DVWA/`
* **Security Level**: Configured to **Low** (to allow direct parameter manipulation without strict input validation filters).
* **Operating System**: Kali Linux

---

## 3. Step-by-Step Execution

### Step 1: Navigate to the Vulnerability Module
1. Log into the DVWA dashboard using your credentials (`admin / password`).
2. Navigate to the **File Inclusion** tab from the left-hand navigation menu.
3. Observe the URL structure, which typically looks like:
   `http://127.0.0.1/DVWA/vulnerabilities/fi/?page=include.php`

> <img width="1668" height="998" alt="image" src="https://github.com/user-attachments/assets/9a3e9104-946f-4c6e-b187-84812a4bf0ab" />


### Step 2: Test for Path Traversal
To test if the application is vulnerable to LFI, modify the `page` parameter in the URL to traverse directories and access system files (such as `/etc/passwd` on Linux systems).
<img width="1668" height="998" alt="image" src="https://github.com/user-attachments/assets/35e50b4e-319a-4238-afd0-60ff326a9d48" />

### step 3: veiw of source code of `ect/passwd`
<img width="1668" height="998" alt="image" src="https://github.com/user-attachments/assets/070c3780-dc01-447c-a63a-ed4f768b3325" />

* **Command / URL Payload:**
  ```text
  [http://127.0.0.1/DVWA/vulnerabilities/fi/?page=../../../../etc/passwd](http://127.0.0.1/DVWA/vulnerabilities/fi/?page=../../../../etc/passwd)
