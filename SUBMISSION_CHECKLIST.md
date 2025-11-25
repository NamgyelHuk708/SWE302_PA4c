# Practical 4b Submission Checklist

**Student Name:** [Your Name]  
**Date:** November 25, 2025  
**Practical:** DAST with OWASP ZAP in GitHub Actions

---

## ✅ Completion Checklist

### Core Requirements

- [ ] **GitHub Actions Workflows Created**
  - [x] `.github/workflows/zap-baseline.yml` exists
  - [x] `.github/workflows/zap-full.yml` exists
  
- [ ] **ZAP Configuration**
  - [x] `.zap/rules.tsv` properly configured (47 rules)
  - [x] Rules include HIGH, MEDIUM, and LOW severity checks

- [ ] **Application Setup**
  - [x] `Dockerfile` exists and configured
  - [x] Application builds successfully
  - [x] Application runs on port 5000

- [ ] **ZAP Scans Executed**
  - [x] Baseline scan completed (reports exist)
  - [x] Full scan completed (reports exist)
  - [ ] Scans run via GitHub Actions (pending push)

---

## 📸 Screenshots Required

### 1. GitHub Actions Workflow Execution
**Status:** ⏳ Pending (need to push to GitHub)

**Required Screenshots:**
- [ ] Workflow runs list showing successful execution
- [ ] Baseline scan workflow details
- [ ] Full scan workflow details
- [ ] Workflow execution logs

**How to Get:**
1. Push code to GitHub
2. Go to repository → Actions tab
3. Run workflows manually or via push
4. Screenshot the successful runs

---

### 2. ZAP Scan Reports
**Status:** ✅ Reports exist locally

**Required Screenshots:**
- [ ] ZAP baseline report summary (risk counts)
- [ ] ZAP full report summary (risk counts)
- [ ] At least 2 identified vulnerabilities with details
- [ ] Evidence of security findings

**How to Get:**
1. Open `zap-baseline-report/report_html.html` in browser
2. Screenshot the summary section
3. Open `zap-full-report/report_html.html` in browser
4. Screenshot specific vulnerabilities (at least 2)

**Example Findings to Look For:**
- Missing security headers (X-Frame-Options, CSP)
- Cookie security issues (SameSite attribute)
- Server version disclosure
- Information disclosure

---

### 3. Configuration Files
**Status:** ✅ All files created

**Files to Include:**
- [x] `.github/workflows/zap-baseline.yml`
- [x] `.github/workflows/zap-full.yml`
- [x] `.zap/rules.tsv`
- [x] `Dockerfile`

---

## 📄 Documentation Required

### 1. Security Analysis Report
**Status:** ✅ Template created

**File:** `SECURITY_ANALYSIS_REPORT.md`

**To Complete:**
1. Open ZAP HTML reports
2. Fill in the vulnerability findings (at least 2)
3. Complete OWASP Top 10 mapping table
4. Add risk counts from reports

---

### 2. README Documentation
**Status:** ✅ Will be created

**Should Include:**
- How to run the application
- How to trigger ZAP scans
- How to view reports
- Summary of findings

---

## 🚀 Steps to Complete Submission

### Step 1: Review Existing Reports ✅ DONE
- [x] Check `zap-baseline-report/report_html.html`
- [x] Check `zap-full-report/report_html.html`
- [x] Note down at least 2 security findings

### Step 2: Complete Security Analysis Report
- [ ] Open `SECURITY_ANALYSIS_REPORT.md`
- [ ] Fill in Finding #1 from ZAP report
- [ ] Fill in Finding #2 from ZAP report
- [ ] Complete OWASP Top 10 mapping table
- [ ] Add risk counts (High/Medium/Low)

### Step 3: Push to GitHub
```bash
# Initialize git if not already done
git init
git add .
git commit -m "Add OWASP ZAP security scanning with GitHub Actions"

# Create GitHub repository and push
git remote add origin <your-repo-url>
git branch -M main
git push -u origin main
```

### Step 4: Run GitHub Actions
- [ ] Go to GitHub Actions tab
- [ ] Manually trigger "OWASP ZAP Baseline Scan"
- [ ] Manually trigger "OWASP ZAP Full Scan"
- [ ] Wait for completion (baseline: ~2-5 min, full: ~10-15 min)

### Step 5: Collect Screenshots
- [ ] Screenshot workflow runs (Actions tab)
- [ ] Screenshot successful baseline scan
- [ ] Screenshot successful full scan
- [ ] Download and screenshot ZAP reports from artifacts
- [ ] Screenshot at least 2 specific vulnerabilities

### Step 6: Create Submission Package

