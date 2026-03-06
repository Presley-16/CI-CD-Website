# UNIT 3 ASSIGNMENT: CI/CD Implementation Guide
## Complete Step-by-Step Instructions

---

## TABLE OF CONTENTS

1. Introduction
2. Prerequisites and Setup
3. Step-by-Step Implementation
4. Dependency Installation Guide
5. Testing and Verification
6. Troubleshooting
7. Conclusion

---

## 1. INTRODUCTION

### Objective
This guide provides complete instructions for implementing a Continuous Integration (CI) pipeline for a static website using GitHub Actions. You will automate build validation, testing, and deployment processes.

### What You'll Build
- A responsive static website (HTML, CSS, JavaScript)
- Automated HTML/CSS validation
- JavaScript linting
- Broken link testing
- Security scanning
- Automated deployment to GitHub Pages
- Build status monitoring

### Time Required
- Approximately 2-3 hours for complete setup

---

## 2. PREREQUISITES AND SETUP

### Required Accounts
1. **GitHub Account**
   - Create free account at https://github.com
   - Verify your email address

### Required Software
1. **Git** (Version Control)
   - Windows: Download from https://git-scm.com/download/win
   - Mac: Run `brew install git` or download from git-scm.com
   - Linux: Run `sudo apt-get install git`
   - Verify: `git --version`

2. **Text Editor** (Choose one)
   - Visual Studio Code (Recommended): https://code.visualstudio.com/
   - Sublime Text: https://www.sublimetext.com/
   - Atom: https://atom.io/

3. **Node.js** (For local testing - Optional)
   - Download from https://nodejs.org/ (LTS version)
   - Verify: `node --version` and `npm --version`

---

## 3. STEP-BY-STEP IMPLEMENTATION

### STEP 1: CREATE GITHUB REPOSITORY

**Duration: 5 minutes**

1. **Log in to GitHub**
   - Navigate to https://github.com
   - Sign in with your credentials

2. **Create New Repository**
   - Click the "+" icon in top-right corner
   - Select "New repository"

3. **Configure Repository**
   - Repository name: `ci-cd-demo-website` (or your choice)
   - Description: "CI/CD demonstration using GitHub Actions"
   - Visibility: Select "Public"
   - ✅ Check "Add a README file"
   - Click "Create repository"

