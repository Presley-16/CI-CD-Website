# Troubleshooting Guide - CI/CD Pipeline

## 🔍 Diagnostic Workflow

```
Problem Detected
    ↓
Check Actions Tab → View Logs → Identify Error
    ↓
Find Solution Below → Apply Fix → Push Changes → Verify
```

---

## 🚨 Common Errors and Solutions

### 1. WORKFLOW ERRORS

#### Error: "Workflow file not found"
**Symptoms:**
- Push doesn't trigger workflow
- No runs in Actions tab

**Diagnosis:**
```bash
# Check file location
ls -la .github/workflows/ci.yml
```

**Solutions:**
1. Ensure file path is exactly: `.github/workflows/ci.yml`
2. Note the dot prefix on `.github`
3. Check file is committed:
   ```bash
   git status
   git add .github/workflows/ci.yml
   git commit -m "Add workflow file"
   git push
   ```

#### Error: "Invalid workflow file"
**Symptoms:**
- Workflow appears but shows error icon
- Message: "Invalid workflow file"

**Diagnosis:**
- YAML syntax error
- Incorrect indentation

**Solutions:**
1. Validate YAML syntax at https://www.yamllint.com/
2. Check indentation (use spaces, not tabs)
3. Ensure colons have space after them: `name: value`
4. Common mistakes:
   ```yaml
   # ❌ WRONG
   name:CI Pipeline
   
   # ✅ CORRECT
   name: CI Pipeline
   ```

---

### 2. HTML VALIDATION ERRORS

#### Error: "HTML validation failed"
**Symptoms:**
- validate-html job fails with red X
- Error messages about HTML issues

**Common Issues:**

**Unclosed Tags:**
```html
<!-- ❌ WRONG -->
<div>
  <p>Content
</div>

<!-- ✅ CORRECT -->
<div>
  <p>Content</p>
</div>
```

**Missing DOCTYPE:**
```html
<!-- ❌ WRONG -->
<html>

<!-- ✅ CORRECT -->
<!DOCTYPE html>
<html lang="en">
```

**Duplicate IDs:**
```html
<!-- ❌ WRONG -->
<div id="main"></div>
<div id="main"></div>

<!-- ✅ CORRECT -->
<div id="main"></div>
<div id="content"></div>
```

**Invalid Attributes:**
```html
<!-- ❌ WRONG -->
<img src="image.jpg">

<!-- ✅ CORRECT -->
<img src="image.jpg" alt="Description">
```

**How to Fix:**
1. Read error message in workflow logs
2. Find line number mentioned
3. Fix the specific issue
4. Test locally: `html-validate index.html`
5. Commit and push

---

### 3. CSS VALIDATION ERRORS

#### Error: "Stylelint errors found"
**Symptoms:**
- validate-css job fails
- CSS formatting issues

**Common Issues:**

**Missing Semicolons:**
```css
/* ❌ WRONG */
.class {
  color: red
  margin: 10px
}

/* ✅ CORRECT */
.class {
  color: red;
  margin: 10px;
}
```

**Invalid Color Values:**
```css
/* ❌ WRONG */
.class {
  color: #f;
}

/* ✅ CORRECT */
.class {
  color: #fff;
}
```

**Unknown Properties:**
```css
/* ❌ WRONG */
.class {
  colr: red;  /* typo */
}

/* ✅ CORRECT */
.class {
  color: red;
}
```

**How to Fix:**
1. Check workflow logs for specific errors
2. Test locally: `stylelint styles.css`
3. Fix reported issues
4. Commit and push

---

### 4. JAVASCRIPT LINTING ERRORS

#### Error: "ESLint found problems"
**Symptoms:**
- lint-javascript job fails or warns
- JavaScript code quality issues

**Common Issues:**

**Undefined Variables:**
```javascript
// ❌ WRONG
console.log(undefinedVariable);

// ✅ CORRECT
const definedVariable = 'value';
console.log(definedVariable);
```

