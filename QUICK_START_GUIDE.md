# Quick Start Guide - Jenkins CI/CD Pipeline

**Student:** Hassan Khalil (202300935)

---

## Step-by-Step Instructions

### 1. Create GitHub Repository

Go to https://github.com and create a new repository:
- **Repository name:** `jenkins_project`
- **Visibility:** Public (or Private if you prefer)
- **DO NOT** initialize with README (we already have files)

### 2. Push Code to GitHub

Open terminal in the jenkins_project directory and run:

```bash
# Add the remote repository
git remote add origin https://github.com/hassankhalill/jenkins_project.git

# Rename branch to main (if needed)
git branch -M main

# Push to GitHub
git push -u origin main
```

If asked for credentials:
- **Username:** hassankhalill
- **Password:** Use a Personal Access Token (not your password)

To create a Personal Access Token:
1. Go to GitHub Settings > Developer settings > Personal access tokens > Tokens (classic)
2. Click "Generate new token (classic)"
3. Give it a name like "Jenkins Lab"
4. Select scopes: `repo` (all repo permissions)
5. Click "Generate token"
6. Copy and save the token (you won't see it again!)

### 3. Install Jenkins

#### On Windows:

1. Download Jenkins from:
   https://www.jenkins.io/download/thank-you-downloading-windows-installer-stable/

2. Run the installer (.msi file)

3. Follow the installation wizard:
   - Default port: 8080
   - Install as Windows service: Yes

4. After installation, Jenkins will start automatically

5. Open browser and go to: http://localhost:8080/

6. Unlock Jenkins:
   - Find the password in: `C:\ProgramData\Jenkins\.jenkins\secrets\initialAdminPassword`
   - Copy and paste it into the unlock page

7. Install suggested plugins (click "Install suggested plugins")

8. Create your admin user:
   - Username: hassankhalil (or anything you like)
   - Password: (choose a password)
   - Full name: Hassan Khalil
   - Email: hmk60@mail.aub.edu

9. Keep the default Jenkins URL: http://localhost:8080/

10. Click "Start using Jenkins"

### 4. Install Required Jenkins Plugins

1. Go to **Manage Jenkins** (left sidebar)
2. Click **Manage Plugins**
3. Click **Available** tab
4. Search for and install these plugins:
   - **Git Plugin** (usually pre-installed)
   - **Pipeline Plugin** (usually pre-installed)
   - **HTML Publisher Plugin** (IMPORTANT - for coverage reports)
   - **SSH Agent Plugin**

5. Check "Restart Jenkins when installation is complete"

### 5. Create Jenkins Pipeline Job

1. From Jenkins Dashboard, click **New Item**

2. Enter item name: `Python-CI-CD`

3. Select: **Pipeline**

4. Click **OK**

5. In the configuration page:

   **General Section:**
   - Description: "Jenkins CI/CD Pipeline for Python application by Hassan Khalil (202300935)"

   **Pipeline Section:**
   - Definition: Select **Pipeline script from SCM**
   - SCM: Select **Git**
   - Repository URL: `https://github.com/hassankhalill/jenkins_project.git`
   - Credentials: (leave as none if repo is public)
   - Branch Specifier: `*/main`
   - Script Path: `Jenkinsfile`

6. Click **Save**

### 6. Run the Pipeline

1. On the job page, click **Build Now**

2. Watch the build in the **Build History** (lower left)

3. Click on the build number (e.g., #1)

4. Click **Console Output** to see detailed logs

5. Wait for all stages to complete

### 7. View Results

After successful build:

1. **Pipeline Stages:**
   - Click on the build number
   - You'll see: Setup ✓ Lint ✓ Test ✓ Coverage ✓ Security Scan ✓ Deploy ✓

2. **Coverage Report:**
   - Click on **Coverage Report** link on the build page
   - View the HTML coverage report showing 100% coverage

3. **Build Artifacts:**
   - Scroll down to **Build Artifacts** section
   - Download: `bandit-report.txt`
   - Download: `deployment-info.txt`

---

## Taking Screenshots

### Screenshot 1: Jenkins Dashboard
**Location:** http://localhost:8080/
**Show:** Main dashboard with Python-CI-CD job visible
**When to take:** After creating the job

### Screenshot 2: Job Configuration
**Location:** Job page > Configure
**Show:** Git repository URL and pipeline settings
**When to take:** During job setup

### Screenshot 3: Pipeline Execution
**Location:** Build page (click on build #1)
**Show:** All 6 stages in green (passed)
**When to take:** After successful build

### Screenshot 4: Console Output
**Location:** Build page > Console Output
**Show:** Full build log showing all stages
**When to take:** After successful build

### Screenshot 5: Coverage Report
**Location:** Build page > Coverage Report
**Show:** HTML coverage report with 100% coverage
**When to take:** After successful build

### Screenshot 6: Build Artifacts
**Location:** Build page (scroll down)
**Show:** List of archived artifacts
**When to take:** After successful build

### Screenshot 7: Security Report Content
**Location:** Build page > Download bandit-report.txt > Open it
**Show:** Contents of security scan
**When to take:** After downloading artifact

---

## What to Submit to Moodle

### File 1: Text File with GitHub Link
**Filename:** `jenkins_submission_Hassan_Khalil_202300935.txt`
**Location:** Already created in the project folder
**Content:** Contains GitHub repository URL and submission details

### File 2: PDF Report with Screenshots
**Filename:** `Lab10_Report_Hassan_Khalil_202300935.pdf`

**How to create:**
1. Open `LAB_REPORT.md` in a Markdown viewer or VS Code
2. Insert the 7 screenshots you took in appropriate sections
3. Export/Print as PDF

**Recommended structure:**
- Cover page with your name and ID
- Introduction
- All screenshots with captions
- Jenkinsfile code
- Explanation of changes
- Conclusion

---

## Troubleshooting

### Problem: Jenkins won't start
**Solution:**
- Check if port 8080 is available
- Restart Jenkins service from Windows Services
- Check logs in `C:\ProgramData\Jenkins\.jenkins\logs`

### Problem: Build fails at Setup stage
**Solution:**
- Ensure Python is installed and in PATH
- Run `python --version` in Command Prompt
- Install Python from https://www.python.org/downloads/ if needed

### Problem: Build fails at Test stage
**Solution:**
- Check that app.py has your name in the greet function
- Verify test_app.py expects the correct output
- Both should include "Hassan Khalil"

### Problem: Coverage report not visible
**Solution:**
- Install HTML Publisher plugin
- Restart Jenkins after installing
- Rebuild the job

### Problem: Git authentication fails
**Solution:**
- Use HTTPS URL, not SSH
- Create Personal Access Token on GitHub
- Use token as password when pushing

### Problem: Can't find initial admin password
**Solution:**
- Look in: `C:\ProgramData\Jenkins\.jenkins\secrets\initialAdminPassword`
- Open with Notepad
- Copy the entire string

---

## Expected Build Time

- First build: 3-5 minutes (installs all dependencies)
- Subsequent builds: 1-2 minutes (uses existing environment)

---

## Verification Checklist

Before submitting, verify:

- [ ] GitHub repository created and code pushed
- [ ] Jenkins installed and running
- [ ] Python-CI-CD job created in Jenkins
- [ ] Job configured with correct GitHub URL
- [ ] Build runs successfully (all stages green)
- [ ] All 6 stages pass: Setup, Lint, Test, Coverage, Security Scan, Deploy
- [ ] Coverage report accessible and shows 100%
- [ ] Build artifacts present (bandit-report.txt, deployment-info.txt)
- [ ] All 7 screenshots taken
- [ ] Submission text file ready
- [ ] PDF report created with screenshots

---

## Contact Information

**Student:** Hassan Khalil
**ID:** 202300935
**Email:** hmk60@mail.aub.edu
**GitHub:** https://github.com/hassankhalill

---

## Additional Resources

- **Jenkins Documentation:** https://www.jenkins.io/doc/
- **Jenkins Pipeline Tutorial:** https://www.jenkins.io/doc/pipeline/tour/hello-world/
- **Python Virtual Environments:** https://docs.python.org/3/library/venv.html
- **Pytest Documentation:** https://docs.pytest.org/
- **Coverage.py:** https://coverage.readthedocs.io/
- **Bandit Security Scanner:** https://bandit.readthedocs.io/

---

**Good luck with your Jenkins setup!**

If you encounter any issues not covered here, check the detailed README.md and LAB_REPORT.md files.
