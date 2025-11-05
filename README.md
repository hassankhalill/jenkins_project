# Jenkins CI/CD Pipeline Project

**Student:** Hassan Khalil
**ID:** 202300935
**Course:** EECE 435L - Software Tools Lab
**GitHub:** hassankhalill

---

## Project Overview

This project implements a complete CI/CD pipeline using Jenkins for a Python application. The pipeline includes automated testing, code quality checks, security scanning, code coverage analysis, and deployment automation.

---

## Project Structure

```
jenkins_project/
├── app.py                          # Main Python application
├── tests/
│   └── test_app.py                 # Unit tests
├── requirements.txt                # Python dependencies
├── Jenkinsfile                     # Jenkins pipeline (cross-platform)
├── Jenkinsfile_Hassan_Khalil      # Jenkins pipeline (Windows specific)
├── .gitignore                      # Git ignore rules
└── README.md                       # This file
```

---

## Features Implemented

### Pipeline Stages

1. **Setup Stage**
   - Creates Python virtual environment
   - Installs all dependencies from requirements.txt

2. **Lint Stage**
   - Runs flake8 for code style checking
   - Ensures PEP 8 compliance

3. **Test Stage**
   - Executes unit tests using pytest
   - Validates application functionality

4. **Coverage Stage** (Part 4 - Exercise)
   - Runs code coverage analysis using coverage.py
   - Generates HTML coverage report
   - Publishes report in Jenkins

5. **Security Scan Stage** (Part 4 - Exercise)
   - Performs security vulnerability scanning using bandit
   - Generates security report
   - Archives the report as Jenkins artifact

6. **Deploy Stage** (Part 4 - Exercise)
   - Simulates application deployment
   - Creates deployment artifact with timestamp
   - Logs deployment information

---

## Local Testing (Before Jenkins)

Before pushing to Jenkins, you can test locally:

### 1. Install Dependencies
```bash
python -m venv venv
venv\Scripts\activate        # On Windows
# source venv/bin/activate   # On Linux/Mac
pip install -r requirements.txt
```

### 2. Run Tests
```bash
pytest tests/ -v
```

### 3. Check Code Style
```bash
flake8 app.py --max-line-length=120
```

### 4. Run Coverage
```bash
coverage run -m pytest tests/
coverage report -m
coverage html
```

### 5. Run Security Scan
```bash
bandit -r . -f txt
```

---

## Setting Up Jenkins

