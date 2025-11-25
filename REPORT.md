# OWASP ZAP Security Scanning Report

**Project:** SWE302_PA4c - CI/CD Security Testing  
**Repository:** [https://github.com/NamgyelHuk708/SWE302_PA4c](https://github.com/NamgyelHuk708/SWE302_PA4c)  
**Date:** November 25, 2025  
**Author:** Namgyel Huk

---

## 1. Overview

This report documents the implementation of automated security testing using OWASP ZAP (Zed Attack Proxy) integrated with GitHub Actions for continuous security scanning.

---

## 2. Implementation Summary

### 2.1 Technologies Used
- **Security Tool:** OWASP ZAP
- **CI/CD Platform:** GitHub Actions
- **Application:** Spring Boot (Java 17)
- **Containerization:** Docker
- **Build Tool:** Maven

### 2.2 Scan Types Implemented
1. **Baseline Scan** - Quick security assessment on every push/PR
2. **Full Scan** - Comprehensive security analysis (scheduled weekly)

---

## 3. GitHub Actions Workflows

### 3.1 ZAP Baseline Scan Workflow
- **Trigger:** On push/pull request to main branch
- **Purpose:** Quick security check for common vulnerabilities
- **Reports:** HTML format uploaded as artifact

![Baseline Workflow Screenshot](screenshots/baseline-workflow.png)
*Screenshot: ZAP Baseline Scan workflow execution*

### 3.2 ZAP Full Scan Workflow
- **Trigger:** Weekly (Sundays at 2 AM) + Manual
- **Purpose:** Comprehensive security scanning
- **Reports:** HTML, JSON, and Markdown formats

![Full Scan Workflow Screenshot](screenshots/full-scan-workflow.png)
*Screenshot: ZAP Full Scan workflow execution*

---

## 4. Configuration Details

### 4.1 Workflow Permissions
```yaml
permissions:
  contents: read
  issues: write
```

### 4.2 Key Features
- ✅ Automated issue creation for vulnerabilities
- ✅ Artifact uploads for detailed reports
- ✅ Integration with GitHub security features
- ✅ Customizable scanning rules

![GitHub Settings Screenshot](screenshots/github-settings.png)
*Screenshot: GitHub Actions workflow permissions configuration*

---

## 5. Scan Results

### 5.1 Latest Baseline Scan Results
- **Status:** ✅ Completed Successfully
- **Warnings Found:** 4
- **Tests Passed:** 66
- **Issues Created:** #5, #6

![Scan Results Screenshot](screenshots/scan-results.png)
*Screenshot: ZAP scan summary results*

### 5.2 Security Issues Identified

| Alert | Risk Level | Status |
|-------|-----------|--------|
| Missing Security Headers | Warning | Identified |
| Content Security Policy | Warning | Identified |
| X-Frame-Options | Warning | Identified |
| Permissions Policy | Warning | Identified |

![Security Issues Screenshot](screenshots/security-issues.png)
*Screenshot: GitHub issues created by ZAP scan*

---

## 6. Artifacts Generated

### 6.1 Available Reports
- **HTML Report** - Visual security assessment
- **JSON Report** - Machine-readable format
- **Markdown Report** - Documentation format

![Artifacts Screenshot](screenshots/artifacts.png)
*Screenshot: Generated artifacts in GitHub Actions*

---

## 7. Issues Encountered & Resolutions

### 7.1 Permission Error
**Problem:** "Resource not accessible by integration"

**Solution:**
- Added `permissions` block to workflows
- Configured `issues: write` permission
- Added `token: ${{ secrets.GITHUB_TOKEN }}`

### 7.2 Artifact Naming Error
**Problem:** "Artifact name zap_scan is not valid"

**Solution:**
- Removed conflicting `artifact_name` parameter
- Let ZAP action use default artifact handling

### 7.3 SonarCloud Configuration
**Problem:** Using friend's organization settings

**Solution:**
- Updated `sonar.organization` to `namgyelhuk708`
- Modified both `pom.xml` and `sonar-project.properties`

---

## 8. Repository Settings

### 8.1 Required GitHub Settings
**Path:** Settings → Actions → General → Workflow permissions

- ✅ Read and write permissions
- ✅ Allow GitHub Actions to create and approve pull requests

![Workflow Permissions Screenshot](screenshots/workflow-permissions.png)
*Screenshot: GitHub Actions workflow permissions settings*

---

## 9. Workflow Execution

### 9.1 Successful Build Steps
1. Checkout code
2. Set up JDK 17
3. Build with Maven
4. Build Docker image
5. Run application container
6. Execute ZAP scan
7. Upload reports
8. Create GitHub issues

![Workflow Steps Screenshot](screenshots/workflow-steps.png)
*Screenshot: Complete workflow execution steps*

---

## 10. Sample Report Output

### 10.1 ZAP Baseline Report
```
Target: http://localhost:5000
Scan Duration: 3m 8s
Endpoints Scanned:
  - / (200 OK)
  - /nations (200 OK)
  - /currencies (200 OK)
  - /robots.txt (404)
  - /sitemap.xml (404)

Results:
  FAIL-NEW: 0
  WARN-NEW: 4
  INFO: 0
  PASS: 66
```

![Report Sample Screenshot](screenshots/report-sample.png)
*Screenshot: Sample ZAP scan report*

---

## 11. Conclusions

### 11.1 Achievements
- ✅ Successfully integrated OWASP ZAP with GitHub Actions
- ✅ Automated security scanning on every push
- ✅ Automatic issue creation for vulnerabilities
- ✅ Comprehensive reporting in multiple formats
- ✅ Configured proper permissions and security settings

### 11.2 Security Posture
The application has been scanned and shows **4 warnings** related to HTTP security headers. No critical vulnerabilities were found. The warnings are related to:
- Missing Content Security Policy headers
- Missing X-Frame-Options headers
- Missing Permissions Policy headers
- Cross-Origin headers configuration

### 11.3 Recommendations
1. Implement missing security headers in Spring Boot configuration
2. Review and address all identified warnings
3. Schedule regular full scans for comprehensive assessment
4. Monitor GitHub issues created by ZAP scans
5. Integrate fixes and re-scan to verify improvements

---

## 12. Repository Links

- **GitHub Repository:** [https://github.com/NamgyelHuk708/SWE302_PA4c](https://github.com/NamgyelHuk708/SWE302_PA4c)
- **GitHub Actions:** [https://github.com/NamgyelHuk708/SWE302_PA4c/actions](https://github.com/NamgyelHuk708/SWE302_PA4c/actions)
- **Issues:** [https://github.com/NamgyelHuk708/SWE302_PA4c/issues](https://github.com/NamgyelHuk708/SWE302_PA4c/issues)

---

## 13. Screenshots Directory Structure

```
screenshots/
├── baseline-workflow.png
├── full-scan-workflow.png
├── github-settings.png
├── scan-results.png
├── security-issues.png
├── artifacts.png
├── workflow-permissions.png
├── workflow-steps.png
└── report-sample.png
```

**Note:** Add screenshots to the `screenshots/` directory in the repository root.

---

## Appendix

### Workflow Files
- `.github/workflows/zap-baseline.yml`
- `.github/workflows/zap-full.yml`

### Configuration Files
- `pom.xml` - Maven build configuration
- `sonar-project.properties` - SonarCloud settings
- `.zap/rules.tsv` - ZAP scanning rules
- `Dockerfile` - Container configuration

---

**End of Report**