**Missing Semicolons:**
```javascript
// ❌ WRONG
const x = 5
const y = 10

// ✅ CORRECT
const x = 5;
const y = 10;
```

**Unused Variables:**
```javascript
// ❌ WRONG
const unused = 'never used';

// ✅ CORRECT - either use it or remove it
const used = 'used value';
console.log(used);
```

**How to Fix:**
1. Review ESLint errors in logs
2. Test locally: `eslint script.js`
3. Fix issues or add `// eslint-disable-next-line` if intentional
4. Commit and push

---

### 5. DEPLOYMENT ERRORS

#### Error: "Deploy to GitHub Pages failed"
**Symptoms:**
- All validation passes
- Deploy job fails
- Website not accessible

**Solution 1: Enable Pages**
1. Go to Settings → Pages
2. Under "Source", select "GitHub Actions"
3. Save and wait 2-3 minutes
4. Re-run workflow

**Solution 2: Check Permissions**
1. Settings → Actions → General
2. Scroll to "Workflow permissions"
3. Select "Read and write permissions"
4. Check "Allow GitHub Actions to create and approve pull requests"
5. Save
6. Re-run failed workflow

**Solution 3: Repository Visibility**
1. Check repository is Public
2. Or ensure GitHub Pro/Teams for private repo Pages
3. Settings → General → Visibility

**Solution 4: Branch Protection**
1. Settings → Branches
2. Check no rules blocking deployments
3. Temporarily disable if needed

---

### 6. PAGE ACCESS ERRORS

#### Error: "404 - Site not found"
**Symptoms:**
- Deploy succeeds
- URL shows 404 error
- Site was previously working

**Solutions:**

**Wrong URL:**
```
❌ https://github.com/username/repo
✅ https://username.github.io/repo
```

**Cache Issue:**
1. Hard refresh: `Ctrl + Shift + R` (Windows/Linux) or `Cmd + Shift + R` (Mac)
2. Clear browser cache
3. Try incognito/private mode
4. Try different browser

**Wait Time:**
- First deployment: Wait 3-5 minutes
- Subsequent deploys: Wait 1-2 minutes
- Check deployment status in Actions

**Deployment URL:**
1. Go to Actions → Latest workflow run
2. Click "deploy" job
3. Find "Deploy to GitHub Pages" step
4. Copy URL from logs

---

### 7. BADGE ERRORS

#### Error: "Badge shows 'unknown' or not found"
**Symptoms:**
- Badge doesn't display
- Shows "unknown" status
- Broken image icon

**Solutions:**

**Check Badge URL:**
```markdown
<!-- Template -->
[![CI/CD Pipeline](https://github.com/USERNAME/REPO/actions/workflows/ci.yml/badge.svg)](https://github.com/USERNAME/REPO/actions/workflows/ci.yml)

<!-- Example -->
[![CI/CD Pipeline](https://github.com/johndoe/ci-cd-demo/actions/workflows/ci.yml/badge.svg)](https://github.com/johndoe/ci-cd-demo/actions/workflows/ci.yml)
```

**Common Mistakes:**
1. Forgot to replace USERNAME
2. Forgot to replace REPO
3. Wrong workflow filename (should be `ci.yml`)
4. Wrong file extension in URL

**Fix Steps:**
1. Update README.md with correct values
2. Commit and push
3. Wait for workflow to complete
4. Refresh repository page
5. Badge should appear within 1 minute

---

### 8. LINK CHECKER ERRORS

#### Error: "Broken links found"
**Symptoms:**
- test-links job fails
- External links not accessible

**Solutions:**

**External Links Down:**
- May be temporary
- Check if site is actually down
- Mark as expected failure in workflow:
  ```yaml
  continue-on-error: true
  ```

**Internal Links Broken:**
```html
<!-- ❌ WRONG -->
<a href="#doesnotexist">Link</a>

<!-- ✅ CORRECT -->
<a href="#features">Link</a>
<!-- Ensure id="features" exists somewhere -->
```

