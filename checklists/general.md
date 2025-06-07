# General Due Diligence Checklist

> **Start here.** Get your bearings before diving into technical details.

## 📋 Pre-Flight Setup

### Access & Permissions
- [ ] Repository access granted (read permissions minimum)
- [ ] CI/CD pipeline access (view builds, logs)
- [ ] Documentation access (wikis, Confluence, Notion, etc.)
- [ ] Architecture diagrams and technical documentation
- [ ] Issue tracker access (Jira, GitHub Issues, etc.)

> 💡 **Pro tip:** Request read-only access first. You can always ask for more later.

### Team Introductions
- [ ] Meet with lead developer/architect (30-60 min)
- [ ] Meet with DevOps/SRE lead (30 min)
- [ ] Meet with product/project manager (30 min)
- [ ] Get contact info for domain experts

> ⚠️ **Gotcha:** Don't skip the human element. Code tells you what, people tell you why.

## 📊 Initial Assessment

### Repository Overview
- [ ] Clone main repository: `git clone <repo-url>`
- [ ] Check repository size: `du -sh .git`
- [ ] Review commit history: `git log --oneline --graph -20`
- [ ] Identify main branches: `git branch -a`
- [ ] Check recent activity: `git log --since="1 month ago" --oneline | wc -l`

```bash
# Quick repo stats
echo "Repository size:" && du -sh .git
echo "Total commits:" && git rev-list --all --count
echo "Contributors:" && git shortlog -sn | wc -l
echo "Last commit:" && git log -1 --format="%cr"
```

### Technology Stack Identification
- [ ] Programming languages (check file extensions)
- [ ] Frameworks and major dependencies
- [ ] Database technologies
- [ ] Infrastructure and deployment tools
- [ ] Third-party services and APIs

```bash
# Language breakdown
find . -type f -name "*.py" | wc -l  # Python files
find . -type f -name "*.js" | wc -l  # JavaScript files
find . -type f -name "*.java" | wc -l # Java files
# Add more as needed
```

### Documentation Quick Scan
- [ ] README.md exists and is comprehensive
- [ ] API documentation exists
- [ ] Setup/installation instructions are clear
- [ ] Architecture documentation is available
- [ ] Runbooks for operations exist

> 🔍 **Common pitfall:** Don't assume good code means good documentation. Check both.

## 🎯 Scope Definition

### What to Focus On
- [ ] Define business-critical components
- [ ] Identify high-risk areas (security, performance, scalability)
- [ ] Determine compliance requirements
- [ ] Set timeline and depth of review

### Resource Planning
- [ ] Estimate time needed for each area
- [ ] Identify areas requiring specialist knowledge
- [ ] Plan for follow-up questions and clarifications
- [ ] Set up regular check-ins with stakeholders

## 📝 Initial Findings Template

Create a findings document to track discoveries:

```markdown
# Due Diligence Findings - [Project Name]

**Date:** [Date]
**Reviewer:** [Your Name]
**Scope:** [What you're reviewing]

## Executive Summary
- Overall assessment: [Green/Yellow/Red]
- Key strengths: [List]
- Major concerns: [List]
- Recommended next steps: [List]

## Detailed Findings
[Use this template for each area you review]
```

## ⏭️ Next Steps

Once you've completed this general checklist:

1. **Code Quality**: Start with [`code-quality.md`](./code-quality.md)
2. **Architecture**: Review [`architecture.md`](./architecture.md)
3. **Security**: Check [`security.md`](./security.md)
4. **DevOps**: Evaluate [`devops.md`](./devops.md)
5. **Documentation**: Assess [`documentation.md`](./documentation.md)

> 📊 **Recommended tool:** Use a simple spreadsheet or markdown table to track completion status across all checklists.