4. **Copy Repository URL**
   - Click the green "Code" button
   - Copy the HTTPS URL (e.g., https://github.com/username/ci-cd-demo-website.git)

---

### STEP 2: CLONE REPOSITORY LOCALLY

**Duration: 5 minutes**

1. **Open Terminal/Command Prompt**
   - Windows: Press Win+R, type `cmd`, press Enter
   - Mac: Press Cmd+Space, type "Terminal", press Enter
   - Linux: Press Ctrl+Alt+T

2. **Navigate to Desired Directory**
   ```bash
   cd Desktop
   # Or any directory where you want to store the project
   ```

3. **Clone Repository**
   ```bash
   git clone https://github.com/YOUR-USERNAME/ci-cd-demo-website.git
   cd ci-cd-demo-website
   ```
   Replace YOUR-USERNAME with your GitHub username

4. **Verify Clone Success**
   ```bash
   ls -la
   # You should see .git folder and README.md
   ```

---

### STEP 3: CREATE WEBSITE FILES

**Duration: 15 minutes**

#### 3A. Create index.html

1. **Create File**
   - Open your text editor
   - Create new file named `index.html`
   - Copy the HTML content from the provided index.html file
   - Save in your repository folder

2. **Key HTML Components**
   - DOCTYPE declaration
   - Proper meta tags for viewport and charset
   - Semantic HTML5 elements (header, nav, main, section, footer)
   - Links to CSS and JavaScript files

#### 3B. Create styles.css

1. **Create File**
   - Create new file named `styles.css`
   - Copy the CSS content from the provided styles.css file
   - Save in your repository folder

2. **Key CSS Features**
   - CSS Variables for theming
   - Responsive grid layouts
   - Flexbox for navigation
   - Media queries for mobile
   - Smooth transitions

#### 3C. Create script.js

1. **Create File**
   - Create new file named `script.js`
   - Copy the JavaScript content from the provided script.js file
   - Save in your repository folder

2. **Key JavaScript Features**
   - Smooth scrolling navigation
   - Active link highlighting
   - Intersection Observer for animations
   - Console logging for verification

---

### STEP 4: CREATE GITHUB ACTIONS WORKFLOW

**Duration: 10 minutes**

1. **Create Directory Structure**
   ```bash
   mkdir -p .github/workflows
   ```
   Note: The dot prefix (.) makes it a hidden folder

2. **Create Workflow File**
   - Create file: `.github/workflows/ci.yml`
   - Copy the complete YAML content from provided ci.yml file
   - Save the file

3. **Understanding the Workflow Structure**

   **Workflow Triggers:**
   ```yaml
   on:
     push:
       branches: [main]
     pull_request:
       branches: [main]
   ```
   - Runs on every push to main branch
   - Runs on pull requests to main

   **Jobs Explained:**
   
   a. **validate-html**: Validates HTML syntax
      - Uses html-validate npm package
      - Checks for proper structure
      - Uploads results as artifacts

   b. **validate-css**: Lints CSS files
      - Uses Stylelint
      - Checks for CSS standards
      - Configures custom rules

   c. **lint-javascript**: Checks JavaScript
      - Uses ESLint
      - Ensures code quality
      - Reports errors and warnings

   d. **test-links**: Checks for broken links
      - Uses broken-link-checker
      - Starts local server
      - Tests all links on page

   e. **security-scan**: Scans for vulnerabilities
      - Uses Trivy scanner
      - Checks for security issues
      - Reports findings

   f. **build**: Packages website
      - Creates build directory
      - Copies files
      - Generates build info
      - Uploads artifacts

   g. **deploy**: Deploys to GitHub Pages
      - Only runs on main branch
      - Configures Pages
      - Uploads and deploys
      - Provides deployment URL

   h. **performance-test**: Runs Lighthouse
      - Tests performance
      - Checks accessibility
      - Reports metrics

---

### STEP 5: CREATE README.MD

**Duration: 10 minutes**

1. **Edit Existing README**
   - Open the README.md file
   - Replace all content with the provided README content
   - Save the file

2. **Customize README**
   Replace these placeholders:
   - `YOUR-USERNAME` → Your GitHub username
   - `YOUR-REPO-NAME` → Your repository name

3. **Add Status Badge**
   The badge URL format:
   ```
   https://github.com/USERNAME/REPO/actions/workflows/ci.yml/badge.svg
   ```

---

### STEP 6: CREATE ADDITIONAL FILES

**Duration: 5 minutes**

1. **Create .gitignore**
   - Create file named `.gitignore`
   - Copy content from provided .gitignore file
   - Prevents committing unnecessary files

2. **Verify File Structure**
   ```
   ci-cd-demo-website/
   ├── .github/
   │   └── workflows/
   │       └── ci.yml
   ├── .gitignore
   ├── index.html
   ├── styles.css
   ├── script.js
   └── README.md
   ```

---

### STEP 7: COMMIT AND PUSH TO GITHUB

**Duration: 5 minutes**

1. **Stage All Files**
   ```bash
   git add .
   ```

2. **Commit Changes**
   ```bash
   git commit -m "Add CI/CD pipeline and website files"
   ```

3. **Push to GitHub**
   ```bash
   git push origin main
   ```

4. **Verify Push Success**
   - You should see "Writing objects: 100%" message
   - Files should appear in GitHub repository

---

### STEP 8: ENABLE GITHUB PAGES

**Duration: 5 minutes**

1. **Navigate to Repository Settings**
   - Go to your repository on GitHub
   - Click "Settings" tab (near top-right)

2. **Configure Pages**
   - Scroll to "Pages" in left sidebar
   - Under "Source", select "GitHub Actions"
   - Click "Save" (if button appears)

3. **Verify Configuration**
   - You should see: "Your site is ready to be published"
   - Note the URL: `https://USERNAME.github.io/REPO-NAME/`

---

### STEP 9: MONITOR WORKFLOW EXECUTION

**Duration: 10 minutes**

1. **Navigate to Actions Tab**
   - Click "Actions" tab in your repository
   - You should see workflow running

2. **View Workflow Details**
   - Click on the running workflow
   - See all jobs listed
   - Watch real-time progress

3. **Check Job Status**
   - Green checkmark ✓ = Success
   - Red X = Failed
   - Yellow circle = Running

4. **Review Logs**
   - Click individual jobs to see logs
   - Read output for each step
   - Download artifacts if needed

5. **Wait for Deployment**
   - All jobs should complete
   - Deploy job should succeed
   - Note deployment URL in logs

---

### STEP 10: VERIFY DEPLOYMENT

**Duration: 5 minutes**

1. **Access Deployed Website**
   - Open browser
   - Navigate to: `https://USERNAME.github.io/REPO-NAME/`
   - Replace USERNAME and REPO-NAME

2. **Test Website Features**
   - Click navigation links
   - Check smooth scrolling
   - Test on mobile view (resize browser)
   - Verify all sections load

3. **Verify Badge**
   - Go to repository main page
   - Scroll to README
   - Badge should show "passing" status

---

## 4. DEPENDENCY INSTALLATION GUIDE

### Dependencies Installed by GitHub Actions

All these are **automatically installed** by the workflow - no manual installation needed:

1. **html-validate**
   - Purpose: HTML validation
   - Version: Latest
   - Installation: `npm install -g html-validate`

2. **stylelint & stylelint-config-standard**
   - Purpose: CSS linting
   - Installation: `npm install -g stylelint stylelint-config-standard`

3. **eslint**
   - Purpose: JavaScript linting
   - Installation: `npm install -g eslint`

4. **broken-link-checker**
   - Purpose: Link validation
   - Installation: `npm install -g broken-link-checker`

5. **http-server**
   - Purpose: Local testing server
   - Installation: `npm install -g http-server`

6. **@lhci/cli**
   - Purpose: Lighthouse performance testing
   - Installation: `npm install -g @lhci/cli`

7. **Trivy**
   - Purpose: Security scanning
   - Installation: Handled by GitHub Action

### Optional: Local Testing Dependencies

If you want to test locally before pushing:

1. **Install Node.js**
   - Download from https://nodejs.org/
   - Choose LTS version
   - Run installer

2. **Install Global Packages**
   ```bash
   npm install -g html-validate
   npm install -g stylelint stylelint-config-standard
   npm install -g eslint
   npm install -g http-server
   ```

3. **Test Locally**
   ```bash
   # Validate HTML
   html-validate "*.html"
   
   # Validate CSS (create .stylelintrc.json first)
   stylelint "*.css"
   
   # Lint JavaScript (create .eslintrc.json first)
   eslint "*.js"
   
   # Start local server
   http-server . -p 8080
   # Open http://localhost:8080 in browser
   ```

### Configuration Files

The workflow automatically creates these config files:

1. **.htmlvalidate.json** (HTML validation rules)
2. **.stylelintrc.json** (CSS linting rules)
3. **.eslintrc.json** (JavaScript linting rules)

You don't need to create these manually - they're generated during workflow execution.

---

## 5. TESTING AND VERIFICATION

### Test Checklist

After deployment, verify:

- [ ] Website loads at GitHub Pages URL
- [ ] All navigation links work
- [ ] Smooth scrolling functions
- [ ] Responsive design on mobile
- [ ] No console errors in browser DevTools
- [ ] Status badge shows "passing"
- [ ] All workflow jobs succeeded

### Making Test Changes

1. **Edit a File Locally**
   ```bash
   # Open index.html and make a small change
   # Example: Change a heading text
   ```

2. **Commit and Push**
   ```bash
   git add index.html
   git commit -m "Update heading text"
   git push
   ```

3. **Watch Workflow**
   - Go to Actions tab
   - Watch new workflow run
   - Verify it completes successfully
   - Check updated website

### Testing HTML Validation Failures

1. **Introduce HTML Error**
   ```html
   <!-- Add this invalid HTML -->
   <div>Unclosed div
   ```

2. **Push and Observe**
   - Workflow should fail at HTML validation step
   - Check logs to see error details
   - Fix the error and push again

---

## 6. TROUBLESHOOTING

### Common Issues and Solutions

#### Issue 1: Workflow Not Running

**Symptoms:**
- No workflow appears in Actions tab
- Push doesn't trigger workflow

**Solutions:**
1. Verify file location: `.github/workflows/ci.yml`
2. Check YAML syntax (use YAML validator)
3. Ensure file is committed and pushed
4. Check branch name is `main` (not `master`)

#### Issue 2: HTML Validation Fails

**Symptoms:**
- validate-html job fails
- Red X on workflow

**Solutions:**
1. Check HTML syntax
2. Ensure all tags are closed
3. Verify proper DOCTYPE
4. Check for duplicate IDs
5. Review validation logs for specific errors

#### Issue 3: GitHub Pages Not Deploying

**Symptoms:**
- Deploy job succeeds but site doesn't load
- 404 error on Pages URL

**Solutions:**
1. Go to Settings → Pages
2. Verify "Source" is set to "GitHub Actions"
3. Check repository visibility (must be public or have GitHub Pro)
4. Wait 2-3 minutes after deployment
5. Clear browser cache
6. Check deployment logs for errors

#### Issue 4: Permission Denied Errors

**Symptoms:**
- Deploy job fails with permission error
- "Resource not accessible by integration"

**Solutions:**
1. Go to Settings → Actions → General
2. Scroll to "Workflow permissions"
3. Select "Read and write permissions"
4. Check "Allow GitHub Actions to create and approve pull requests"
5. Save changes
6. Re-run workflow

#### Issue 5: Badge Not Showing

**Symptoms:**
- Badge shows "unknown" or doesn't appear
- Image broken in README

**Solutions:**
1. Verify badge URL syntax
2. Replace USERNAME and REPO placeholders
3. Check workflow file name is `ci.yml`
4. Wait for first workflow to complete
5. Hard refresh browser (Ctrl+Shift+R)

#### Issue 6: CSS/JS Not Loading

**Symptoms:**
- Website loads but no styling
- JavaScript not working

**Solutions:**
1. Check file names match exactly (case-sensitive)
2. Verify file paths in HTML are correct
3. Check browser console for 404 errors
4. Ensure files are committed and pushed
5. Clear browser cache

---

## 7. ADVANCED CUSTOMIZATION

### Customizing Workflow Triggers

**Run only on specific files:**
```yaml
on:
  push:
    paths:
      - '**.html'
      - '**.css'
      - '**.js'
```

**Run on schedule:**
```yaml
on:
  schedule:
    - cron: '0 0 * * 0'  # Weekly on Sunday
```

**Run manually only:**
```yaml
on:
  workflow_dispatch:
```

### Adding More Jobs

**Accessibility Testing:**
```yaml
accessibility-test:
  name: A11y Check
  runs-on: ubuntu-latest
  steps:
    - uses: actions/checkout@v4
    - name: Install Pa11y
      run: npm install -g pa11y
    - name: Run accessibility test
      run: pa11y http://localhost:8080
```

**Spell Checking:**
```yaml
spell-check:
  name: Spell Check
  runs-on: ubuntu-latest
  steps:
    - uses: actions/checkout@v4
    - uses: streetsidesoftware/cspell-action@v2
```

### Deploying to Other Platforms

**Netlify:**
```yaml
- name: Deploy to Netlify
  uses: netlify/actions/cli@master
  env:
    NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_TOKEN }}
    NETLIFY_SITE_ID: ${{ secrets.NETLIFY_SITE_ID }}
  with:
    args: deploy --prod --dir=.
```

**Vercel:**
```yaml
- name: Deploy to Vercel
  uses: amondnet/vercel-action@v20
  with:
    vercel-token: ${{ secrets.VERCEL_TOKEN }}
    vercel-org-id: ${{ secrets.ORG_ID }}
    vercel-project-id: ${{ secrets.PROJECT_ID }}
```

---

## 8. CONCLUSION

### What You've Accomplished

✅ Created a professional static website
✅ Implemented complete CI/CD pipeline
✅ Automated HTML/CSS/JavaScript validation
✅ Set up broken link testing
✅ Configured security scanning
✅ Deployed to GitHub Pages
✅ Added status monitoring
✅ Created comprehensive documentation

### Key Takeaways

1. **CI/CD Automation**: You've learned how to automate the entire development workflow
2. **GitHub Actions**: You understand workflow syntax, jobs, and triggers
3. **Quality Assurance**: You've implemented multiple validation layers
4. **Deployment**: You can automatically deploy websites on code changes
5. **Monitoring**: You know how to track build status and debug issues

### Next Steps

1. **Add More Features**
   - Implement contact form
   - Add more pages
   - Include images and media

2. **Enhance CI/CD**
   - Add accessibility testing
   - Implement E2E tests
   - Add code coverage reporting

3. **Performance Optimization**
   - Minify CSS/JavaScript
   - Optimize images
   - Implement CDN

4. **Advanced Topics**
   - Environment variables
   - Secrets management
   - Multi-environment deployment
   - A/B testing

### Resources for Further Learning

- **GitHub Actions Docs**: https://docs.github.com/en/actions
- **GitHub Pages Guide**: https://docs.github.com/en/pages
- **HTML Validation**: https://html-validate.org/
- **CSS Linting**: https://stylelint.io/
- **JavaScript Linting**: https://eslint.org/
- **Lighthouse**: https://developers.google.com/web/tools/lighthouse

### Submission Checklist

For Assignment Submission:

- [ ] Repository URL provided
- [ ] Live website URL provided
- [ ] README.md complete with badge
- [ ] All workflow jobs passing
- [ ] Status badge showing "passing"
- [ ] Website deployed and accessible
- [ ] Documentation clear and complete
- [ ] Customizations documented (if any)

---

## APPENDIX: QUICK REFERENCE

### Essential Git Commands
```bash
git add .                          # Stage all changes
git commit -m "message"            # Commit with message
git push                           # Push to GitHub
git status                         # Check status
git log                            # View commit history
git pull                           # Pull latest changes
```

### Essential GitHub Actions Commands
```yaml
uses: actions/checkout@v4          # Checkout code
uses: actions/setup-node@v4        # Setup Node.js
uses: actions/upload-artifact@v4   # Upload artifacts
uses: actions/download-artifact@v4 # Download artifacts
```

### Workflow Status Commands
```bash
# View workflow runs
gh run list

# View specific run
gh run view [run-id]

# Rerun failed jobs
gh run rerun [run-id]
```

### Local Testing Commands
```bash
# HTML validation
html-validate "*.html"

# CSS validation
stylelint "*.css"

# JavaScript linting
eslint "*.js"

# Start local server
http-server . -p 8080

# Check links
blc http://localhost:8080
```

---

**Document Version:** 1.0
**Last Updated:** February 11, 2026
**Author:** CI/CD Demo Project Team

For questions or issues, please open an issue in the GitHub repository or contact your instructor.

---

**END OF GUIDE**