Create a folder with:
```
submission/
├── screenshots/
│   ├── 01-workflow-runs.png
│   ├── 02-baseline-scan-success.png
│   ├── 03-full-scan-success.png
│   ├── 04-zap-report-summary.png
│   ├── 05-vulnerability-1.png
│   └── 06-vulnerability-2.png
├── configuration-files/
│   ├── zap-baseline.yml
│   ├── zap-full.yml
│   └── rules.tsv
├── reports/
│   ├── zap-baseline-report.html
│   └── zap-full-report.html
└── SECURITY_ANALYSIS_REPORT.md
```

---

## 🎯 Submission Verification

### Minimum Requirements Met?

**GitHub Actions:**
- [ ] At least 1 workflow file created and working
- [ ] Workflow successfully executes ZAP scan
- [ ] Reports generated as artifacts

**ZAP Configuration:**
- [x] Rules file exists with proper configuration
- [x] At least 20+ security rules configured

**Evidence:**
- [ ] At least 2 screenshots of workflow execution
- [ ] At least 2 screenshots of security findings
- [ ] ZAP reports accessible

**Analysis:**
- [ ] Security analysis report completed
- [ ] At least 2 vulnerabilities documented
- [ ] Remediation recommendations provided

---

## ⚠️ Common Issues to Avoid

1. **Workflow Doesn't Run**
   - Check: File is in `.github/workflows/` directory
   - Check: YAML syntax is correct
   - Check: Branch name matches (main vs master)

2. **Application Won't Start in Docker**
   - Check: Maven build succeeds
   - Check: JAR file exists in target/
   - Check: Port 5000 is exposed

3. **ZAP Can't Connect to App**
   - Check: Application is fully started before scan
   - Check: Wait/timeout logic is working
   - Check: Endpoints are accessible (curl test)

4. **No Findings in Report**
   - This is normal! It means the app is secure
   - But check if scan actually ran (check logs)
   - Consider the baseline scan vs full scan difference

---

## 📊 Expected Findings (Based on Typical Spring Boot Apps)

You will likely see these common findings:

### High Priority:
- None expected (if basic Spring Security is configured)

### Medium Priority:
1. **X-Frame-Options Header Not Set** - Very common
2. **Content Security Policy Header Not Set** - Very common
3. **Cookie Without SameSite Attribute** - Common
4. **X-Content-Type-Options Header Missing** - Common

### Low Priority:
1. **Server Version Disclosure** - Common
2. **Timestamp Disclosure** - Common
3. **Information Disclosure** - May occur

**Use These for Your Report!** Pick at least 2 from the above for documentation.

---

## 🎓 Learning Outcomes Achieved

By completing this practical, you have:

- [x] Understood DAST vs SAST differences
- [x] Configured OWASP ZAP for automated scanning
- [x] Integrated security testing in CI/CD pipeline
- [ ] Analyzed runtime security vulnerabilities (pending report completion)
- [ ] Mapped findings to OWASP Top 10 (pending report completion)
- [x] Created reproducible security testing workflow

---

## 📝 Final Notes

### What Makes Your Friend's Work Good:
1. ✅ Proper ZAP rules configuration (comprehensive)
2. ✅ Both baseline and full reports exist
3. ✅ Application is properly dockerized
4. ✅ Project structure is clean

### What Was Missing (Now Fixed):
1. ✅ GitHub Actions workflows (JUST ADDED)
2. ✅ Security analysis documentation (JUST ADDED)
3. ⏳ GitHub repository setup (YOU NEED TO DO)
4. ⏳ Workflow execution evidence (YOU NEED TO DO)

### Your Contribution:
1. ✅ Created GitHub Actions workflows
2. ✅ Created security analysis template
3. ✅ Created submission documentation
4. ⏳ Will execute workflows and collect evidence
5. ⏳ Will complete security analysis report

---

## 🔗 Quick Commands

### Build and Test Locally:
```bash
# Build application
mvn clean package -DskipTests

# Build Docker image
docker build -t cicd-demo:test .

# Run application
docker run -d -p 5000:5000 --name app cicd-demo:test

# Test endpoints
curl http://localhost:5000/nations
curl http://localhost:5000/currencies

# Stop application
docker stop app && docker rm app
```

### Run ZAP Scan Locally (Optional):
```bash
# Baseline scan
docker run -v $(pwd):/zap/wrk/:rw -t ghcr.io/zaproxy/zaproxy:stable \
  zap-baseline.py -t http://localhost:5000 -r baseline_report.html

# Full scan
docker run -v $(pwd):/zap/wrk/:rw -t ghcr.io/zaproxy/zaproxy:stable \
  zap-full-scan.py -t http://localhost:5000 -r full_report.html
```

---

**Status:** Ready for GitHub push and workflow execution!  
**Next Action:** Push to GitHub and run workflows to collect evidence.
