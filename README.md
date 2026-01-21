# 🔐 Web Application Security Testing Lab  
### SQL Injection & Cross-Site Scripting (XSS) – Manual Testing with Burp Suite

## 📌 Project Overview

This project is a **locally hosted, intentionally vulnerable web application** built to simulate a **real-world web application penetration test**.  
The goal was to **manually identify, validate, and document SQL Injection (SQLi) and Cross-Site Scripting (XSS) vulnerabilities** using **Burp Suite Community Edition**, following realistic penetration testing methodology.

The application runs **entirely on localhost**, demonstrating that professional security testing tools like Burp Suite can be used **offline against local development environments**, just as they are used against production systems.

---

## 🎯 Objectives

- Build a custom web application using **Flask + SQLite**
- Intercept and analyze HTTP traffic using **Burp Suite**
- Perform **manual SQL Injection testing** against authentication logic
- Perform **manual XSS testing** against reflected user input
- Correctly identify **true vulnerabilities vs false positives**
- Document findings in a **professional pentest-style format**
- Create a **portfolio-ready security project** for recruiters

---

## 🛠️ Technologies & Tools

### Application Stack
- Python 3
- Flask (Web Framework)
- SQLite (Database)
- HTML (Jinja2 Templates)

### Security Testing Tools
- **Burp Suite Community Edition**
  - Proxy
  - HTTP History
  - Repeater
- Firefox (Configured to proxy traffic through Burp)

---

## 🧱 Application Structure

Local-Vulnerable-App/
│

├── app.py

├── users.db

├── templates/

│ ├── login.html

│ ├── dashboard.html

│ └── search.html
└── README.md


---

## 🌐 Test Environment

- Application URL: http://127.0.0.1:5000

- Burp Proxy: 127.0.0.1:8080
 
  - All traffic manually intercepted and modified
- No automated scanners used

---

## 🔍 Testing Methodology

This project follows a **manual web application penetration testing workflow**, similar to real assessments:

1. Intercept requests using Burp Proxy  
2. Identify user-controlled parameters  
3. Send requests to Burp Repeater  
4. Modify parameters manually  
5. Analyze server responses  
6. Validate exploitability  
7. Document findings accurately  

---

## 💉 SQL Injection Testing

### Target
- Login endpoint (`POST /`)
- Parameters:
- `username`
- `password`

### Process

- Intercepted login requests via Burp Proxy
- Sent captured requests to **Burp Repeater**
- Manually injected SQL payloads into parameters

Example payloads tested:

' OR '1'='1


admin' --


' OR 1=1 --


### Observations

- Application behavior changed based on injected input
- Authentication logic did not properly sanitize user input
- Indicates **SQL Injection vulnerability** in login handling

### Impact

- Authentication bypass possible
- Unauthorized access to application
- Potential exposure of sensitive data

---

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 🧪 Cross-Site Scripting (XSS) Testing

### Target
- Search functionality (  GET /search?q=  )

### Payload Tested

" <script>alert(1)</script> "



### Server Response Analysis

The payload was reflected in the HTML response as:


&lt;script&gt;alert(1)&lt;/script&gt;

### Payload Tested

" <b > hello < /b> "

### Server Response Analysis

The payload was reflected in the HTML response as:

 &lt ;b& gt;hello& lt;/b &g t;

Conclusion

User input is reflected, but properly HTML-encoded

JavaScript does not execute

Browser renders payload as text

Final Verdict

✅ No exploitable XSS vulnerability present
❌ No script execution possible

Classification:

Reflected input present, but XSS mitigated via output encoding

Risk Level: Informational

This demonstrates correct handling of user input and highlights the importance of distinguishing false positives during security testing.


🔐 Security Impact Summary

| Vulnerability | Status          | Risk          |
| ------------- | --------------- | ------------- |
| SQL Injection | Confirmed       | High          |
| Reflected XSS | Not exploitable | Informational |

🛡️ Mitigation Recommendations
SQL Injection

Use parameterized queries / prepared statements

Avoid string-based SQL query construction

Validate and sanitize all user input

XSS

Continue using output encoding

Avoid rendering raw user input

Implement Content Security Policy (CSP)

📸 Evidence

Screenshots were captured during:

HTTP request interception

Repeater-based parameter manipulation

SQL Injection payload testing

XSS response analysis

(Screenshots to be added to /screenshots directory)

📈 Skills Demonstrated

Manual web application penetration testing

Burp Suite Proxy & Repeater proficiency

SQL Injection exploitation

XSS testing & false-positive analysis

HTTP protocol analysis

Secure coding awareness

Professional security documentation

##🚀 Why This Project Matters

This project demonstrates:

Realistic pentesting workflow (no automation shortcuts)

Understanding of both offensive and defensive security

Ability to explain why a vulnerability does or does not exist

Portfolio-level security thinking suitable for junior roles

⚠️ Disclaimer

All testing was performed only on a locally hosted application created for learning purposes.
No unauthorized testing was conducted against real-world systems.

👤 Author

Sandiso
Aspiring Cybersecurity & Web Application Security Professional

