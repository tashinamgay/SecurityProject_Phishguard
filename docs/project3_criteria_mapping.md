# Project 3 Criteria Mapping

This document maps the ICT 932 Project 3 phishing email detector requirements to the CyberMailGuard implementation.

## Objective

CyberMailGuard analyzes submitted email text or `.eml` and `.txt` files, detects phishing indicators with pattern matching and heuristics, assigns a RED, YELLOW, or GREEN risk result, explains the findings, and supports reporting and quarantine review.

## Core Feature Coverage

| Requirement | Status | Implementation evidence |
|---|---|---|
| Secure login with RBAC and 2FA | Complete | `backend/src/auth/routes.py`, `backend/src/auth/rbac.py`, `backend/src/auth/twofa.py`, `frontend/templates/auth/verify_2fa.html` |
| URL analysis with suspicious domain detection | Complete | `backend/src/email_analysis/url_checker.py` checks shorteners, suspicious TLDs, raw IP URLs, insecure HTTP, and suspicious domain words |
| Keyword pattern matching | Complete | `backend/src/pattern_engine/keywords.py` and `backend/src/pattern_engine/risk_scorer.py` detect urgency, financial, credential, and job scam wording |
| Header analysis | Complete | `backend/src/email_analysis/header_checker.py` checks sender and Reply-To mismatch, SPF, DKIM, DMARC, and suspicious display names |
| Attachment safety checking | Complete | `backend/src/email_analysis/attachment.py` flags dangerous extensions, archives, macro files, and double extensions |
| Visual risk indicators | Complete | `backend/src/pattern_engine/risk_scorer.py` produces RED, YELLOW, and GREEN results; `frontend/templates/dashboard/results.html` displays score, level, and detailed reasoning |
| Email quarantine feature | Complete | RED emails are automatically quarantined in `backend/src/dashboard/routes.py`; admin review and release use `backend/src/pattern_engine/quarantine.py` and `frontend/templates/dashboard/quarantine.html` |
| Exportable analysis reports | Complete | PDF export is available per analysis in `backend/src/dashboard/reports.py`; CSV export is available only after analyses exist |
| Optional ML extension | Complete | `backend/src/pattern_engine/ml_classifier.py` trains a TF-IDF and Naive Bayes classifier from a CSV dataset with `text` and `label` columns |

## Technical Requirement Coverage

| Requirement | Status | Implementation evidence |
|---|---|---|
| Python email parsing library | Complete | `backend/src/email_analysis/parser.py` uses Python `email.message_from_string` with `policy.default` |
| BeautifulSoup | Complete | `backend/src/email_analysis/parser.py` uses `BeautifulSoup` to extract HTML anchor links |
| Regular expressions | Complete | `backend/src/email_analysis/parser.py`, `backend/src/email_analysis/url_checker.py`, and `backend/src/pattern_engine/risk_scorer.py` use regex-based matching |

## Assessment Testing Evidence

The automated tests cover authentication protection, 2FA token validation, URL checks, attachment checks, header checks, parser behavior, risk scoring, report export access control, and ML dataset validation.

Run the test suite from the backend folder:

```powershell
cd C:\Users\Lenovo\Desktop\SecurityProject\CyberMailGuard\backend
.\venv\Scripts\python.exe -m pytest
```

Expected result: all tests pass.
