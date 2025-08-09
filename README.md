## Project Objective
Perform a web security audit and penetration testing workflow using OWASP ZAP to identify common web vulnerabilities (SQL Injection, Cross-Site Scripting (XSS), CSRF, insecure methods, etc.). All testing was done only on intentionally vulnerable test environments.

> **Important:** Live testing of Internee.pk was not performed because explicit permission was not received; all tests were conducted on safe, intentionally vulnerable environments.

## Tools used
- **OWASP ZAP v2.16.1** — Automated scanner & manual inspection.  
- **Firefox** — Browser configured to proxy through ZAP (127.0.0.1:8080).  
- **testphp.vulweb.com** — Primary test target (deliberately vulnerable).  

---

## Summary of Actions
1. Configured Firefox to use ZAP proxy (`127.0.0.1:8080`).  
2. Imported ZAP root certificate into Firefox to inspect HTTPS (if required).  
3. Browsed the target application to populate ZAP’s Site tree.  
4. Performed an **Active Scan** from ZAP on captured target URLs.  
5. Reviewed alerts, examined request/response evidence, and exported HTML report.  
6. Prepared remediation recommendations for each finding.

---

## Findings (high level)
- **Cross-Site Scripting (Reflected)** — 1 alert  
  - Impact: Client-side code execution, cookie/session theft.  
  - Recommendation: Properly escape/sanitize user-supplied output, use CSP headers.

- **SQL Injection** — 2 alerts (MySQL & SQLite)  
  - Impact: Unauthorized DB access/modification.  
  - Recommendation: Use parameterized queries / prepared statements, input validation.

- **GET for POST** — 1 alert  
  - Impact: Sensitive data exposure in URLs / logs.  
  - Recommendation: Use POST for state-changing operations, avoid sending sensitive info in URL.

- **User Agent Fuzzer** — multiple informational outputs  
  - Impact: Server behavior may vary by UA; may leak information.  
  - Recommendation: Normalize responses and log/handle user agent data safely.

> Note: No CSRF was detected during this assessment.

## Ethics & Permissions
All testing was carried out only on intentionally vulnerable test environments. No testing was performed on Internee.pk’s production or staging systems because explicit permission was not received.

