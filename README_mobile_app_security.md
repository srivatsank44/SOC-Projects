# 📱 Mobile App Security Report

**App Analyzed:** Clone Master – Multi Dual Space (`com.cmaster.cloner`)
**Tool Used:** [MobSF (Mobile Security Framework)](https://github.com/MobSF/Mobile-Security-Framework-MobSF)

---

## 1. Key Metrics

This app scored **49 out of 100** for security — a medium-to-high risk level. It has problems like unencrypted internet traffic, too many risky permissions, and code that tries to hide from testing tools.

| What I Checked | Result |
|---|---|
| Security Score | 49 / 100 |
| Trackers Found | 1 |
| Serious (High) Problems | 1 |
| Medium (Warning) Problems | 7 (below) |
| Info-Only Notes | 2 |
| Risky Permissions Matched to Malware | 18 out of 25 |

---

## 2. Scope & Methodology

- Assessed the Clone Master Android application (11.77 MB)
- Performed static analysis using MobSF via Docker
- Code examined without execution; no runtime testing performed

---

## 3. Findings & Recommendations

- **Cleartext traffic enabled** — enforce HTTPS across all connections
- **Application backups enabled** — disable to prevent data extraction
- **Exported service lacks proper protection** — restrict access
- **Insecure random number generator in use** — implement a secure alternative
- **SQL injection risk identified** — use parameterized queries
- **Hardcoded credentials possible** — remove from source code
- **Sensitive files stored in external storage** — migrate to private storage
- **FORTIFY compiler protection missing** — enable in native build
- **Sensitive data written to logs** — remove prior to release

---

## 4. Permissions & Behavioral Analysis

- Requests high-risk permissions beyond stated app functionality
- Establishes network connections to remote servers
- Capable of launching external actions such as web pages or phone calls

---

## 5. Network & Infrastructure

- Communicates with servers hosted in the United States
- All contacted domains returned a clean security status
- No communication with sanctioned countries identified

---

## 6. Risk Rating

**Overall risk level: Medium-High**

---

## 7. Conclusion

- No malicious payload confirmed through static analysis alone
- Risk indicators warrant further dynamic analysis and manual review
- Not recommended for deployment without additional vetting

---

## 8. Tools & References

- [MobSF (Mobile Security Framework)](https://github.com/MobSF/Mobile-Security-Framework-MobSF)
- [OWASP Mobile Top 10](https://owasp.org/www-project-mobile-top-10/)
- [CWE (Common Weakness Enumeration)](https://cwe.mitre.org/)

---

## 9. How This Can Be Prevented in the Future

To prevent this in the future, the app just needs to follow basic security habits: encrypt data, ask for fewer permissions, protect stored files, and get scanned for issues before it's released.

---

## Screenshots

Analysis screenshots (MobSF dashboard, manifest/code findings, permissions, behavior analysis, etc.) are included in the `screenshots/` folder of this repository.
