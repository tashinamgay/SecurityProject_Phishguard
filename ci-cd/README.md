# CyberMailGuard CI/CD

The executable GitHub Actions workflow is stored in:

```text
.github/workflows/security.yml
```

This folder is included to match the ICT932 Assessment 3 repository structure requirement for `/ci-cd` pipeline documentation. The workflow runs Build, Bandit SAST, pip-audit dependency scanning, pytest, OWASP ZAP DAST, and a deployment gate.
