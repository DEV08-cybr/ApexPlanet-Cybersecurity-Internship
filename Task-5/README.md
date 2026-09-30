**Objective**

The goal of Task 5 is to demonstrate how insecure file upload mechanisms in web applications can be exploited. By bypassing basic input and extension validation filters, an attacker can upload a custom **PHP** webshell to the server and achieve Remote Code Execution (**RCE**) when chained with Local File Inclusion (**LFI**).

### Lab Environment

Target Application: Damn Vulnerable Web Application (**DVWA**)

Security Level: Low

Environment: Kali Linux (Attack Host) / Local Web Server (Target)

Step-by-Step Implementation

Creating the **PHP** Webshell A lightweight **PHP** script is crafted to accept command-line arguments via **HTTP** requests and execute them on the underlying operating system.

Note: Avoid complex escaping issues in Zsh by using a simple payload. Command: echo '' > shell.php

Uploading the Payload

Navigate to the File Upload module in **DVWA**.

Select the generated shell.php file.

Click Upload to push the script to the server's upload directory (../../hackable/uploads/shell.php successfully uploaded!)[cite: 4].

Executing Commands via Webshell / **LFI** Chaining Point the browser to the **LFI** path incorporating the uploaded webshell and append your target system commands[cite: 2, 3]:

Command uname -a: [suspicious link removed] -a

Command id: [suspicious link removed]

Important Notes & Troubleshooting

Zsh Syntax Errors: If you encounter parse errors when creating files via echo, use double quotes for internal attributes or switch to a cat << '**EOF**' block to prevent quote-escaping conflicts.

Path Verification: Always double-check the exact upload path reported by **DVWA** after uploading your script (../../hackable/uploads/shell.php)[cite: 4].

Security Settings: Ensure **DVWA** security is set to Low so that file extension validation checks do not block the **PHP** payload upload.

Screenshots / Evidence

### File Upload Success

Image: <img width="1668" height="998" alt="image" src="https://github.com/user-attachments/assets/78814929-b4f6-4aa8-84fe-74b44737deea" />


Command Execution (uname -a) Image: <img width="1668" height="998" alt="image" src="https://github.com/user-attachments/assets/e875e6c9-e9cb-49b0-9126-8b554cb82d34" />


Command Execution (id) Image: <img width="1668" height="998" alt="image" src="https://github.com/user-attachments/assets/e6a5f22e-4208-420b-8cc4-787ad9c60685" />


Mitigation & Security Recommendations

Extension Whitelisting: Restrict uploaded files strictly to safe extensions (e.g., .jpg, .png) rather than relying on blacklist filters or client-side checks.

Storage Isolation: Store uploaded assets outside of the web root directory or on a dedicated static content server to prevent direct script execution.

File Renaming: Automatically rename uploaded files with cryptographic hashes to prevent direct referencing and execution of uploaded scripts.
