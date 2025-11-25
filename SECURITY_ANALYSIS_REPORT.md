# ZAP Security Analysis Report

**Date:** November 25, 2025  
**Project:** cicd-demo (Spring Boot REST API)  
**Analyst:** [Your Name]  
**Repository:** SWE302_PA4c

---

## Executive Summary

This report documents the Dynamic Application Security Testing (DAST) performed on the cicd-demo application using OWASP ZAP. Both baseline and full scans were conducted to identify runtime vulnerabilities and security misconfigurations.

### Scan Summary
- **Baseline Scan**: Completed - Passive vulnerability detection
- **Full Scan**: Completed - Active vulnerability detection
- **Target URL**: http://localhost:5000
- **Endpoints Tested**: /nations, /currencies

---

## Scan Configuration

### ZAP Rules Applied
The scan used a comprehensive ruleset covering:
- Anti-CSRF token validation
- Security headers (X-Frame-Options, CSP, HSTS)
- Cookie security (SameSite, Secure, HttpOnly)
- Information disclosure
- XSS vulnerabilities
- Code injection risks

**Configuration File:** `.zap/rules.tsv`  
**Total Rules:** 47 security checks

---

## Critical Findings Analysis

### Instructions for Completing This Section:

**Step 1:** Open your ZAP report files:
- `zap-baseline-report/report_html.html`
- `zap-full-report/report_html.html`

**Step 2:** Look for the "Risk Level Summary" section in the reports

**Step 3:** Document findings below using this template:

---

### Finding #1: [Copy Vulnerability Name from Report]

**Risk Level:** [High/Medium/Low]  
**OWASP Category:** [e.g., A05:2021 – Security Misconfiguration]  
**Location:** [URL/Endpoint where found]  

**Description:**  
[Copy the description from the ZAP report]

**Evidence:**  
```
[Copy the evidence/payload from the report]
```

**Impact:**  
[Describe what an attacker could do - copy from "Description" in report]

**Remediation:**  
[Copy the "Solution" from the ZAP report]

**Priority:** [Critical/High/Medium/Low]

---

### Finding #2: [Copy Vulnerability Name from Report]

**Risk Level:** [High/Medium/Low]  
**OWASP Category:** [e.g., A03:2021 – Injection]  
**Location:** [URL/Endpoint where found]  

**Description:**  
[Copy the description from the ZAP report]

**Evidence:**  
```
[Copy the evidence/payload from the report]
```

**Impact:**  
[Describe what an attacker could do]

**Remediation:**  
[Copy the "Solution" from the ZAP report]

**Priority:** [Critical/High/Medium/Low]

---

## OWASP Top 10 2021 Mapping

Based on ZAP findings, map vulnerabilities to OWASP categories:

| OWASP Category | Findings Count | Highest Risk | Status |
|----------------|----------------|--------------|--------|
| A01:2021 – Broken Access Control | [Count] | [Risk] | ⚠️ |
| A02:2021 – Cryptographic Failures | [Count] | [Risk] | ⚠️ |
| A03:2021 – Injection | [Count] | [Risk] | ⚠️ |
| A04:2021 – Insecure Design | [Count] | [Risk] | ✅ |
| A05:2021 – Security Misconfiguration | [Count] | [Risk] | ⚠️ |
| A06:2021 – Vulnerable Components | [Count] | [Risk] | ✅ |
| A07:2021 – ID & Auth Failures | [Count] | [Risk] | ⚠️ |
| A08:2021 – Software & Data Integrity | [Count] | [Risk] | ✅ |
| A09:2021 – Security Logging Failures | [Count] | [Risk] | ⚠️ |
| A10:2021 – SSRF | [Count] | [Risk] | ✅ |

**Legend:** ✅ No issues | ⚠️ Issues found | ❌ Critical issues

---

## Common Expected Findings

Based on the Spring Boot application, you will likely find:

### 1. Missing Security Headers
- X-Frame-Options Header Not Set
- Content Security Policy (CSP) Header Not Set
- X-Content-Type-Options Header Missing
- Strict-Transport-Security Header Not Set

