# Red Flags: Warning Signs to Watch For

> **Critical indicators** that suggest significant technical risk or poor engineering practices.

## 🚨 Critical Red Flags (Deal Breakers)

### Security
- [ ] **Hardcoded secrets** in repository history
- [ ] **No authentication** on production APIs
- [ ] **SQL injection vulnerabilities** in production code
- [ ] **Admin credentials** shared or default
- [ ] **Production data** in development environments

### Code Quality
- [ ] **No version control** or irregular commits
- [ ] **No tests** whatsoever
- [ ] **Single developer** with all knowledge
- [ ] **No code reviews** evident in history
- [ ] **Production hotfixes** bypassing all processes

### Operations
- [ ] **No backups** or untested backup procedures
- [ ] **Manual deployments** to production
- [ ] **No monitoring** or alerting
- [ ] **Shared production access** without audit trails
- [ ] **No incident response** procedures

## 🔴 High-Risk Red Flags

### Architecture & Scalability
- [ ] **Single points of failure** throughout system
- [ ] **No horizontal scaling** capability
- [ ] **Monolithic database** with no partitioning strategy
- [ ] **Synchronous processing** for all operations
- [ ] **No caching strategy** implemented

### Development Practices
- [ ] **<30% test coverage** on critical business logic
- [ ] **No CI/CD pipeline** or automated testing
- [ ] **Dependencies >2 years old** without updates
- [ ] **No coding standards** or style guides
- [ ] **Commented-out code** throughout codebase

### Team & Process
- [ ] **High turnover** in engineering team
- [ ] **No documentation** for critical systems
- [ ] **No onboarding process** for new developers
- [ ] **No change management** process
- [ ] **Blame culture** evident in communications

### Infrastructure
- [ ] **No infrastructure as code**
- [ ] **Manual server management**
- [ ] **No environment separation** (dev/staging/prod)
- [ ] **No disaster recovery** plan
- [ ] **Vendor lock-in** without alternatives

## 🟠 Medium-Risk Red Flags

### Code Organization
- [ ] **God objects** or classes >1000 lines
- [ ] **Circular dependencies** between modules
- [ ] **Magic numbers** and hardcoded values everywhere
- [ ] **Inconsistent naming** conventions
- [ ] **Dead code** not removed

### Performance
- [ ] **N+1 query problems** in database access
- [ ] **No performance testing** or benchmarks
- [ ] **Memory leaks** in long-running processes
- [ ] **Blocking operations** on main threads
- [ ] **No query optimization** or indexing strategy

### Security Practices
- [ ] **Outdated frameworks** with known vulnerabilities
- [ ] **No input validation** on user data
- [ ] **Weak password policies**
- [ ] **No security headers** implemented
- [ ] **Logs containing** sensitive information

### Operational Issues
- [ ] **Long deployment times** (>30 minutes)
- [ ] **Frequent rollbacks** due to issues
- [ ] **No capacity planning**
- [ ] **Alert fatigue** from too many false positives
- [ ] **No performance monitoring**

## 🟡 Warning Signs (Proceed with Caution)

### Technical Debt
- [ ] **TODO comments** older than 6 months
- [ ] **Workarounds** instead of proper fixes
- [ ] **Copy-paste code** duplication
- [ ] **Outdated documentation**
- [ ] **Technical debt** not tracked or prioritized

### Development Velocity
- [ ] **Slow feature delivery** compared to team size
- [ ] **Bug fix rate** higher than feature delivery
- [ ] **Long code review** cycles
- [ ] **Frequent context switching** between projects
- [ ] **Estimation accuracy** consistently poor

### Communication
- [ ] **Unclear requirements** or changing scope
- [ ] **Poor stakeholder** communication
- [ ] **Technical decisions** not documented
- [ ] **Knowledge silos** within team
- [ ] **Resistance to change** from team

## 🔍 How to Investigate Red Flags

