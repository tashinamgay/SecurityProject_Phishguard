# ðŸ›¡ï¸ CyberMailGuard â€” Phishing Email Detector
> ICT932 Cybersecurity Assessment 3 â€” Group Project

---

## ðŸ‘¥ Team Members

| Member | Role | GitHub Branch |
|--------|------|---------------|
| **Tashi** | Auth & Security Lead | feature/auth |
| **Giovanni** | Email Analysis Lead | feature/email-engine |
| **Masaba** | Pattern & Risk Engine Lead | feature/pattern-engine |
| **Aditi** | Frontend & DevOps Lead | feature/dashboard |

---

## ðŸš€ Quick Start

### 1. Clone the repo
```bash
git clone https://github.com/tashinamgay/CyberMailGuard.git
cd CyberMailGuard
```

### 2. Setup
```bash
cd backend
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # Mac/Linux
pip install -r requirements.txt
```

### 3. Configure .env
```bash
copy .env.example .env
```
Edit `.env` and add your MongoDB Atlas URI:
```
SECRET_KEY=change-this-to-a-long-random-secret
MONGO_URI=mongodb+srv://user:pass@cluster.mongodb.net/cybermailguard_ict932?retryWrites=true&w=majority&appName=Cluster0
FLASK_ENV=development
OPENAI_API_KEY=optional
```

### 4. Run
```bash
python app.py
```
Open: **http://localhost:5000**

> â­ First user to register = Admin automatically!

---

## ðŸ“ Project Structure

```
â”œâ”€â”€ backend/
â”‚   â”œâ”€â”€ app.py                    â† Start server here
â”‚   â”œâ”€â”€ src/
â”‚   â”‚   â”œâ”€â”€ auth/                 â† Tashi: Login, RBAC, 2FA
â”‚   â”‚   â”œâ”€â”€ email_analysis/       â† Giovanni: Parser, URLs, Headers
â”‚   â”‚   â”œâ”€â”€ pattern_engine/       â† Masaba: Scoring, ML, Quarantine
â”‚   â”‚   â”œâ”€â”€ dashboard/            â† Aditi: Routes, PDF/CSV
â”‚   â”‚   â””â”€â”€ database/             â† MongoDB helpers
â”‚   â”œâ”€â”€ tests/                    â† All unit tests
â”‚   â””â”€â”€ locustfile.py             â† Performance testing
â””â”€â”€ frontend/
    â”œâ”€â”€ templates/                â† All HTML pages
    â””â”€â”€ static/                   â† CSS + JS
```

---

## âœ… Features

- ðŸ” Secure login with RBAC (Admin/Analyst)
- ðŸ“± Two-Factor Authentication (2FA)
- ðŸ‘¥ Admin: approve/suspend/delete/change role
- ðŸ” URL analysis (suspicious domains, shorteners)
- ðŸ“‹ Header analysis (spoofed sender detection)
- ðŸ”‘ Keyword matching (urgency, financial, credentials, job scams)
- ðŸ“Ž Attachment safety checking
- ðŸ¤– AI explanation of findings
- ðŸ§  ML classifier (optional)
- ðŸ”´ RED/YELLOW/GREEN risk scoring
- ðŸ”’ Auto-quarantine RED emails
- ðŸ“¥ PDF + CSV export
- ðŸ“Š Admin security panel
- ðŸ“± Fully responsive design

---

## ðŸ§ª Running Tests

```bash
cd backend
pytest tests/ -v --cov=src
```

## ðŸ” Security Scanning

```bash
# SAST - Bandit
bandit -r src/ -ll -f txt

# Dependency scan
pip install pip-audit
python -m pip_audit

# Performance test
python -m locust -f locustfile.py --host=http://localhost:5000
```

## ðŸ”„ CI/CD Pipeline

```
Push to GitHub -> Build -> Bandit SAST -> pip-audit -> pytest -> OWASP ZAP -> Deploy Gate
```
 
## DevSecOps Evidence

The project includes evidence files for the ICT932 DevSecOps marking criteria:

- `docs/devsecops_changes.md` - security fixes and pipeline improvements
- `docs/architecture.md` - system architecture and security architecture
- `docs/threat_model.md` - STRIDE threat model and OWASP mapping
- `docs/devsecops_pipeline.md` - CI/CD pipeline stages and evidence mapping
- `docs/security_testing_results.md` - Bandit, pip-audit, pytest, and OWASP Top 10 mapping
- `docs/incident_response.md` - failed-login incident response simulation
- `docs/testing/pytest_coverage.txt` - pytest and coverage output
- `docs/security/bandit_report.txt` - SAST report
- `docs/security/pip_audit_report.json` - dependency scan report
- `docs/screenshots/` - screenshot-style evidence images for the report appendix

Current verified local result:

```text
56 tests passed
47% total coverage
Bandit high-severity scan: 0 high issues
pip-audit: 0 known vulnerable dependencies
```