### Prerequisites
- Jenkins installed (download from https://www.jenkins.io/download/)
- Python 3.x installed on Jenkins server
- Git installed

### Required Jenkins Plugins
1. **Git Plugin** - For Git integration
2. **Pipeline Plugin** - For Jenkins pipelines
3. **HTML Publisher Plugin** - For coverage reports

### Installing Jenkins on Windows

1. Download Jenkins installer from:
   https://www.jenkins.io/download/thank-you-downloading-windows-installer-stable/

2. Run the installer and follow setup wizard

3. Start Jenkins (usually runs on http://localhost:8080/)

4. Unlock Jenkins using the initial admin password from:
   `C:\ProgramData\Jenkins\.jenkins\secrets\initialAdminPassword`

5. Install suggested plugins

6. Create admin user

---

## Creating the Jenkins Pipeline

### Step 1: Create GitHub Repository

1. Go to https://github.com and create a new repository named `jenkins_project`
2. Push your code:

```bash
cd jenkins_project
git add .
git commit -m "Initial commit - Jenkins CI/CD Pipeline Project by Hassan Khalil (202300935)"
git branch -M main
git remote add origin https://github.com/hassankhalill/jenkins_project.git
git push -u origin main
```

### Step 2: Create Jenkins Job

1. Open Jenkins Dashboard (http://localhost:8080/)
2. Click **New Item**
3. Enter name: `Python-CI-CD`
4. Select **Pipeline** project type
5. Click **OK**

### Step 3: Configure Pipeline

1. In the job configuration page, scroll to **Pipeline** section
2. Select **Pipeline script from SCM**
3. Set **SCM** to **Git**
4. Enter repository URL: `https://github.com/hassankhalill/jenkins_project.git`
5. Set branch to: `*/main`
6. Script Path: `Jenkinsfile` (or `Jenkinsfile_Hassan_Khalil` for Windows-specific)
7. Click **Save**

### Step 4: Run the Pipeline

1. Click **Build Now** on the job page
2. Watch the pipeline execute through all stages
3. View console output for detailed logs
4. Access build artifacts and coverage reports

---

## Taking Screenshots for Submission

### Screenshot 1: Jenkins Dashboard
- Show the main Jenkins dashboard with your job listed
- **When:** After creating the job

### Screenshot 2: Job Configuration
- Show the pipeline configuration with Git repository URL
- **When:** During job setup

### Screenshot 3: Pipeline Stages View
- Show all pipeline stages (Setup, Lint, Test, Coverage, Security Scan, Deploy)
- **When:** After successful build

### Screenshot 4: Console Output
- Show the console output with all stages passing
- **When:** After successful build

### Screenshot 5: Coverage Report
- Click on "Coverage Report" link in build
- Show the HTML coverage report
- **When:** After successful build

### Screenshot 6: Build Artifacts
- Show the archived artifacts (bandit-report.txt, deployment-info.txt)
- **When:** After successful build

### Screenshot 7: Security Scan Report
- Open and show the bandit security scan results
- **When:** After successful build

---

## Expected Pipeline Output

When the pipeline runs successfully, you should see:

```
✓ Setup - Creates virtual environment and installs dependencies
✓ Lint - Code passes flake8 style checks
✓ Test - All unit tests pass
✓ Coverage - Code coverage report generated
✓ Security Scan - Security vulnerabilities checked
✓ Deploy - Application deployed successfully
```

---

## What to Submit to Moodle

### 1. Create a text file with the following information:

**File name:** `jenkins_submission_Hassan_Khalil_202300935.txt`

**Content:**
```
Student Name: Hassan Khalil
Student ID: 202300935
GitHub Repository: https://github.com/hassankhalill/jenkins_project
Jenkins Job Name: Python-CI-CD

Lab Completion Notes:
- All required stages implemented (Setup, Lint, Test)
- Additional stages added (Coverage, Security Scan, Deploy)
- Code coverage analysis implemented using coverage.py
- Security scanning implemented using bandit
- Deployment script created
- All tests passing
- Pipeline runs successfully
```

### 2. Create a brief report (PDF):

**File name:** `Lab10_Report_Hassan_Khalil_202300935.pdf`

Include:
- Modified Jenkinsfile (both versions)
- Explanation of changes made for Part 4
- Screenshots of successful Jenkins build
- Coverage report results
- Security scan results
- Deployment output

---

## Troubleshooting

### Issue: Python not found
**Solution:** Ensure Python is in system PATH or specify full path in Jenkinsfile

### Issue: pip install fails
**Solution:** Upgrade pip: `python -m pip install --upgrade pip`

### Issue: Tests fail
**Solution:** Check that app.py returns the correct string with your name

### Issue: Coverage report not showing
**Solution:** Install HTML Publisher plugin in Jenkins

### Issue: Git authentication required
**Solution:** Use GitHub personal access token or SSH keys

---

## Dependencies

All dependencies are listed in `requirements.txt`:
- **flake8** - Code style checker
- **pytest** - Testing framework
- **coverage** - Code coverage tool
- **bandit** - Security vulnerability scanner

---

## Additional Notes

- The pipeline is cross-platform compatible (works on both Windows and Linux)
- Two Jenkinsfiles provided: one generic, one Windows-specific
- All Part 4 requirements completed:
  - Code coverage analysis ✓
  - Security scanning ✓
  - Deployment implementation ✓

---

## Contact

For questions or issues:
- **Email:** hmk60@mail.aub.edu
- **GitHub:** https://github.com/hassankhalill

---

## License

This project is for educational purposes as part of EECE 435L coursework.
