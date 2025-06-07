# Code Quality Checklist

> **Focus:** Code maintainability, testing, and technical debt assessment.

## 🧹 Code Standards & Linting

### Python Projects
- [ ] Run Flake8: `flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics`
- [ ] Check with Black: `black --check .`
- [ ] Run isort: `isort --check-only .`
- [ ] Type checking with mypy: `mypy .`

```bash
# Install tools
pip install flake8 black isort mypy

# Run all checks
flake8 . && black --check . && isort --check-only . && mypy .
```

> 💡 **Pro tip:** Look for `.flake8`, `pyproject.toml`, or `setup.cfg` for existing configuration.

### JavaScript/Node.js Projects
- [ ] Run ESLint: `npx eslint .`
- [ ] Check Prettier: `npx prettier --check .`
- [ ] TypeScript check: `npx tsc --noEmit`

```bash
# Install and run
npm install eslint prettier typescript
npx eslint . && npx prettier --check . && npx tsc --noEmit
```

### General Code Quality
- [ ] Check for TODO/FIXME comments: `grep -r "TODO\|FIXME" --include="*.py" --include="*.js" .`
- [ ] Look for code duplication
- [ ] Review function/class complexity
- [ ] Check for magic numbers and hardcoded values

## 🧪 Testing

### Test Coverage
- [ ] Run test suite: `pytest` or `npm test`
- [ ] Generate coverage report: `pytest --cov=.` or `npm run test:coverage`
- [ ] Check coverage percentage (aim for >80%)
- [ ] Review uncovered critical paths

```bash
# Python coverage
pip install pytest pytest-cov
pytest --cov=. --cov-report=html

# JavaScript coverage  
npm test -- --coverage
```

### Test Quality Assessment
- [ ] Unit tests exist for core business logic
- [ ] Integration tests cover critical workflows
- [ ] Tests are readable and maintainable
- [ ] Test data is properly managed
- [ ] Flaky tests identified and documented

> ⚠️ **Red flag:** High coverage with poor test quality is worse than honest low coverage.

### Test Organization
- [ ] Tests are organized logically
- [ ] Test naming conventions are consistent
- [ ] Setup/teardown is handled properly
- [ ] Mock usage is appropriate

## 📦 Dependencies

### Dependency Analysis
- [ ] List all dependencies: `pip list` or `npm list`
- [ ] Check for outdated packages: `pip list --outdated` or `npm outdated`
- [ ] Review dependency licenses
- [ ] Identify unused dependencies

```bash
# Python dependency check
pip install pip-audit
pip-audit

# Node.js dependency check
npm audit
npx depcheck  # Find unused dependencies
```

### Dependency Security
- [ ] Run security audit: `pip-audit` or `npm audit`
- [ ] Check for known vulnerabilities
- [ ] Review dependency update frequency
- [ ] Assess dependency maintenance status

> 🔍 **Common pitfall:** Don't just count vulnerabilities—assess their actual impact on your use case.

## 📊 Code Metrics

### Complexity Analysis
- [ ] Cyclomatic complexity check
- [ ] Function length analysis
- [ ] Class size review
- [ ] Inheritance depth assessment

```bash
# Python complexity
pip install radon
radon cc . -a  # Cyclomatic complexity
radon mi .     # Maintainability index

# JavaScript complexity
npx complexity-report --format json src/
```

### Code Statistics
- [ ] Lines of code count
- [ ] Comment ratio
- [ ] File size distribution
- [ ] Language breakdown

```bash
# Use cloc for comprehensive stats
cloc .
```

## 🔧 Static Analysis

### Advanced Analysis Tools
- [ ] SonarQube scan (if available)
- [ ] CodeClimate analysis
- [ ] Language-specific analyzers

```bash
# SonarQube scanner
sonar-scanner \
  -Dsonar.projectKey=my-project \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000
```

### Code Smells Detection
- [ ] Long parameter lists
- [ ] Large classes/functions
- [ ] Duplicate code blocks
- [ ] Inappropriate intimacy between classes
- [ ] Dead code identification

## 📋 Quality Gates

### Minimum Standards Checklist
- [ ] **Linting**: No critical linting errors
- [ ] **Tests**: >70% code coverage (>80% preferred)
- [ ] **Dependencies**: No high-severity vulnerabilities
- [ ] **Complexity**: No functions with complexity >10
- [ ] **Documentation**: Public APIs documented

### Quality Scoring

| Metric | Weight | Score (1-10) | Weighted Score |
|--------|--------|--------------|----------------|
| Test Coverage | 25% | ___ | ___ |
| Linting Clean | 20% | ___ | ___ |
| Dependency Health | 20% | ___ | ___ |
| Code Complexity | 15% | ___ | ___ |
| Documentation | 10% | ___ | ___ |
| Security | 10% | ___ | ___ |
| **Total** | **100%** | | **___** |

## 🚩 Red Flags

- [ ] **No tests** or <30% coverage
- [ ] **Hundreds of linting errors** ignored
- [ ] **Dependencies >2 years old** without updates
- [ ] **No code review process** evident
- [ ] **Commented-out code** everywhere
- [ ] **No consistent coding standards**

## 🟢 Green Flags

- [ ] **>80% test coverage** with quality tests
- [ ] **Clean linting** with consistent standards
- [ ] **Regular dependency updates**
- [ ] **Code review evidence** in commit history
- [ ] **Clear coding conventions** followed
- [ ] **Automated quality checks** in CI

## 🛠️ Automation Script

Run our automated code quality script:

```bash
# From the target repository root
../cto-due-diligence-checklist/scripts/general/code-quality-scan.sh
```

## 📝 Findings Template

```markdown
## Code Quality Assessment

**Overall Score:** ___/10

### Strengths
- [List positive findings]

### Areas for Improvement  
- [List issues found]

### Critical Issues
- [List any blocking issues]

### Recommendations
- [Specific actionable items]
```

## ⏭️ Next Steps

After completing code quality review:
1. **Architecture Review**: [`architecture.md`](./architecture.md)
2. **Security Assessment**: [`security.md`](./security.md)
3. **DevOps Evaluation**: [`devops.md`](./devops.md)
