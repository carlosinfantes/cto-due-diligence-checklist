# Automation Scripts

> **Practical tools** to automate common due diligence tasks.

## 🎯 Overview

These scripts help automate the technical assessment process. All scripts are designed to be run from the **target repository root**, not from this checklist repository.

## 📁 Script Organization

```
scripts/
├── general/           # Language-agnostic tools
│   ├── security-scan.sh
│   ├── code-quality-scan.sh
│   ├── dependency-graph.sh
│   └── generate-architecture.py
├── python/           # Python-specific tools
│   └── run-quality-checks.py
├── javascript/       # JavaScript/Node.js tools
│   └── run-quality-checks.sh
└── README.md         # This file
```

## 🚀 Quick Start

### 1. Basic Usage Pattern

```bash
# Navigate to the target repository
cd /path/to/target-repository

# Run scripts from the target repo root
../cto-due-diligence-checklist/scripts/general/security-scan.sh
../cto-due-diligence-checklist/scripts/python/run-quality-checks.py
```

### 2. Make Scripts Executable

```bash
# Make all scripts executable
find scripts/ -name "*.sh" -exec chmod +x {} \;
find scripts/ -name "*.py" -exec chmod +x {} \;
```

## 🛠️ Available Scripts

### General Scripts (Language Agnostic)

#### `security-scan.sh`
**Purpose:** Comprehensive security scanning for any repository.

**What it does:**
- Scans for hardcoded secrets with truffleHog
- Checks dependency vulnerabilities (Python & Node.js)
- Runs static security analysis
- Validates Docker configurations
- Generates security report

**Usage:**
```bash
../cto-due-diligence-checklist/scripts/general/security-scan.sh
```

**Output:** `security-reports/` directory with detailed findings

**Requirements:**
- Git repository
- Optional: truffleHog, pip-audit, safety, bandit

---

#### `code-quality-scan.sh`
**Purpose:** General code quality assessment.

**What it does:**
- Counts lines of code by language
- Identifies TODO/FIXME comments
- Checks for common code smells
- Analyzes repository structure

**Usage:**
```bash
../cto-due-diligence-checklist/scripts/general/code-quality-scan.sh
```

**Output:** `quality-reports/general-analysis.txt`

---

### Python Scripts

#### `run-quality-checks.py`
**Purpose:** Comprehensive Python code quality assessment.

**What it does:**
- Runs Flake8 linting
- Checks Black formatting
- Validates import sorting (isort)
- Performs type checking (mypy)
- Measures test coverage
- Analyzes code complexity (radon)

**Usage:**
```bash
../cto-due-diligence-checklist/scripts/python/run-quality-checks.py
```

**Output:** `quality-reports/` with detailed analysis

**Requirements:**
- Python project with .py files
- Optional tools: flake8, black, isort, mypy, pytest, pytest-cov, radon

**Installation:**
```bash
pip install flake8 black isort mypy pytest pytest-cov radon
```

---

### JavaScript Scripts

#### `run-quality-checks.sh`
**Purpose:** JavaScript/Node.js code quality assessment.

**What it does:**
- Runs ESLint for code quality
- Checks Prettier formatting
- Validates TypeScript (if applicable)
- Measures test coverage
- Analyzes dependencies

**Usage:**
```bash
../cto-due-diligence-checklist/scripts/javascript/run-quality-checks.sh
```

**Output:** `quality-reports/` with detailed analysis

**Requirements:**
- Node.js project with package.json
- Optional tools: eslint, prettier, typescript, jest/mocha

**Installation:**
```bash
npm install eslint prettier typescript jest
```

## 📊 Understanding Script Output

### Exit Codes
- `0`: Success (good quality/security)
- `1`: Issues found (review needed)

### Report Directories
All scripts create report directories in the target repository:

- `security-reports/`: Security scan results
- `quality-reports/`: Code quality analysis
- `architecture-reports/`: Architecture analysis

### Report Formats
- **JSON**: Machine-readable data for further processing
- **TXT**: Human-readable summaries
- **HTML**: Coverage reports and detailed analysis

## 🔧 Customization

### Environment Variables

```bash
# Skip certain checks
export SKIP_SECURITY_SCAN=true
export SKIP_DEPENDENCY_CHECK=true

# Custom tool paths
export FLAKE8_CONFIG=.flake8
export ESLINT_CONFIG=.eslintrc.js
```

### Configuration Files

Scripts respect standard configuration files:
- `.flake8`, `pyproject.toml` for Python tools
- `.eslintrc.js`, `.prettierrc` for JavaScript tools
- Custom configs in project root

## 🚨 Troubleshooting

### Common Issues

**"Command not found" errors:**
```bash
# Install missing tools
pip install flake8 black isort mypy pytest pytest-cov radon bandit safety pip-audit
npm install eslint prettier typescript jest
```

**Permission denied:**
```bash
# Make scripts executable
chmod +x scripts/general/security-scan.sh
chmod +x scripts/python/run-quality-checks.py
```

**"Not in a git repository":**
```bash
# Ensure you're in the target repository root
cd /path/to/target-repository
git status  # Should show git info
```

### Tool Installation

**Python tools:**
```bash
# Essential tools
pip install flake8 black isort mypy pytest pytest-cov

# Security tools
pip install bandit safety pip-audit truffleHog

# Analysis tools
pip install radon
```

**JavaScript tools:**
```bash
# Essential tools
npm install eslint prettier typescript

# Testing tools
npm install jest @types/jest

# Security tools
npm install eslint-plugin-security
```

**System tools:**
```bash
# Ubuntu/Debian
sudo apt-get install git cloc

# macOS
brew install git cloc
```

## 📈 Interpreting Results

### Quality Scores
- **80-100**: Excellent - Ready for production
- **60-79**: Good - Minor improvements needed
- **40-59**: Needs Improvement - Significant work required
- **0-39**: Poor - Major refactoring needed

### Security Risk Levels
- **🟢 Good**: No critical issues found
- **🟡 Moderate**: Some issues, manageable risk
- **🟠 Concerning**: Multiple issues, needs attention
- **🔴 High Risk**: Critical issues, immediate action required

### Priority Guidelines
1. **Critical Security Issues**: Fix immediately
2. **High Complexity Code**: Refactor for maintainability
3. **Low Test Coverage**: Add tests for critical paths
4. **Outdated Dependencies**: Update with caution
5. **Code Style Issues**: Fix for consistency

## 🔄 Integration with CI/CD

### GitHub Actions Example
```yaml
name: Due Diligence Check
on: [push, pull_request]
jobs:
  quality-check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run Quality Checks
        run: |
          git clone https://github.com/username/cto-due-diligence-checklist.git
          ./cto-due-diligence-checklist/scripts/python/run-quality-checks.py
```

### Pre-commit Hooks
```yaml
# .pre-commit-config.yaml
repos:
  - repo: local
    hooks:
      - id: quality-check
        name: Quality Check
        entry: ../cto-due-diligence-checklist/scripts/python/run-quality-checks.py
        language: system
        pass_filenames: false
```

## 🤝 Contributing

### Adding New Scripts
1. Follow the existing naming convention
2. Include comprehensive error handling
3. Generate both human and machine-readable output
4. Add documentation to this README
5. Test on multiple repositories

### Script Requirements
- **Portable**: Work on Linux, macOS, Windows (WSL)
- **Graceful**: Handle missing tools gracefully
- **Informative**: Provide clear output and next steps
- **Safe**: Don't modify the target repository
- **Fast**: Complete in reasonable time (<5 minutes)

---

**Need help?** Check the main [README](../README.md) or open an issue.
