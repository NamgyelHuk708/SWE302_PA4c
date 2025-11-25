# Setup Your Own Repository

## Current Situation
You're working with a friend's repository: `NamgyelHuk708/SWE302_PA4c`

## Errors You Encountered
1. **"Resource not accessible by integration"** - No permission to create GitHub issues
2. **"Artifact name zap_scan is not valid"** - Invalid artifact naming

## ✅ Solutions Applied
- Added `permissions:` block for issues
- Added `artifact_name` with hyphens instead of underscores
- Added `token`, `issue_title`, and `fail_action` parameters

---

## 🚀 Make This Repository YOURS

### Option 1: Fork the Repository (Easiest)

1. **Fork on GitHub:**
   - Go to: https://github.com/NamgyelHuk708/SWE302_PA4c
   - Click the "Fork" button (top-right)
   - Select your GitHub account

2. **Update Local Repository:**
   ```bash
   cd /home/namgyel/Desktop/SEM5/SWE302/practical_4c/SWE302_PA4c
   
   # Replace YOUR_USERNAME with your GitHub username
   git remote set-url origin https://github.com/YOUR_USERNAME/SWE302_PA4c.git
   
   # Verify
   git remote -v
   
   # Push to your fork
   git push -u origin main
   ```

3. **Enable GitHub Actions:**
   - Go to your forked repo on GitHub
   - Click "Actions" tab
   - Click "I understand my workflows, go ahead and enable them"

4. **Configure Repository Settings:**
   - Go to Settings → Actions → General
   - Under "Workflow permissions":
     - Select "Read and write permissions"
     - Check "Allow GitHub Actions to create and approve pull requests"
   - Click "Save"

---

### Option 2: Create New Repository

1. **Create New Repo on GitHub:**
   - Go to: https://github.com/new
   - Name: `SWE302_PA4c` (or any name you want)
   - Make it Public or Private
   - DON'T initialize with README
   - Click "Create repository"

2. **Update Local Repository:**
   ```bash
   cd /home/namgyel/Desktop/SEM5/SWE302/practical_4c/SWE302_PA4c
   
   # Remove old remote
   git remote remove origin
   
   # Add your new remote (replace YOUR_USERNAME)
   git remote add origin https://github.com/YOUR_USERNAME/SWE302_PA4c.git
   
   # Push everything
   git push -u origin main
   ```

3. **Configure Repository Settings** (same as Option 1, step 4)

---

## 📋 Required Repository Settings

After creating/forking, you MUST configure these settings:

### 1. Workflow Permissions
**Path:** Settings → Actions → General → Workflow permissions

✅ **Select:** "Read and write permissions"
✅ **Check:** "Allow GitHub Actions to create and approve pull requests"

### 2. Enable Actions (for forks)
**Path:** Actions tab

✅ Click "I understand my workflows, go ahead and enable them"

---

## 🔧 Files Already Fixed

The following files have been updated with the correct configuration:

### `.github/workflows/zap-baseline.yml`
- ✅ Added `permissions` block
- ✅ Added `token: ${{ secrets.GITHUB_TOKEN }}`
- ✅ Added `artifact_name: 'zap-baseline-scan'`
- ✅ Added `issue_title` and `fail_action`

### `.github/workflows/zap-full.yml`
- ✅ Added `permissions` block
- ✅ Added `token: ${{ secrets.GITHUB_TOKEN }}`
- ✅ Added `artifact_name: 'zap-full-scan'`
- ✅ Added `issue_title` and `fail_action`

---

## ✨ What Happens After Setup

Once you've created your own repository and configured the settings:

1. **Automatic Scanning:**
   - ZAP Baseline Scan runs on every push/PR to main
   - ZAP Full Scan runs weekly on Sundays at 2 AM

2. **GitHub Issues Created:**
   - Security issues found by ZAP will create GitHub issues automatically
   - Issues will have detailed information about vulnerabilities

3. **Artifacts Available:**
   - HTML, JSON, and Markdown reports uploaded as artifacts
   - Download from the Actions tab → Select workflow run → Artifacts section

4. **Manual Triggers:**
   - Both workflows can be manually triggered
   - Go to Actions tab → Select workflow → "Run workflow"

---

## 🧪 Test Your Setup

After completing the setup:

```bash
# Make a small change to trigger workflow
echo "# Test" >> README.md
git add README.md
git commit -m "Test workflow trigger"
git push

# Then check:
# 1. Go to GitHub Actions tab
# 2. Watch the workflow run
# 3. Check if issues are created (if vulnerabilities found)
# 4. Download artifacts from the workflow run
```

---

## 📞 Troubleshooting

### Workflow Fails with Permission Error
**Solution:** Check Settings → Actions → General → Workflow permissions
- Must be "Read and write permissions"

### No Issues Created Despite Warnings
**Solution:** 
- Check that `token: ${{ secrets.GITHUB_TOKEN }}` is present
- Verify workflow permissions include `issues: write`

### Artifact Upload Fails
**Solution:**
- Ensure artifact names use hyphens, not underscores
- Check that `artifact_name` parameter is set

---

## 🎯 Quick Commands Reference

```bash
# Check current remote
git remote -v

# Change to your fork/repo
git remote set-url origin https://github.com/YOUR_USERNAME/SWE302_PA4c.git

# Push changes
git push -u origin main

# View GitHub Actions logs
# (Must be done in GitHub web interface)
# Go to: https://github.com/YOUR_USERNAME/SWE302_PA4c/actions
```

---

## ✅ Checklist

- [ ] Fork repository OR create new repository on GitHub
- [ ] Update local git remote to your repository
- [ ] Push code to your repository
- [ ] Enable GitHub Actions (if forked)
- [ ] Set "Read and write permissions" in workflow settings
- [ ] Test by pushing a commit
- [ ] Verify workflow runs successfully
- [ ] Check that artifacts are uploaded
- [ ] Verify issues are created (if warnings/alerts exist)

**Good luck! 🚀**
