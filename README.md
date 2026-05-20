# CyberMailGuard - Phishing Email Detector

ICT932 Cybersecurity Assessment 3 group project.

CyberMailGuard is a Flask web application that analyses suspicious emails and explains whether they are likely phishing. It includes secure login, RBAC, 2FA, email analysis, quarantine, PDF/CSV reports, ML classifier support, and DevSecOps testing evidence.

## Team Members

| Member | Role | GitHub Branch |
|---|---|---|
| Tashi | Auth and Security Lead | feature/auth |
| Giovanni | Email Analysis Lead | feature/email-engine |
| Masaba | Pattern and Risk Engine Lead | feature/pattern-engine |
| Aditi | Frontend and DevOps Lead | feature/dashboard |

## Quick Start on Windows CMD

Open Command Prompt and run:

```cmd
cd C:\Users\Lenovo\Desktop\SecurityProject\CyberMailGuard\backend
venv\Scripts\python.exe -m pip install -r requirements.txt
venv\Scripts\python.exe app.py
```

Then open:

```text
http://127.0.0.1:5000
```

Use `Ctrl + C` in CMD to stop the server.

Important: use `venv\Scripts\python.exe app.py`, not `py app.py`. The `py` command may use your system Python instead of the project virtual environment.

## Setup From a Fresh Clone

```cmd
git clone https://github.com/tashinamgay/CyberMailGuard.git
cd CyberMailGuard\backend
py -m venv venv
venv\Scripts\python.exe -m pip install -r requirements.txt
copy .env.example .env
```

Edit `.env` and add your MongoDB Atlas URI:

```text
SECRET_KEY=change-this-to-a-long-random-secret
MONGO_URI=mongodb+srv://user:pass@cluster.mongodb.net/cybermailguard_ict932?retryWrites=true&w=majority&appName=Cluster0
FLASK_ENV=development
OPENAI_API_KEY=optional
```

Run the app:

```cmd
venv\Scripts\python.exe app.py
```

The first registered user becomes admin automatically.

## Project Structure

```text
backend/
  app.py                  Start server here
  src/
    auth/                 Login, RBAC, 2FA
    email_analysis/       Parser, URL, header and attachment checks
    pattern_engine/       Scoring, ML and quarantine
    dashboard/            Routes, PDF and CSV reports
    database/             MongoDB helpers
  tests/                  Unit and security tests
  locustfile.py           Performance testing

frontend/
  templates/              HTML pages
  static/                 CSS, JavaScript and CIHE logo

docs/                     Architecture, threat model, testing evidence
ci-cd/                    Pipeline documentation
```

## Features

- Secure login with RBAC for admin and analyst users
- Two-factor authentication using authenticator app codes
- Admin user approval, suspend, delete and role management
- Email upload support for `.txt`, `.eml`, and `.docx`
- URL analysis for suspicious domains, HTTP links, shorteners and raw IPs
- Header analysis for spoofing and Reply-To mismatch
- Keyword matching for urgency, finance, credentials and job scams
- Attachment safety checking for dangerous extensions and double extensions
- RED, YELLOW and GREEN risk scoring
- Plain-English explanation of findings
- Automatic quarantine for RED emails
- PDF report download
- CSV export after analyses exist
- Optional ML classifier training
- Admin security panel and login monitoring

## Running Tests

From the backend folder:

```cmd
cd C:\Users\Lenovo\Desktop\SecurityProject\CyberMailGuard\backend
venv\Scripts\python.exe -m pytest
```

Current verified result:

```text
60 passed
```

## Security Scanning

Run from the backend folder:

```cmd
venv\Scripts\python.exe -m bandit -r src -ll -f txt
venv\Scripts\python.exe -m pip_audit
venv\Scripts\python.exe -m locust -f locustfile.py --host=http://localhost:5000
```

OWASP ZAP and Postman were also used for web and API testing evidence.

## DevSecOps Evidence

The project includes evidence files for the ICT932 marking criteria:

- `docs/project3_criteria_mapping.md`
- `docs/devsecops_changes.md`
- `docs/architecture.md`
- `docs/threat_model.md`
- `docs/devsecops_pipeline.md`
- `docs/security_testing_results.md`
- `docs/incident_response.md`
- `docs/testing/pytest_coverage.txt`
- `docs/security/bandit_report.txt`
- `docs/security/pip_audit_report.json`
- `docs/screenshots/`

## Notes

If the browser shows `The CSRF token has expired`, refresh the page with `Ctrl + F5`, log in again if needed, and submit the form again. This is normal security behaviour after the server restarts or an old form stays open too long.