**File Not Found:**
```html
<!-- ❌ WRONG -->
<link rel="stylesheet" href="style.css">

<!-- ✅ CORRECT -->
<link rel="stylesheet" href="styles.css">
```

---

### 9. BUILD ERRORS

#### Error: "Build artifacts not created"
**Symptoms:**
- Build job fails
- No artifacts uploaded

**Solutions:**

**Missing Files:**
```bash
# Check files exist
ls -la *.html *.css *.js
```

**Copy Command Issues:**
```yaml
# Make copy commands non-failing
cp *.html build/ || true
cp *.css build/ || true
cp *.js build/ || true
```

**Directory Not Created:**
```bash
# Ensure build directory exists
mkdir -p build
```

---

### 10. PERFORMANCE TEST ERRORS

#### Error: "Lighthouse failed"
**Symptoms:**
- performance-test job fails
- Lighthouse can't access site

**Solutions:**

**Server Not Started:**
```yaml
# Add sleep to ensure server is ready
- run: |
    npx http-server . -p 8080 &
    sleep 5  # Increase wait time
```

**Port Conflict:**
```yaml
# Use different port
npx http-server . -p 8081
# Update Lighthouse URL accordingly
```

**Mark as Non-Critical:**
```yaml
- name: Run Lighthouse
  continue-on-error: true  # Don't fail build
```

---

## 🛠️ General Debugging Steps

### 1. Read the Logs
```
Actions Tab → Click Workflow Run → Click Failed Job → Read Error Messages
```

### 2. Test Locally
```bash
# Install dependencies
npm install -g html-validate stylelint eslint

# Test each component
html-validate "*.html"
stylelint "*.css"
eslint "*.js"
```

### 3. Isolate the Problem
```bash
# Comment out jobs to find which fails
# In ci.yml, add 'if: false' to skip jobs:

validate-html:
  if: false  # Temporarily skip this job
  runs-on: ubuntu-latest
  # ... rest of job
```

### 4. Check Dependencies
```bash
# Verify Node.js version
node --version  # Should be 18+

# Clear npm cache if needed
npm cache clean --force
```

### 5. Re-run Workflow
```
Actions → Failed Workflow → Re-run all jobs
```

---

## 📞 Getting Help

### Before Asking for Help

1. ✅ Read the error message completely
2. ✅ Check this troubleshooting guide
3. ✅ Review workflow logs
4. ✅ Test locally if possible
5. ✅ Google the specific error message

### When Asking for Help

Provide:
- Repository URL
- Specific error message
- Workflow run link
- What you've already tried
- Relevant code snippets

### Where to Get Help

1. **GitHub Issues** - Repository issues
2. **GitHub Discussions** - Community forum
3. **Stack Overflow** - Tag with `github-actions`
4. **GitHub Docs** - https://docs.github.com
5. **Instructor/TA** - For assignment help

---

## ✅ Success Checklist

All these should be ✅ for successful deployment:

- [ ] Repository exists on GitHub
- [ ] All files committed and pushed
- [ ] Workflow file in correct location
- [ ] YAML syntax valid
- [ ] HTML validation passing
- [ ] CSS validation passing
- [ ] JavaScript linting passing
- [ ] Build job successful
- [ ] Deploy job successful
- [ ] GitHub Pages enabled
- [ ] Site accessible at Pages URL
- [ ] Badge showing "passing"
- [ ] README updated with correct info

---

## 🎯 Quick Fixes Reference

| Error | Quick Fix |
|-------|-----------|
| Workflow not found | Check `.github/workflows/ci.yml` path |
| YAML syntax error | Validate at yamllint.com |
| HTML validation fails | Close all tags, add alt attributes |
| CSS validation fails | Add missing semicolons |
| Deploy permission error | Enable Read/Write in Settings |
| 404 on Pages | Wait 3 mins, check URL format |
| Badge not showing | Update USERNAME/REPO in badge URL |
| Links broken | Check file names match exactly |

---

**Remember:** Most issues are simple fixes. Read error messages carefully!

**Last Updated:** February 11, 2026
