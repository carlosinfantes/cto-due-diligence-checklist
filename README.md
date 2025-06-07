# CTO's Guide: Tech Due Diligence Checklist

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Last Updated](https://img.shields.io/github/last-commit/username/cto-due-diligence-checklist)](https://github.com/username/cto-due-diligence-checklist)

> **Practical. No jargon. Action-oriented.**

A hands-on guide from CTO to CTO for conducting thorough technical due diligence. This repo provides checklists, automation scripts, and real examples to help you evaluate any codebase systematically.

## 🎯 Philosophy

- **Open Source First**: Every tool and script uses open-source solutions
- **Reproducible**: Every step can be repeated on any codebase
- **Opinionated but Flexible**: We provide defaults, but you can swap tools
- **Transparency**: Clear distinction between automated checks and human review

## 🚀 Quick Start

1. **Clone this repo**: `git clone https://github.com/username/cto-due-diligence-checklist.git`
2. **Start with the general checklist**: [`/checklists/general.md`](./checklists/general.md)
3. **Run automated scripts**: Check [`/scripts/`](./scripts/) for your tech stack
4. **Generate reports**: Use templates in [`/templates/`](./templates/)

## 📁 Repository Structure

```
├── README.md                 # You are here
├── checklists/              # Markdown checklists by area
│   ├── general.md           # Pre-flight checklist
│   ├── code-quality.md      # Linting, coverage, dependencies
│   ├── architecture.md      # System design evaluation
│   ├── security.md          # Vulnerability and secret scans
│   ├── devops.md           # CI/CD and deployment review
│   └── documentation.md     # Process and knowledge review
├── scripts/                 # Automation scripts
│   ├── python/             # Python-specific tools
│   ├── javascript/         # JS/Node.js tools
│   ├── general/            # Language-agnostic scripts
│   └── README.md           # Script usage guide
├── diagrams/               # Architecture diagram examples
│   ├── mermaid/            # Mermaid diagram code
│   ├── python-diagrams/    # Python Diagrams code
│   └── README.md           # Diagram generation guide
├── examples/               # Sample outputs and reports
│   ├── reports/            # Example due diligence reports
│   └── outputs/            # Tool output examples
├── docs/                   # Extended guides
│   ├── red-flags.md        # Warning signs to watch for
│   ├── green-flags.md      # Positive indicators
│   └── tool-comparison.md  # Tool alternatives and comparisons
└── templates/              # Issue and PR templates
    ├── due-diligence-issue.md
    └── findings-report.md
```

## 🎯 Core Checklists

| Area | Checklist | Key Tools |
|------|-----------|-----------|
| **General** | [general.md](./checklists/general.md) | Access, team intro, documentation |
| **Code Quality** | [code-quality.md](./checklists/code-quality.md) | Flake8, ESLint, SonarQube |
| **Architecture** | [architecture.md](./checklists/architecture.md) | Diagrams, Mermaid |
| **Security** | [security.md](./checklists/security.md) | truffleHog, Snyk, Dependabot |
| **DevOps** | [devops.md](./checklists/devops.md) | GitHub Actions, pipeline review |
| **Documentation** | [documentation.md](./checklists/documentation.md) | Runbooks, onboarding, diagrams |

## 🛠️ Automation Scripts

All scripts are designed to be run from the target repository root:

```bash
# Python projects
./scripts/python/run-quality-checks.py

# JavaScript projects  
./scripts/javascript/run-quality-checks.sh

# Security scans (any project)
./scripts/general/security-scan.sh
```

## 📊 Example Usage

```bash
# 1. Clone target repository
git clone https://github.com/target-org/target-repo.git
cd target-repo

# 2. Run automated checks
../cto-due-diligence-checklist/scripts/python/run-quality-checks.py

# 3. Generate architecture diagram
../cto-due-diligence-checklist/scripts/general/generate-architecture.py

# 4. Create findings report
cp ../cto-due-diligence-checklist/templates/findings-report.md ./due-diligence-findings.md
```

## 🚩 Quick Reference

### Red Flags 🔴
- No tests or <50% coverage
- Dependencies >2 years old
- Hardcoded secrets in code
- No CI/CD pipeline
- Single points of failure

### Green Flags 🟢
- >80% test coverage
- Automated dependency updates
- Infrastructure as code
- Clear documentation
- Monitoring and alerting

## 🤝 Contributing

Found a useful tool or checklist item? PRs welcome! Please:

1. Keep the "practical, no jargon" tone
2. Test scripts on real repositories
3. Update relevant documentation

## 📄 License

MIT License - feel free to adapt for your organization's needs.

---

**Made by CTOs, for CTOs.** No consultant speak, just practical tools that work.
