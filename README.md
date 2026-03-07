# CI/CD Demo Website

[![CI/CD Pipeline](https://github.com/Presley-16/CI-CD-Website/actions/workflows/ci.yml/badge.svg)](https://github.com/Presley-16/CI-CD-Website/actions/workflows/ci.yml)

A demonstration of Continuous Integration and Continuous Deployment (CI/CD) using GitHub Actions for a simple static website.

## 🌐 Live Demo

Visit the live website: [https://presley-16.github.io/CI-CD-Website/](https://presley-16.github.io/CI-CD-Website/)

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [CI/CD Pipeline](#cicd-pipeline)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Workflow Details](#workflow-details)
- [Dependencies](#dependencies)
- [Deployment](#deployment)
- [Customization](#customization)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Project Overview

This project demonstrates the implementation of a complete CI/CD pipeline for a static website using GitHub Actions. Every push to the main branch automatically:

- Validates HTML and CSS
- Lints JavaScript code
- Tests for broken links
- Performs security scans
- Builds the website
- Deploys to GitHub Pages

## ✨ Features

### Website Features
- **Responsive Design**: Mobile-friendly layout
- **Modern UI**: Clean and professional design
- **Smooth Animations**: Scroll-based animations
- **Navigation**: Smooth scrolling navigation
- **Performance**: Optimized for fast loading

### CI/CD Features
- **Automated Validation**: HTML, CSS, and JavaScript validation
- **Link Testing**: Automatic broken link detection
- **Security Scanning**: Trivy vulnerability scanner
- **Performance Testing**: Lighthouse CI audits
- **Automated Deployment**: Push to GitHub Pages on success
- **Status Monitoring**: Real-time build status badges
- **Artifact Storage**: Build artifacts saved for 30 days

## 🔄 CI/CD Pipeline

The pipeline consists of 8 jobs:

1. **HTML Validation** - Validates HTML structure using html-validate
2. **CSS Validation** - Lints CSS using Stylelint
3. **JavaScript Linting** - Checks JavaScript with ESLint
4. **Link Checker** - Tests all links for broken references
5. **Security Scan** - Scans for vulnerabilities with Trivy
6. **Build** - Packages the website and creates artifacts
7. **Deploy** - Deploys to GitHub Pages (main branch only)
8. **Performance Test** - Runs Lighthouse performance audits

## 🚀 Getting Started

### Prerequisites

Before you begin, ensure you have:
- A GitHub account
- Git installed on your local machine
- A text editor (VS Code, Sublime, etc.)
- Basic knowledge of HTML, CSS, and JavaScript

### Installation Steps

#### Step 1: Create GitHub Repository

1. Go to [GitHub](https://github.com) and log in
2. Click the "+" icon in the top right
3. Select "New repository"
4. Name your repository (e.g., `ci-cd-demo`)
5. Choose "Public" visibility
6. Click "Create repository"

#### Step 2: Clone and Setup Project

```bash
# Clone your repository
git clone https://github.com/YOUR-USERNAME/YOUR-REPO-NAME.git
cd YOUR-REPO-NAME

# Copy all project files to your repository
# (Copy index.html, styles.css, script.js, and .github folder)

# Initialize git (if not already done)
git init

# Add all files
git add .

# Commit changes
git commit -m "Initial commit: Add CI/CD demo website"

# Push to GitHub
git push -u origin main
```

#### Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click "Settings" tab
3. Navigate to "Pages" in the left sidebar
4. Under "Source", select "GitHub Actions"
5. Save the changes

#### Step 4: Update README Badge

Edit the README.md file and replace:
- `YOUR-USERNAME` with your GitHub username
- `YOUR-REPO-NAME` with your repository name

```markdown
[![CI/CD Pipeline](https://github.com/YOUR-USERNAME/YOUR-REPO-NAME/actions/workflows/ci.yml/badge.svg)](https://github.com/YOUR-USERNAME/YOUR-REPO-NAME/actions/workflows/ci.yml)
```

#### Step 5: Verify Workflow

1. Go to the "Actions" tab in your repository
2. You should see the CI/CD Pipeline running
3. Click on the workflow to see detailed logs
4. Wait for all jobs to complete (green checkmarks)

## 📁 Project Structure

```
ci-cd-demo/
├── .github/
│   └── workflows/
│       └── ci.yml           # GitHub Actions workflow
├── index.html               # Main HTML file
├── styles.css               # CSS stylesheet
├── script.js                # JavaScript file
└── README.md                # This file
```

## 🔧 Workflow Details

### Trigger Conditions

The workflow runs when:
- Code is pushed to the `main` branch
- Changes are made to HTML, CSS, JS, or workflow files
- Pull requests are opened to `main`
- Manually triggered via workflow_dispatch

### Job Dependencies

```
validate-html ─┐
validate-css ──┼─→ build ─→ deploy
lint-js ───────┘      ↓
test-links ───────────┘
```

### Validation Tools

| Tool | Purpose | Configuration |
|------|---------|---------------|
| html-validate | HTML validation | `.htmlvalidate.json` |
| Stylelint | CSS linting | `.stylelintrc.json` |
| ESLint | JavaScript linting | `.eslintrc.json` |
| broken-link-checker | Link testing | CLI options |
| Trivy | Security scanning | Built-in |
| Lighthouse CI | Performance | Auto-generated |

## 📦 Dependencies

### Runtime Dependencies
All dependencies are installed automatically by GitHub Actions:

- **Node.js 18**: JavaScript runtime
- **html-validate**: HTML validation
- **stylelint**: CSS linting
- **stylelint-config-standard**: Stylelint rules
- **eslint**: JavaScript linting
- **broken-link-checker**: Link validation
- **http-server**: Local testing server
- **@lhci/cli**: Lighthouse CI
- **Trivy**: Security scanner

### Development Dependencies (Optional)

For local development, install Node.js and run:

```bash
# Install validation tools globally
npm install -g html-validate
npm install -g stylelint stylelint-config-standard
npm install -g eslint
npm install -g broken-link-checker
npm install -g http-server

# Or use npx to run without installing
npx html-validate "*.html"
npx stylelint "*.css"
npx eslint "*.js"
```

## 🌐 Deployment

### Automatic Deployment

Deployment happens automatically when:
1. Code is pushed to the `main` branch
2. All validation jobs pass successfully
3. Build job completes without errors

### Manual Deployment

You can manually trigger deployment:
1. Go to "Actions" tab
2. Select "CI/CD Pipeline"
3. Click "Run workflow"
4. Select `main` branch
5. Click "Run workflow" button

### Deployment URL

After successful deployment, your site will be available at:
```
https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/
```

## ⚙️ Customization

### Customize Workflow Triggers

Edit `.github/workflows/ci.yml`:

```yaml
# Run only on specific file changes
on:
  push:
    branches:
      - main
    paths:
      - 'src/**'
      - '*.html'

# Run on schedule
on:
  schedule:
    - cron: '0 0 * * 0'  # Weekly on Sunday
```

### Add More Validation

Add new jobs to the workflow:

```yaml
accessibility-test:
  name: Accessibility Check
  runs-on: ubuntu-latest
  steps:
    - uses: actions/checkout@v4
    - name: Run Pa11y
      run: |
        npm install -g pa11y-ci
        pa11y-ci --sitemap http://localhost:8080/sitemap.xml
```

### Custom Deployment

Deploy to other platforms:

```yaml
deploy-to-netlify:
  runs-on: ubuntu-latest
  steps:
    - uses: actions/checkout@v4
    - name: Deploy to Netlify
      uses: netlify/actions/cli@master
      with:
        args: deploy --prod
      env:
        NETLIFY_SITE_ID: ${{ secrets.NETLIFY_SITE_ID }}
        NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
```

## 🐛 Troubleshooting

### Common Issues

**Issue: Workflow fails on HTML validation**
- Check HTML syntax in your files
- Review the validation logs in Actions tab
- Ensure all tags are properly closed

**Issue: GitHub Pages not deploying**
- Verify GitHub Pages is enabled in Settings
- Check that deployment job completed successfully
- Ensure repository is public or GitHub Pages is enabled for private repos

**Issue: Badge not showing**
- Update badge URL with correct username and repo name
- Wait a few minutes after first workflow run
- Check badge syntax in README.md

### Viewing Logs

1. Go to "Actions" tab
2. Click on the workflow run
3. Click on individual jobs to see detailed logs
4. Download artifacts for detailed validation results

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is open source and available under the MIT License.

## 📚 Additional Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [HTML Validation](https://html-validate.org/)
- [Stylelint Rules](https://stylelint.io/user-guide/rules)
- [ESLint Documentation](https://eslint.org/docs/latest/)

## 🎓 Learning Objectives

By completing this project, you will:
- ✅ Understand CI/CD concepts and workflows
- ✅ Learn GitHub Actions syntax and configuration
- ✅ Implement automated validation and testing
- ✅ Deploy static websites automatically
- ✅ Monitor build status and handle failures
- ✅ Customize workflows for specific needs

## 🏆 Evaluation Checklist

- [x] CI workflow with build and validation steps implemented
- [x] HTML validation configured
- [x] CSS validation configured
- [x] JavaScript linting configured
- [x] Link testing included
- [x] Workflow triggers customized
- [x] Status badge integrated
- [x] Deployment to GitHub Pages configured
- [x] Documentation complete and clear
- [x] Security scanning included
- [x] Performance testing added

---

**Built with ❤️ using GitHub Actions**

For questions or issues, please open an issue in the repository.
