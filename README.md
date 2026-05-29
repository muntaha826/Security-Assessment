# Cybersecurity Internship – Week 1: Security Assessment

## Overview
This repository contains the Week 1 security assessment performed on **OWASP Juice Shop**,
a purposely vulnerable web application used for cybersecurity learning and practice.

The goal was to explore the application, identify common web vulnerabilities using manual
testing and automated tools, and document all findings.

---

## Application Used
**OWASP Juice Shop**  
Access: `http://localhost:3000`  
Source: https://github.com/juice-shop/juice-shop

### Setup Commands
```bash
git clone https://github.com/juice-shop/juice-shop.git
cd juice-shop
npm install
npm start
```

---

## Tools Used
OWASP ZAP was used for automated vulnerability scanning.  
Browser DevTools were used for manual XSS and injection testing.  
Git Bash was used for application setup and navigation.

---

## Pages Explored
- Login page
- Signup page
- User profile page
- Search bar
- Contact and Feedback page

---

## Vulnerabilities Found

### 1. Cross-Site Scripting (XSS)
**Location:** Search bar and Contact page  
**Payload tested:** `<script>alert('XSS')</script>` which was blocked by the browser  
**Successful payload:** `<img src="on" onerror="alert('vulnerability found'">`  
**Result:** Alert popup confirmed JavaScript injection in the browser  
**Risk:** Cookie theft, session hijacking, page defacement, malicious redirects  
**Fix:** Sanitize inputs, escape HTML characters, implement Content Security Policy (CSP)

### 2. SQL Injection
**Location:** Login form email field  
**Payload used:** ' OR 1=1-- 
**Result:** Successfully bypassed authentication and logged in as Administrator  
**Risk:** Unauthorized access, database exposure, authentication bypass  
**Fix:** Use parameterized queries, avoid dynamic SQL, validate all inputs

### 3. Security Misconfigurations (via OWASP ZAP)
The automated scan identified the following issues: SQL Injection, Content Security Policy
Header Not Set, Missing Anti-Clickjacking Header, Cross-Domain Misconfiguration, Session ID
in URL Rewrite, Private IP Disclosure, Server Version Information Disclosure,
Strict-Transport-Security Header Not Set, X-Content-Type-Options Header Missing,
and Timestamp Disclosure.

**Fix:** Configure proper HTTP security headers, disable information disclosure,
use secure session handling.

---

## Screenshots
All screenshots are available in the screenshots folder.

---

## Key Takeaways
- Direct `<script>` tags are blocked by modern browsers; event-based payloads like `onerror` bypass this
- SQL injection via `' OR 1=1--` comments out the password check entirely, granting admin access
- Missing HTTP headers leave the application exposed to clickjacking, XSS, and information leakage
- Regular automated scanning with OWASP ZAP is essential for identifying misconfigurations
