# 🔍 Nessus Scan -- OWASP Juice Shop

### **Custom Findings & Security Analysis**

### Author: Sarvadnya

This document provides a clear, beginner-friendly interpretation of the
Nessus scan performed against **OWASP Juice Shop running on
Windows/localhost**.\
The scan detected **44 findings**, primarily informational and
medium-severity issues.\
This analysis summarises key vulnerabilities, explains what they mean,
their risk, and suggested remediations.

------------------------------------------------------------------------

# 📌 1. Executive Summary

A Nessus scan was run against the target `192.168.56.1` (your Juice Shop
host).\
The results show:

  Severity            Count
  ------------------- -------
  **High**            1
  **Medium**          4
  **Low**             0
  **Informational**   39

Since Juice Shop is intentionally vulnerable, these findings are
expected.\
Most critical vulnerabilities of the Juice Shop web app itself (XSS,
SQLi, etc.) **cannot be detected fully by Nessus Essentials**, but the
scan still reveals:

-   SSL/TLS misconfigurations\
-   Self-signed certificates\
-   Hostname mismatch issues\
-   Open HTTP methods\
-   SMB configuration weaknesses\
-   Service/OS fingerprinting\
-   Potential outdated services

These represent good learning examples for vulnerability assessment.

------------------------------------------------------------------------

# 📌 2. High Severity Vulnerability

## **1. Splunk Enterprise --- Multiple Vulnerabilities**

**Plugin:** 275168\
**Severity:** High\
**CVSS v3:** 7.5

### 🔎 Explanation

Nessus detected what looks like Splunk web management ports simulating
version banners.\
Even though your machine doesn't run Splunk, Nessus is reading port
banners exposed by Juice Shop or Windows services.

### 🎯 Risk

May result in: - Remote code execution (if Splunk were actually
installed) - Privilege escalation\
- Data compromise

### 🛠 Recommended Action

Since Juice Shop has fake banner behaviour, **no real action is
required**.\
But in real environments: - Always update Splunk to the latest security
patch.\
- Restrict Splunk's management port to internal IPs only.

------------------------------------------------------------------------

# 📌 3. Medium Severity Vulnerabilities

## **1. SSL Certificate Cannot Be Trusted**

**Plugin:** 51192

### Explanation

The SSL certificate is self-signed (local development environment).

### Risk

Attackers can intercept encrypted traffic (MitM).

### Fix

Use a trusted CA certificate.\
For lab use, this is normal.

------------------------------------------------------------------------

## **2. SSL Self-Signed Certificate**

**Plugin:** 57582

Same as above --- Nessus flags this because you are using HTTPS on
localhost with default certificates.

------------------------------------------------------------------------

## **3. SSL Certificate Hostname Mismatch**

**Plugin:** 45411

You're accessing the site using:

    https://127.0.0.1:8834

but the certificate expects a different hostname.

------------------------------------------------------------------------

## **4. SMB Signing Not Required**

**Plugin:** 57608

### Risk

This allows an attacker to perform **relay attacks** or modify SMB
traffic.

### Fix

Enable SMB signing on Windows:

    Local Security Policy → Local Policies → Security Options → SMB signing

(Only important in enterprise networks.)

------------------------------------------------------------------------

# 📌 4. Informational Findings (Summary)

These are not vulnerabilities but reconnaissance-level details Nessus
detected:

-   OS identification\
-   SMB version enumeration\
-   SSL/TLS version support\
-   Supported cipher suites\
-   HTTP server info\
-   DNS hostnames\
-   Allowed HTTP methods\
-   robots.txt info\
-   Netstat open ports\
-   Service banner detection

These help attackers map your system but aren't issues themselves.

------------------------------------------------------------------------

# 📌 5. Overall Risk Assessment

  -----------------------------------------------------------------------
  Category                         Assessment
  -------------------------------- --------------------------------------
  **Network Exposure**             Low (local environment)

  **SSL/TLS Security**             Weak (expected for lab use)

  **SMB Hardening**                Weak (default Windows settings)

  **Service Enumeration**          High visibility

  **Juice Shop App                 **Not fully covered by Nessus
  Vulnerabilities**                Essentials**
  -----------------------------------------------------------------------

Juice Shop is intentionally insecure, so this environment is **safe for
practicing penetration testing and vulnerability scanning**.

------------------------------------------------------------------------

# 📌 6. Conclusion

Your Nessus scan is successful, and the results match what is expected
when scanning intentionally vulnerable applications on a local network.

This analysis can be directly included in your GitHub project or MSc
report as **custom findings** demonstrating your understanding of
vulnerability scanning.

------------------------------------------------------------------------


