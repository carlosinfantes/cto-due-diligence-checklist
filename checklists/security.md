# Security Checklist

> **Focus:** Vulnerability assessment, secret management, and security practices.

## 🔐 Secret Management

### Secret Scanning
- [ ] Scan for hardcoded secrets: `trufflehog git .`
- [ ] Check for API keys in code: `grep -r "api_key\|API_KEY" --include="*.py" --include="*.js" .`
- [ ] Look for database credentials: `grep -r "password\|PASSWORD" --include="*.py" --include="*.js" .`
- [ ] Search for private keys: `find . -name "*.pem" -o -name "*.key"`

```bash
# Install and run truffleHog
pip install truffleHog
trufflehog git . --json > secrets-scan.json

# Alternative: git-secrets
git secrets --scan
```

> ⚠️ **Critical:** Any hardcoded secrets are an immediate red flag requiring rotation.

### Environment Configuration
- [ ] Environment variables used for secrets
- [ ] `.env` files in `.gitignore`
- [ ] No `.env` files committed to repository
- [ ] Secret management service integration (AWS Secrets Manager, HashiCorp Vault, etc.)

```bash
# Check for committed .env files
git log --all --full-history -- .env
git log --all --full-history -- "*.env"
```

## 🛡️ Dependency Vulnerabilities

### Python Dependencies
- [ ] Run pip-audit: `pip-audit`
- [ ] Check Safety database: `safety check`
- [ ] Review requirements.txt/pyproject.toml for pinned versions

```bash
# Install and run security tools
pip install pip-audit safety
pip-audit --format=json --output=vulnerabilities.json
safety check --json > safety-report.json
```

### Node.js Dependencies
- [ ] Run npm audit: `npm audit`
- [ ] Check with Snyk: `npx snyk test`
- [ ] Review package.json for version pinning

```bash
# Run security audits
npm audit --json > npm-audit.json
npx snyk test --json > snyk-report.json
```

### Dependency Analysis
- [ ] Count total vulnerabilities by severity
- [ ] Identify outdated packages with known issues
- [ ] Check for abandoned/unmaintained dependencies
- [ ] Review transitive dependency risks

## 🔍 Code Security Analysis

### Static Application Security Testing (SAST)
- [ ] Run Bandit (Python): `bandit -r .`
- [ ] Run ESLint security plugin (JavaScript): `npx eslint --ext .js,.ts .`
- [ ] Check for SQL injection patterns
- [ ] Look for XSS vulnerabilities

```bash
# Python security scanning
pip install bandit
bandit -r . -f json -o bandit-report.json

# JavaScript security scanning
npm install eslint-plugin-security
npx eslint --ext .js,.ts . --format json > eslint-security.json
```

### Common Vulnerability Patterns
- [ ] SQL injection risks: `grep -r "execute\|query" --include="*.py" --include="*.js" .`
- [ ] Command injection: `grep -r "subprocess\|exec\|eval" --include="*.py" --include="*.js" .`
- [ ] Path traversal: `grep -r "\.\./" --include="*.py" --include="*.js" .`
- [ ] Unsafe deserialization: `grep -r "pickle\|eval\|exec" --include="*.py" .`

## 🌐 Web Application Security

### Input Validation
- [ ] User input validation implemented
- [ ] SQL parameterization used
- [ ] XSS protection in place
- [ ] CSRF protection enabled
- [ ] File upload restrictions

### Authentication & Authorization
- [ ] Strong password policies
- [ ] Multi-factor authentication support
- [ ] Session management security
- [ ] Role-based access control
- [ ] JWT token security (if used)

```bash
# Check for authentication patterns
grep -r "password\|auth\|login" --include="*.py" --include="*.js" . | head -20
```

## 🏗️ Infrastructure Security

### Configuration Files
- [ ] Review Docker configurations
- [ ] Check Kubernetes manifests
- [ ] Examine CI/CD pipeline security
- [ ] Infrastructure as Code security

```bash
# Check Docker security
docker run --rm -v $(pwd):/app clair-scanner:latest /app/Dockerfile

# Kubernetes security scanning
kubectl apply --dry-run=client -f k8s/ 2>&1 | grep -i security
```

