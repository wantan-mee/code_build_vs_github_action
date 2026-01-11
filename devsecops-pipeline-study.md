# DevSecOps CI/CD Pipeline Study Guide

## Table of Contents
1. [Introduction to DevSecOps](#introduction-to-devsecops)
2. [CI/CD Pipeline Stages](#cicd-pipeline-stages)
3. [Build Stage](#build-stage)
4. [Linting Stage](#linting-stage)
5. [Security Scanning](#security-scanning)
6. [Popular CI/CD Platforms](#popular-cicd-platforms)
7. [Implementation Examples](#implementation-examples)
8. [Best Practices](#best-practices)
9. [Tool Comparison](#tool-comparison)

---

## Introduction to DevSecOps

**DevSecOps** integrates security practices into the DevOps workflow, making security a shared responsibility throughout the entire software development lifecycle.

### Key Principles:
- **Shift Left**: Integrate security early in the development process
- **Automation**: Automate security testing and compliance checks
- **Continuous Monitoring**: Monitor security throughout the pipeline
- **Collaboration**: Break down silos between development, security, and operations teams

### Why DevSecOps in CI/CD?
- Catch vulnerabilities early when they're cheaper to fix
- Reduce security debt
- Maintain compliance requirements
- Speed up delivery without compromising security

---

## CI/CD Pipeline Stages

A typical DevSecOps pipeline includes:

```
Code Commit → Build → Lint → Unit Tests → Security Scans → Integration Tests → Deploy → Monitor
```

### Core Stages We'll Focus On:

1. **Build**: Compile/package the application
2. **Lint**: Code quality and style checks
3. **Security Scan**: Multiple layers of security testing

---

## Build Stage

### Purpose
Compile source code, resolve dependencies, and create deployable artifacts.

### Key Activities:
- **Dependency Resolution**: Download and verify dependencies
- **Compilation**: Build the application (for compiled languages)
- **Artifact Creation**: Package into containers, binaries, or packages
- **Caching**: Speed up builds with dependency caching

### Common Tools by Language:

| Language | Build Tools |
|----------|-------------|
| JavaScript/Node.js | npm, yarn, pnpm, webpack, vite |
| Python | pip, poetry, setuptools |
| Java | Maven, Gradle |
| Go | go build, go mod |
| .NET | dotnet build, MSBuild |
| Ruby | bundler, rake |
| Rust | cargo |

### Build Best Practices:
- Use lock files (package-lock.json, poetry.lock, Gemfile.lock)
- Pin dependency versions
- Use multi-stage Docker builds for smaller images
- Cache dependencies between builds
- Fail fast on build errors
- Generate build artifacts (SBOM - Software Bill of Materials)

---

## Linting Stage

### Purpose
Enforce code quality, consistency, and catch potential bugs before runtime.

### Types of Linting:

#### 1. **Code Style Linting**
Enforces consistent formatting and style conventions.

**Tools:**
- **JavaScript/TypeScript**: ESLint, Prettier, StandardJS
- **Python**: Pylint, Flake8, Black, Ruff
- **Go**: golint, gofmt, golangci-lint
- **Java**: Checkstyle, SpotBugs
- **Ruby**: RuboCop
- **Rust**: clippy, rustfmt

#### 2. **Static Analysis**
Detects bugs, code smells, and potential issues.

**Tools:**
- **SonarQube/SonarCloud**: Multi-language support
- **CodeClimate**: Code quality metrics
- **Semgrep**: Pattern-based static analysis
- **PMD**: Java, Apex, JavaScript
- **Pylint**: Python
- **RuboCop**: Ruby

#### 3. **Type Checking**
Ensures type safety (for languages with optional typing).

**Tools:**
- **TypeScript**: tsc (TypeScript compiler)
- **Python**: mypy, pyright
- **PHP**: Psalm, PHPStan

### Linting Best Practices:
- Define linting rules in version-controlled config files
- Use pre-commit hooks for fast feedback
- Fail the pipeline on critical issues
- Use warning levels (error, warning, info)
- Integrate with IDE for developer feedback
- Keep rules consistent across team

---

## Security Scanning

Security scanning is the heart of DevSecOps. It includes multiple layers:

### 1. **Secret Scanning**

**Purpose**: Detect hardcoded secrets, API keys, passwords, tokens.

**Tools:**
- **TruffleHog**: Deep secret scanning in git history
- **GitGuardian**: Real-time secret detection
- **Gitleaks**: Fast, configurable secret scanner
- **detect-secrets**: Yelp's secret scanner
- **GitHub Secret Scanning**: Built into GitHub

**What it catches:**
- API keys
- Private keys
- Database passwords
- AWS credentials
- OAuth tokens

**Best Practice**: Scan both current code and git history.

---

### 2. **Dependency Scanning (SCA - Software Composition Analysis)**

**Purpose**: Identify vulnerabilities in third-party dependencies.

**Tools:**
- **Snyk**: Comprehensive vulnerability database
- **Dependabot**: GitHub's automated dependency updates
- **OWASP Dependency-Check**: Free, open-source
- **npm audit**: Built into npm
- **pip-audit**: Python package auditing
- **Trivy**: Multi-scanner including dependencies
- **WhiteSource/Mend**: Enterprise SCA
- **Grype**: Vulnerability scanner by Anchore

**What it checks:**
- Known CVEs (Common Vulnerabilities and Exposures)
- Outdated dependencies
- License compliance
- Dependency health metrics

**Best Practice**:
- Scan on every commit
- Auto-update non-breaking security patches
- Set severity thresholds (fail on high/critical)

---

### 3. **SAST (Static Application Security Testing)**

**Purpose**: Analyze source code for security vulnerabilities without executing it.

**Tools:**
- **SonarQube**: Code quality + security
- **Semgrep**: Fast, customizable patterns
- **Checkmarx**: Enterprise SAST
- **Veracode**: Cloud-based SAST
- **Bandit**: Python security linter
- **Brakeman**: Ruby on Rails security scanner
- **ESLint security plugins**: JavaScript security rules
- **CodeQL**: GitHub's semantic code analysis

**What it catches:**
- SQL injection
- Cross-site scripting (XSS)
- Path traversal
- Insecure deserialization
- Hardcoded credentials
- Weak cryptography
- Buffer overflows

**Best Practice**:
- Run early in pipeline
- Integrate with developer IDE
- Create custom rules for your framework
- Review false positives and tune rules

---

### 4. **Container Scanning**

**Purpose**: Scan Docker images for vulnerabilities and misconfigurations.

**Tools:**
- **Trivy**: Fast, comprehensive container scanner
- **Clair**: Open-source container scanner
- **Anchore**: Container analysis and compliance
- **Snyk Container**: Container vulnerability scanning
- **Aqua Security**: Enterprise container security
- **Docker Scan**: Built into Docker
- **Grype**: Container and filesystem scanner

**What it checks:**
- Vulnerable OS packages
- Vulnerable application dependencies
- Misconfigured containers
- Base image vulnerabilities
- Secrets in images

**Best Practice**:
- Scan both during build and in registry
- Use minimal base images (Alpine, distroless)
- Don't run containers as root
- Scan on schedule for new CVEs

---

### 5. **Infrastructure as Code (IaC) Scanning**

**Purpose**: Detect security misconfigurations in infrastructure code.

**Tools:**
- **Checkov**: Multi-cloud IaC scanner (Terraform, CloudFormation, Kubernetes, etc.)
- **tfsec**: Terraform security scanner
- **Terrascan**: IaC security scanner
- **KICS**: Universal IaC scanner by Checkmarx
- **Snyk IaC**: Cloud security configuration scanner
- **Bridgecrew**: Policy-as-code platform

**What it checks:**
- Publicly exposed resources
- Unencrypted storage
- Weak authentication
- Overly permissive IAM policies
- Missing security groups
- Kubernetes misconfigurations

**Best Practice**:
- Scan Terraform/CloudFormation/Kubernetes YAML files
- Enforce policies before deployment
- Use policy-as-code frameworks

---

### 6. **License Scanning**

**Purpose**: Ensure compliance with open-source licenses.

**Tools:**
- **FOSSA**: License compliance and attribution
- **Black Duck**: License and security scanning
- **WhiteSource**: License compliance
- **LicenseFinder**: Multi-language license detector

**What it checks:**
- Incompatible licenses (GPL, AGPL)
- License conflicts
- Attribution requirements

---

## Popular CI/CD Platforms

### 1. **GitHub Actions**
- Native to GitHub
- YAML-based workflows
- Large marketplace of actions
- Free tier for public repos
- Matrix builds for testing multiple versions

**Pros**: Easy GitHub integration, good free tier
**Cons**: Can be expensive for private repos with heavy usage

### 2. **GitLab CI/CD**
- Built into GitLab
- YAML-based .gitlab-ci.yml
- Auto DevOps features
- Container registry included
- Good for complete GitOps

**Pros**: All-in-one platform, generous free tier
**Cons**: Steeper learning curve

### 3. **Jenkins**
- Self-hosted, open-source
- Groovy-based pipelines
- Extensive plugin ecosystem
- Flexible and customizable

**Pros**: Free, highly customizable, mature
**Cons**: Requires maintenance, UI can be dated

### 4. **CircleCI**
- Cloud-based or self-hosted
- YAML configuration
- Docker-first approach
- Good parallelization

**Pros**: Fast builds, good caching
**Cons**: Pricing can be expensive

### 5. **Azure DevOps**
- Microsoft's CI/CD platform
- YAML pipelines
- Tight Azure integration
- Boards, Repos, Artifacts included

**Pros**: Great for Azure/Microsoft stack
**Cons**: Complex for simple projects

### 6. **Travis CI**
- Cloud-based
- YAML configuration
- Good for open-source

**Pros**: Simple setup
**Cons**: Pricing changes, less popular now

---

## Implementation Examples

### GitHub Actions Example Structure

```yaml
name: DevSecOps Pipeline

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      # Checkout code
      # Setup language runtime
      # Install dependencies
      # Build application
      # Upload artifacts

  lint:
    runs-on: ubuntu-latest
    steps:
      # Run code style checks
      # Run static analysis
      # Report results

  security-secrets:
    runs-on: ubuntu-latest
    steps:
      # Scan for secrets

  security-dependencies:
    runs-on: ubuntu-latest
    steps:
      # Scan dependencies
      # Check for CVEs

  security-sast:
    runs-on: ubuntu-latest
    steps:
      # Run SAST tools
      # Upload results

  security-container:
    runs-on: ubuntu-latest
    needs: build
    steps:
      # Build Docker image
      # Scan container

  deploy:
    runs-on: ubuntu-latest
    needs: [build, lint, security-secrets, security-dependencies, security-sast]
    if: github.ref == 'refs/heads/main'
    steps:
      # Deploy to environment
```

### GitLab CI Example Structure

```yaml
stages:
  - build
  - lint
  - security
  - test
  - deploy

build:
  stage: build
  # Build steps

lint:
  stage: lint
  # Linting steps

secret-scan:
  stage: security
  # Secret scanning

dependency-scan:
  stage: security
  # Dependency scanning

sast:
  stage: security
  # SAST scanning

container-scan:
  stage: security
  # Container scanning

deploy:
  stage: deploy
  # Deployment steps
```

---

## Best Practices

### 1. **Pipeline Design**
- Keep pipelines fast (< 10 minutes ideal)
- Run tests in parallel where possible
- Fail fast - run quick checks first
- Cache dependencies between runs
- Use matrix builds for multiple environments

### 2. **Security Gates**
- Define security thresholds (e.g., no HIGH or CRITICAL vulnerabilities)
- Allow manual approval for production deployments
- Don't block on low-severity issues in development
- Implement security exceptions process for justified risks

### 3. **Secrets Management**
- Never hardcode secrets in code or configs
- Use CI/CD platform's secret management
- Rotate secrets regularly
- Use short-lived tokens where possible
- Scan git history for leaked secrets

### 4. **Artifact Management**
- Sign build artifacts
- Generate SBOM (Software Bill of Materials)
- Store artifacts in secure registries
- Implement retention policies
- Scan artifacts before deployment

### 5. **Monitoring and Alerts**
- Alert on pipeline failures
- Track security metrics (vulnerabilities found/fixed)
- Monitor build times
- Set up notifications for critical issues
- Create security dashboards

### 6. **Developer Experience**
- Provide clear error messages
- Make pipelines self-service
- Document security requirements
- Integrate security in IDE
- Fast feedback loops (pre-commit hooks)

### 7. **Compliance**
- Generate audit trails
- Store security scan results
- Implement policy-as-code
- Track compliance metrics
- Regular security reviews

---

## Tool Comparison

### Secret Scanning Tools

| Tool | Open Source | Languages | CI/CD Integration | Price |
|------|-------------|-----------|-------------------|-------|
| Gitleaks | Yes | All | Easy | Free |
| TruffleHog | Yes | All | Easy | Free |
| GitGuardian | No | All | Easy | Paid (free tier) |
| detect-secrets | Yes | All | Medium | Free |

### Dependency Scanning Tools

| Tool | Open Source | Languages | Database | Price |
|------|-------------|-----------|----------|-------|
| Snyk | No | 15+ | Proprietary | Paid (free tier) |
| OWASP Dependency-Check | Yes | Java, .NET, Ruby, Python, Node.js | NVD | Free |
| Trivy | Yes | Multiple | Multiple sources | Free |
| npm audit | Yes | JavaScript | npm registry | Free |
| pip-audit | Yes | Python | PyPI + OSV | Free |

### SAST Tools

| Tool | Open Source | Languages | False Positive Rate | Price |
|------|-------------|-----------|---------------------|-------|
| SonarQube | Community edition | 25+ | Medium | Free/Paid |
| Semgrep | Yes | 30+ | Low | Free/Paid |
| CodeQL | No (queries are) | 10+ | Low | Free for open source |
| Bandit | Yes | Python | Medium | Free |
| Brakeman | Yes | Ruby/Rails | Low | Free |

### Container Scanning Tools

| Tool | Open Source | Databases | Speed | Price |
|------|-------------|-----------|-------|-------|
| Trivy | Yes | Multiple | Fast | Free |
| Clair | Yes | CVE databases | Medium | Free |
| Snyk Container | No | Proprietary | Fast | Paid (free tier) |
| Grype | Yes | Multiple | Fast | Free |

---

## Getting Started Checklist

### Phase 1: Foundation
- [ ] Choose CI/CD platform
- [ ] Set up basic build pipeline
- [ ] Add linting for code quality
- [ ] Implement secret scanning

### Phase 2: Security Integration
- [ ] Add dependency scanning
- [ ] Implement SAST scanning
- [ ] Set up container scanning (if using containers)
- [ ] Define security thresholds

### Phase 3: Optimization
- [ ] Optimize pipeline speed
- [ ] Implement caching
- [ ] Add parallel execution
- [ ] Set up security dashboards

### Phase 4: Advanced
- [ ] Add IaC scanning
- [ ] Implement DAST (Dynamic testing)
- [ ] Set up runtime security monitoring
- [ ] Create security metrics and KPIs

---

## Key Takeaways

1. **Start Simple**: Begin with build, lint, and basic security scans
2. **Automate Everything**: Security checks should be automatic, not manual
3. **Shift Left**: Catch issues early when they're cheaper to fix
4. **Don't Block Unnecessarily**: Balance security with developer velocity
5. **Continuous Improvement**: Regularly review and update security policies
6. **Educate Team**: Security is everyone's responsibility
7. **Measure Success**: Track metrics like vulnerabilities found/fixed, MTTR

---

## Additional Resources

### Learning Resources:
- OWASP DevSecOps Guideline
- NIST DevSecOps Framework
- Cloud Security Alliance DevSecOps Working Group
- CIS Benchmarks

### Communities:
- DevSecOps Community on Reddit
- OWASP Slack channels
- Cloud Native Security Community

### Certifications:
- Certified DevSecOps Professional (CDP)
- AWS Certified Security - Specialty
- Certified Kubernetes Security Specialist (CKS)

---

## Conclusion

A robust DevSecOps pipeline integrates security at every stage:
- **Build**: Ensures reproducible, secure artifacts
- **Lint**: Maintains code quality and catches basic issues
- **Security Scans**: Multiple layers (secrets, dependencies, SAST, containers, IaC)

The goal is to make security transparent to developers while maintaining velocity. Start small, automate progressively, and continuously improve your security posture.
