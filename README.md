# SecureByte CLI

> Open-source command-line tool for cloud security scanning and compliance checks

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![SecureByte](https://img.shields.io/badge/SecureByte-Organization-181717?style=flat&logo=github&logoColor=white)](https://github.com/securebyte-consulting)
[![Status](https://img.shields.io/badge/Status-Planning-yellow.svg)]()

## 🎯 Purpose

SecureByte CLI is an open-source command-line tool that brings compliance automation to your terminal and CI/CD pipelines. Scan your cloud infrastructure, run security checks locally, and integrate compliance gates into your development workflow - all without needing the full SecureByte platform.

## ✨ Planned Features

### Infrastructure Scanning (Q4 2026)
```bash
# Scan AWS infrastructure for security misconfigurations
securebyte scan aws --profile production

# Scan specific resource types
securebyte scan aws --resources s3,ec2,rds

# Output results in different formats
securebyte scan aws --format json --output report.json
```

### Local Compliance Checks (Q4 2026)
```bash
# Check compliance against specific frameworks
securebyte check --framework popia
securebyte check --framework soc2
securebyte check --framework iso27001

# Run custom compliance rules
securebyte check --rules ./custom-rules.yaml
```

### CI/CD Integration (Q4 2026)
```bash
# Fail builds if critical issues are found
securebyte scan aws --fail-on critical

# Generate compliance reports for pull requests
securebyte report --format markdown >> $GITHUB_STEP_SUMMARY

# Compare compliance status between branches
securebyte diff main feature-branch
```

### Continuous Monitoring (Q4 2026)
```bash
# Watch for infrastructure changes
securebyte watch --interval 5m

# Monitor specific resources
securebyte monitor s3://my-bucket --alerts slack
```

## 🚧 Current Status

**Status:** Planning Phase  
**Target Release:** Q4 2026  
**Language:** Go (planned) or TypeScript/Node.js  
**License:** MIT

## 📋 Roadmap

### Phase 1: Core Scanner (Q4 2026)
- [ ] AWS resource discovery and scanning
- [ ] Basic security misconfiguration detection
- [ ] JSON/YAML output formats
- [ ] CLI framework and command structure

### Phase 2: Compliance Rules (Q1 2027)
- [ ] POPIA compliance checks
- [ ] SOC 2 control validation
- [ ] ISO 27001 security checks
- [ ] CIS Benchmarks implementation
- [ ] Custom rule engine

### Phase 3: CI/CD Integration (Q2 2027)
- [ ] GitHub Actions integration
- [ ] GitLab CI support
- [ ] Jenkins plugin
- [ ] Pre-commit hooks
- [ ] Compliance gate enforcement

### Phase 4: Multi-Cloud & Advanced (Q3 2027)
- [ ] Azure support
- [ ] GCP support
- [ ] Kubernetes/container scanning
- [ ] Infrastructure-as-Code scanning (Terraform, CloudFormation)
- [ ] Drift detection

## 🎨 Design Principles

- **Fast & Lightweight** - Built for speed with minimal dependencies
- **CI/CD First** - Designed to integrate seamlessly into pipelines
- **Extensible** - Plugin architecture for custom rules and integrations
- **Developer Friendly** - Clear output, helpful errors, extensive documentation
- **Privacy Respecting** - No telemetry, all scanning happens locally or in your environment

## 🔧 Planned Installation

```bash
# Homebrew (macOS/Linux)
brew install securebyte-cli

# NPM (cross-platform)
npm install -g @securebyte/cli

# Go install
go install github.com/securebyte-consulting/securebyte-cli@latest

# Docker
docker run securebyte/cli scan aws

# Direct download
curl -sSL https://get.securebyte.co.za/cli | sh
```

## 📖 Example Usage (Planned)

### Basic Security Scan
```bash
# Scan AWS account for security issues
securebyte scan aws

# Output:
# ✓ Scanning AWS infrastructure...
# ✓ Found 127 resources
# 
# Critical Issues: 3
# High Issues: 12
# Medium Issues: 24
# Low Issues: 8
# 
# Top Issues:
# ❌ S3 bucket "customer-data" has public read access
# ❌ RDS instance "production-db" has encryption disabled
# ❌ IAM user "admin" has root account access keys
```

### CI/CD Integration Example
```yaml
# .github/workflows/security-scan.yml
name: Security Scan

on: [pull_request]

jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Install SecureByte CLI
        run: npm install -g @securebyte/cli
      
      - name: Scan Infrastructure
        run: |
          securebyte scan aws \
            --fail-on critical \
            --format markdown >> $GITHUB_STEP_SUMMARY
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

### Custom Compliance Rules
```yaml
# custom-rules.yaml
rules:
  - id: custom-s3-encryption
    name: S3 Buckets Must Use KMS Encryption
    severity: critical
    resource_type: aws_s3_bucket
    condition: |
      encryption.type == "aws:kms"
    remediation: |
      Enable KMS encryption on S3 bucket:
      aws s3api put-bucket-encryption \
        --bucket {{resource.name}} \
        --server-side-encryption-configuration \
        '{"Rules":[{"ApplyServerSideEncryptionByDefault":{"SSEAlgorithm":"aws:kms"}}]}'
```

## 🤝 Contributing

SecureByte CLI is open source and we welcome contributions! Once launched, you'll be able to contribute:

- **Security Rules** - Add detection rules for new misconfigurations
- **Cloud Providers** - Extend support to new cloud platforms
- **Integrations** - Build plugins for CI/CD tools and platforms
- **Documentation** - Improve guides and examples
- **Bug Fixes** - Help make the tool more reliable

**Contribution guidelines will be published with our first release.**

## 🔒 Security & Privacy

- **No Data Collection** - All scanning happens locally or in your environment
- **No Telemetry** - We don't track usage or send data anywhere
- **Credentials Stay Local** - Uses your existing cloud credentials (AWS CLI, environment variables)
- **Open Source** - Audit the code yourself, no black boxes

## 📖 About SecureByte

SecureByte CLI is part of the [SecureByte](https://github.com/securebyte-consulting) ecosystem - a compliance automation platform built for South African companies.

**SecureByte Platform Features:**
- ⚡ 24-hour compliance progress
- 💰 60% cheaper than international alternatives
- 🇿🇦 POPIA-first design with local expertise
- 🔒 Multi-cloud security automation
- 📊 Public Trust Centers

**Differences between CLI and Platform:**
- **CLI:** Open source, free, local scanning, CI/CD focused
- **Platform:** Full compliance automation, evidence collection, team collaboration, audit reports

The CLI is perfect for developers and DevOps teams who want to integrate security checks into their workflow. The platform is designed for compliance officers and executives who need comprehensive compliance management.

## 🔗 Related Projects

- **Main Platform:** [securebyte](private)
- **Documentation:** [securebyte-docs](https://github.com/securebyte-consulting/securebyte-docs)
- **Integrations:** [securebyte-integrations](https://github.com/securebyte-consulting/securebyte-integrations) (planned)
- **Frameworks:** [compliance-frameworks](https://github.com/securebyte-consulting/compliance-frameworks) (planned)

## 📧 Contact

Questions? Suggestions? Want to contribute?

- **Email:** securebyte.consulting@gmail.com
- **Twitter:** [coming soon]()
- **LinkedIn:** [coming soon]()

## 📄 License

SecureByte CLI will be licensed under the [MIT License](https://opensource.org/licenses/MIT).

This means you'll be free to:
- Use commercially
- Modify
- Distribute
- Use privately
- Sublicense

The only requirement is to include the original copyright and license notice.

---

**Building open-source security tools for the developer community** 🔒

*Part of the SecureByte Consulting family of projects*

---

## 🌟 Why Open Source?

We believe security tools should be transparent, accessible, and community-driven. By open-sourcing the CLI, we enable:

- **Trust through Transparency** - Audit the code that scans your infrastructure
- **Community Innovation** - Collective knowledge beats proprietary algorithms
- **Accessibility** - Free tools for startups and developers
- **Ecosystem Growth** - Building blocks for the security community

The CLI serves as a gateway to compliance automation while giving back to the community that supports us.

## 🗺️ Stay Updated

- **Star this repository** to be notified when we launch ⭐
- **Watch releases** for updates on development progress
- **Follow [@securebyte](https://twitter.com/securebyte)** for announcements

**Target Release:** Q4 2026
```