### Network Security
- [ ] HTTPS enforcement
- [ ] Security headers implementation
- [ ] API rate limiting
- [ ] Network segmentation
- [ ] Firewall configurations

## 📊 Security Metrics

### Vulnerability Scoring

| Category | Critical | High | Medium | Low | Score (1-10) |
|----------|----------|------|--------|-----|--------------|
| Dependencies | ___ | ___ | ___ | ___ | ___ |
| Code Issues | ___ | ___ | ___ | ___ | ___ |
| Config Issues | ___ | ___ | ___ | ___ | ___ |
| **Total** | **___** | **___** | **___** | **___** | **___** |

### Security Checklist Score
- [ ] **No hardcoded secrets** (Critical)
- [ ] **No critical vulnerabilities** in dependencies
- [ ] **Input validation** implemented
- [ ] **Authentication** properly configured
- [ ] **HTTPS** enforced
- [ ] **Security headers** implemented
- [ ] **Regular security updates** process

## 🚨 Critical Security Issues

### Immediate Action Required
- [ ] **Exposed secrets** in code history
- [ ] **Critical CVE vulnerabilities** in production dependencies
- [ ] **No authentication** on sensitive endpoints
- [ ] **SQL injection** vulnerabilities
- [ ] **Remote code execution** risks

### High Priority Issues
- [ ] **Outdated dependencies** with known vulnerabilities
- [ ] **Weak authentication** mechanisms
- [ ] **Missing input validation**
- [ ] **Insecure configurations**
- [ ] **No security monitoring**

## 🔧 Security Tools Integration

### Automated Security Scanning
- [ ] Dependabot/Renovate for dependency updates
- [ ] GitHub Security Advisories enabled
- [ ] SAST tools in CI pipeline
- [ ] Container image scanning
- [ ] Infrastructure scanning

```yaml
# Example GitHub Action for security
name: Security Scan
on: [push, pull_request]
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run Trivy vulnerability scanner
        uses: aquasecurity/trivy-action@master
        with:
          scan-type: 'fs'
          format: 'sarif'
          output: 'trivy-results.sarif'
```

## 📋 Compliance Considerations

### Regulatory Requirements
- [ ] GDPR compliance (if applicable)
- [ ] SOC 2 requirements
- [ ] PCI DSS (if handling payments)
- [ ] HIPAA (if handling health data)
- [ ] Industry-specific regulations

### Data Protection
- [ ] Data encryption at rest
- [ ] Data encryption in transit
- [ ] Personal data handling
- [ ] Data retention policies
- [ ] Backup security

## 🛠️ Automation Script

Run our automated security scan:

```bash
# From the target repository root
../cto-due-diligence-checklist/scripts/general/security-scan.sh
```

## 📝 Security Findings Template

```markdown
## Security Assessment

**Overall Security Score:** ___/10
**Critical Issues Found:** ___
**High Priority Issues:** ___

### Critical Findings
- [List any critical security issues]

### High Priority Findings
- [List high priority issues]

### Recommendations
1. **Immediate Actions:**
   - [Critical fixes needed]

2. **Short Term (1-4 weeks):**
   - [High priority improvements]

3. **Long Term (1-3 months):**
   - [Security enhancements]

### Compliance Notes
- [Any compliance-related observations]
```

## 🚩 Security Red Flags

- [ ] **Hardcoded secrets** in repository
- [ ] **No dependency updates** in >6 months
- [ ] **Critical vulnerabilities** ignored
- [ ] **No authentication** on APIs
- [ ] **Plain text passwords** stored
- [ ] **No security testing** in CI

## 🟢 Security Green Flags

- [ ] **Automated security scanning** in place
- [ ] **Regular dependency updates**
- [ ] **No secrets in code**
- [ ] **Strong authentication** implemented
- [ ] **Security headers** configured
- [ ] **Vulnerability management** process

## ⏭️ Next Steps

After completing security review:
1. **DevOps Assessment**: [`devops.md`](./devops.md)
2. **Documentation Review**: [`documentation.md`](./documentation.md)
3. **Architecture Analysis**: [`architecture.md`](./architecture.md)
