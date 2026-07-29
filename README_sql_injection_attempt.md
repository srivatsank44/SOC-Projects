# 🛡️ SQL Injection Attempt — DVWA Web Application

| Field | Value |
|---|---|
| Date of Analysis | July 27, 2026 |
| Analysed By | Srivatsan |
| Severity | Medium (lab/simulated environment) |
| Status | Contained — controlled lab exercise |
| Affected Asset | DVWA web application |
| Detection Tools | Wireshark, Splunk |

---

## 1. Executive Summary

- SQL injection attempt detected against `127.0.0.1` (Kali)
- Confirmed independently through Wireshark (network) and Splunk (logs)
- Conducted in an isolated lab against DVWA; no production systems or real data involved

---

## 2. Incident Timeline

- **18:14:19 – 18:14:30 UTC** — Repeated GET requests to `/vulnerabilities/sqli/`
- **18:14:30 UTC** — Payload `' OR '1'='1` submitted via the `id` parameter
- **18:14:30 UTC** — Server responded `200 OK` — request processed, not rejected
- **Post-incident** — Traffic captured in Wireshark; logs ingested and queried in Splunk

---

## 3. Indicators of Compromise (IOCs)

- **Source IP:** 172.17.0.1
- **Destination:** 127.0.0.1:80
- **HTTP Method:** GET
- **Target URI:** `/vulnerabilities/sqli/?id=%27+OR+%271%27%3D%271&Submit=Submit`
- **Payload (decoded):** `' OR '1'='1`
- **User-Agent:** Mozilla/5.0 (X11; Linux x86_64; rv:140.0) Gecko/20100101 Firefox/140.0
- **HTTP Response:** 200 OK

---

## 4. Network-Layer Analysis (Wireshark)

- Captured on loopback interface (`lo`), filtered with `http`
- Isolated the suspicious request from surrounding traffic
- Reconstructed full request/response via Follow HTTP Stream
- Payload sent as plain URL-encoded GET parameter, no obfuscation
- Server returned 200 OK — no input validation rejection

---

## 5. Log-Layer Analysis (Splunk)

Ingested the Apache access log into Splunk and used queries like `source=access_combined` to isolate the SQL injection request from normal traffic.

---

## 6. Correlation & Root Cause

Wireshark and Splunk logged the same event by timestamp, source, URI, and payload. Root cause: unsanitized input concatenated directly into the SQL query.

---

## 7. Impact Assessment

This payload can bypass authentication logic and, in production, could lead to unauthorized data access or database compromise.

---

## 8. Immediate Recommendations

Use parameterized queries, validate input server-side, and configure Splunk alerts for SQLi-pattern strings like `OR '1'='1` or `UNION SELECT`.

---

## 9. Future Prevention Strategy

Enforce secure coding standards (parameterized queries), deploy a WAF, apply least-privilege database accounts, and run regular scans and penetration tests.

---

## 10. Conclusion

Successfully identified and confirmed a SQL injection attack using both network-layer (Wireshark) and log-layer (Splunk) detection, reflecting a standard SOC investigation workflow.

---

## Screenshots

Wireshark packet capture, HTTP stream reconstruction, and Splunk log query screenshots are included in the `screenshots/` folder of this repository.
