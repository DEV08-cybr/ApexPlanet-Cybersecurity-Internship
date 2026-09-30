# ApexPlanet Cybersecurity Internship - Task 4: File Inclusion (LFI)

## 🎯 Objective
Identify, exploit, and document a Local File Inclusion (LFI) vulnerability within the Damn Vulnerable Web Application (DVWA) environment, culminating in Remote Code Execution (RCE) via vulnerability chaining.

---

## 🛠️ Methodology & Execution

1. **Environment Setup:**
   * Launched DVWA locally at `http://127.0.0.1:42001`.
   * Set security level to **Low** via the DVWA Security panel.

2. **Verifying Local File Inclusion (LFI):**
   * Navigated to the **File Inclusion** module in the sidebar.
   * Modified the `page` parameter in the URL bar to traverse directories and read system configuration files (such as `/etc/passwd`):
     ```text
     http://127.0.0.1:42001/vulnerabilities/fi/?page=../../../../etc/passwd
     ```

3. **Achieving Remote Code Execution (RCE) via Chaining:**
   * Targeted a previously uploaded server-side script (`shell.php`) located in the upload directory.
   * Passed system commands dynamically through the URL query parameter (`&cmd=`):
     ```text
     http://127.0.0.1:42001/vulnerabilities/fi/?page=../../hackable/uploads/shell.php&cmd=uname%20-a
     ```

---

##  Evidence & Screenshots to Attach
* ** <img width="1668" height="998" alt="image" src="https://github.com/user-attachments/assets/8f174084-1eb4-440a-86ff-4b39283aad14" /> ** Browser showing directory traversal output when accessing `http://127.0.0.1:42001/vulnerabilities/fi/?page=../../hackable/uploads/shell.php&cmd=id`.
* **<img width="1668" height="998" alt="image" src="https://github.com/user-attachments/assets/a10da8b6-d64a-4e24-97ff-6b46e436de78" />** Browser rendering the system kernel output (`Linux kali 6.19.14...`) via the chained LFI command execution payload.

---

## 🛡️ Remediation
* Implement strict input whitelisting for file inclusion parameters.
* Avoid passing user-supplied input directly into filesystem inclusion functions (`include()`, `require()`).
* Disable `allow_url_include` in the `php.ini` configuration.