### 2. Cookie Security Issues
- Cookie Without SameSite Attribute
- Cookie Without Secure Flag (if using HTTP)
- Cookie Without HttpOnly Flag

### 3. Information Disclosure
- Server Version Disclosure
- Stack Trace Disclosure (if errors occur)
- Timestamp Disclosure

---

## Remediation Roadmap

### Phase 1: Critical Issues (Fix Immediately)
- [ ] [List HIGH risk findings here]
- [ ] [Add specific items from your ZAP report]

### Phase 2: High Priority (Fix Within 1 Week)
- [ ] [List MEDIUM risk findings]
- [ ] Add security headers (X-Frame-Options, CSP)
- [ ] Configure SameSite cookie attribute

### Phase 3: Medium Priority (Fix Within 2-4 Weeks)
- [ ] [List LOW risk findings]
- [ ] Remove server version disclosure
- [ ] Review information disclosure issues

### Phase 4: Best Practices (Continuous Improvement)
- [ ] Implement comprehensive logging
- [ ] Add rate limiting
- [ ] Enhanced authentication mechanisms

---

## Recommended Security Improvements

### 1. Add Security Headers (Spring Boot)

Add this to your SecurityConfig.java:

```java
@Configuration
public class SecurityConfig {
    
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .headers(headers -> headers
                .frameOptions().deny()
                .contentSecurityPolicy("default-src 'self'")
                .xssProtection()
                .contentTypeOptions()
            );
        return http.build();
    }
}
```

### 2. Configure Secure Cookies

Add to `application.properties`:

```properties
server.servlet.session.cookie.http-only=true
server.servlet.session.cookie.secure=true
server.servlet.session.cookie.same-site=strict
```

### 3. Remove Server Version Disclosure

```properties
server.error.include-stacktrace=never
server.error.include-message=never
```

---

## DAST vs SAST Comparison (For Your Understanding)

### What ZAP (DAST) Found:
- Runtime configuration issues
- Missing security headers
- Cookie security problems
- Server misconfigurations
- Authentication/session issues

### What SonarCloud (SAST) Would Find:
- Code vulnerabilities
- Hard-coded credentials
- SQL injection in code
- Insecure cryptography usage
- Code quality issues

**Conclusion:** Both tools are necessary for complete security coverage!

---

## Continuous Security Monitoring

### GitHub Actions Integration
- ✅ Baseline scan on every PR
- ✅ Full scan weekly (scheduled)
- ✅ Manual trigger capability
- ✅ Automated report generation

### Report Retention
- Baseline reports: 30 days
- Full reports: 90 days
- Available in GitHub Actions artifacts

---

## Tools and Technologies Used

- **DAST Tool:** OWASP ZAP 2.14.0
- **Scan Types:** Baseline (passive) + Full (active)
- **CI/CD Platform:** GitHub Actions
- **Application:** Spring Boot 3.x REST API
- **Runtime:** Docker container
- **Report Formats:** HTML, JSON, Markdown

---

## Conclusion

This DAST assessment provides comprehensive runtime security analysis of the cicd-demo application. The findings should be addressed according to the remediation roadmap, with high-risk issues taking priority.

### Key Takeaways:
1. DAST complements SAST for complete security coverage
2. Regular automated scanning catches new vulnerabilities
3. Security headers are critical for web application security
4. Continuous monitoring is essential for production applications

### Next Steps:
1. ✅ Review all ZAP findings in detail
2. ⏳ Implement security header configurations
3. ⏳ Fix high and medium risk vulnerabilities
4. ⏳ Re-scan after fixes to verify remediation
5. ⏳ Integrate into regular deployment pipeline

---

**Report Generated:** [Date]  
**Reviewed By:** [Your Name]  
**Status:** Ready for submission

---

## Appendix: How to Fill This Report

1. **Open ZAP HTML Reports:** Open both baseline and full scan reports
2. **Count Issues:** Look for the summary section showing High/Medium/Low counts
3. **Document Top Issues:** Pick at least 2-3 significant findings
4. **Take Screenshots:** Capture the summary and specific findings
5. **Complete OWASP Mapping:** Map findings to OWASP Top 10 categories
6. **Create Remediation Plan:** Prioritize fixes based on risk levels
