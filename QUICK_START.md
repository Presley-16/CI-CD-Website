# CI/CD Quick Start Cheat Sheet

## 🚀 Fast Setup (10 Minutes)

### 1. Create GitHub Repo
```bash
# On GitHub.com:
# New Repository → Name: ci-cd-demo → Public → Create
```

### 2. Clone and Setup
```bash
git clone https://github.com/YOUR-USERNAME/ci-cd-demo.git
cd ci-cd-demo
```

### 3. Copy All Files
Copy these files from the project:
- ✅ index.html
- ✅ styles.css
- ✅ script.js
- ✅ .github/workflows/ci.yml
- ✅ README.md
- ✅ .gitignore

### 4. Update README
Replace in README.md:
- YOUR-USERNAME → your GitHub username
- YOUR-REPO-NAME → your repo name

### 5. Push to GitHub
```bash
git add .
git commit -m "Add CI/CD pipeline"
git push origin main
```

### 6. Enable GitHub Pages
1. Go to Settings → Pages
2. Source: GitHub Actions
3. Save

### 7. Watch It Deploy
1. Go to Actions tab
2. Watch workflow run
3. Get your URL: https://YOUR-USERNAME.github.io/ci-cd-demo/

---

## 📋 Essential Commands

### Git Workflow
```bash
git status              # Check changes
git add .               # Stage all
git commit -m "msg"     # Commit
git push                # Push to GitHub
```

### Local Testing (Optional)
```bash
# Install tools
npm install -g html-validate stylelint eslint http-server

# Test files
html-validate "*.html"
stylelint "*.css"
eslint "*.js"

# Run local server
http-server . -p 8080
# Visit: http://localhost:8080
```

---

## ⚠️ Common Issues

### Workflow Not Running
- ✅ Check: `.github/workflows/ci.yml` exists
- ✅ Branch is `main` (not master)
- ✅ File is pushed to GitHub

### Pages Not Deploying
- ✅ Settings → Pages → Source: GitHub Actions
- ✅ Wait 2-3 minutes
- ✅ Check deploy job succeeded

### Permission Error
- ✅ Settings → Actions → General
- ✅ Workflow permissions: Read/Write
- ✅ Save and re-run

### Badge Not Showing
- ✅ Update USERNAME and REPO-NAME in badge URL
- ✅ Wait for first workflow to complete
- ✅ Hard refresh (Ctrl+Shift+R)

---

## 📊 Workflow Jobs

| Job | What It Does | Time |
|-----|--------------|------|
| validate-html | Checks HTML syntax | ~30s |
| validate-css | Lints CSS files | ~30s |
| lint-javascript | Checks JS code | ~30s |
| test-links | Tests for broken links | ~45s |
| security-scan | Scans for vulnerabilities | ~1m |
| build | Packages website | ~20s |
| deploy | Deploys to Pages | ~1m |
| performance-test | Runs Lighthouse | ~1m |

**Total Time:** ~5 minutes

---

## 🎯 Quick Validation

### Before Pushing
```bash
# Check HTML
html-validate index.html

# Check CSS  
stylelint styles.css

# Check JS
eslint script.js
```

### After Pushing
1. ✅ Actions tab shows green checkmarks
2. ✅ Badge shows "passing"
3. ✅ Website loads at Pages URL
4. ✅ All features work

---

## 🔧 File Structure
```
ci-cd-demo/
├── .github/
│   └── workflows/
│       └── ci.yml          ← CI/CD pipeline
├── .gitignore              ← Ignore rules
├── index.html              ← Main page
├── styles.css              ← Styling
├── script.js               ← Interactivity
└── README.md               ← Documentation
```

---

## 🎓 Assignment Checklist

- [ ] Repository created on GitHub
- [ ] All files added and committed
- [ ] Workflow running successfully
- [ ] HTML validation passing
- [ ] CSS validation passing
- [ ] JavaScript linting passing
- [ ] Link testing passing
- [ ] Deployment to GitHub Pages working
- [ ] Status badge integrated
- [ ] README updated with your info
- [ ] Website accessible at Pages URL
- [ ] Documentation complete

---

## 📚 Quick Links

- **GitHub Actions**: https://docs.github.com/en/actions
- **GitHub Pages**: https://docs.github.com/en/pages
- **html-validate**: https://html-validate.org/
- **Stylelint**: https://stylelint.io/
- **ESLint**: https://eslint.org/

---

## 💡 Pro Tips

1. **Test locally first** - Catch errors before pushing
2. **Read workflow logs** - They show exactly what failed
3. **Start simple** - Get basic pipeline working first
4. **Use badge** - Shows build status at a glance
5. **Commit often** - Smaller commits are easier to debug

---

## 🆘 Need Help?

1. Check IMPLEMENTATION_GUIDE.md for detailed steps
2. Read README.md for complete documentation
3. Review workflow logs in Actions tab
4. Check GitHub Actions documentation
5. Open an issue in your repository

---

**Quick Start Time:** 10 minutes
**Full Setup Time:** 30 minutes with testing
**Skill Level:** Beginner-friendly

Good luck! 🚀