### Code Analysis
```bash
# Check for hardcoded secrets
grep -r "password\|api_key\|secret" --include="*.py" --include="*.js" .

# Find large files (potential god objects)
find . -name "*.py" -o -name "*.js" | xargs wc -l | sort -n | tail -10

# Check for TODO/FIXME comments
grep -r "TODO\|FIXME" --include="*.py" --include="*.js" . | wc -l
```

### Git History Analysis
```bash
# Check commit frequency
git log --since="6 months ago" --oneline | wc -l

# Find contributors
git shortlog -sn | head -10

# Check for large commits (potential code dumps)
git log --oneline --stat | grep -E "files? changed" | sort -n | tail -10
```

### Dependency Analysis
```bash
# Python: Check for outdated packages
pip list --outdated

# Node.js: Check for vulnerabilities
npm audit

# Check for unused dependencies
# Python: pip-check
# Node.js: depcheck
```

## 📊 Red Flag Scoring System

### Critical (10 points each)
- Hardcoded secrets in production
- No authentication on APIs
- No backups or disaster recovery
- Single person dependency
- No version control

### High Risk (5 points each)
- <30% test coverage
- No CI/CD pipeline
- Dependencies >2 years old
- No monitoring/alerting
- Manual deployments

### Medium Risk (3 points each)
- Poor code organization
- Performance issues
- Security vulnerabilities
- Operational inefficiencies

### Warning Signs (1 point each)
- Technical debt accumulation
- Communication issues
- Process inefficiencies

### Risk Assessment
- **0-5 points**: Low risk, proceed
- **6-15 points**: Medium risk, address issues
- **16-30 points**: High risk, significant work needed
- **30+ points**: Critical risk, consider walking away

## 🛠️ Red Flag Mitigation Strategies

### Immediate Actions
1. **Document all findings** with evidence
2. **Estimate remediation effort** and cost
3. **Prioritize by business impact**
4. **Create improvement roadmap**
5. **Set clear success metrics**

### Negotiation Points
- **Escrow funds** for critical fixes
- **Extended due diligence** period
- **Price adjustments** based on technical debt
- **Retention of key personnel**
- **Investment in infrastructure**

### Post-Acquisition Planning
- **Technical debt reduction** sprints
- **Security audit** and remediation
- **Process improvement** initiatives
- **Team training** and development
- **Infrastructure modernization**

## 📋 Red Flag Checklist Template

```markdown
## Red Flag Assessment

**Project:** [Name]
**Date:** [Date]
**Reviewer:** [Name]

### Critical Red Flags (10 points each)
- [ ] Hardcoded secrets: ___
- [ ] No authentication: ___
- [ ] No backups: ___
- [ ] Single person dependency: ___
- [ ] No version control: ___

### High Risk (5 points each)
- [ ] Low test coverage: ___
- [ ] No CI/CD: ___
- [ ] Outdated dependencies: ___
- [ ] No monitoring: ___
- [ ] Manual deployments: ___

### Medium Risk (3 points each)
- [ ] Poor code organization: ___
- [ ] Performance issues: ___
- [ ] Security vulnerabilities: ___
- [ ] Operational issues: ___

### Warning Signs (1 point each)
- [ ] Technical debt: ___
- [ ] Communication issues: ___
- [ ] Process problems: ___

**Total Score:** ___
**Risk Level:** [Low/Medium/High/Critical]

### Top 3 Concerns
1. [Most critical issue]
2. [Second most critical]
3. [Third most critical]

### Recommended Actions
- **Immediate:** [Must fix before proceeding]
- **Short-term:** [Fix within 90 days]
- **Long-term:** [Address within 12 months]
```

## 🎯 Remember

> **Red flags are not necessarily deal breakers** - they're indicators that require deeper investigation and potentially significant investment to address.

> **Context matters** - A startup's technical debt tolerance is different from an enterprise acquisition.

> **Document everything** - Red flags need evidence and clear remediation plans.

> **Quantify impact** - Translate technical issues into business risk and cost.
