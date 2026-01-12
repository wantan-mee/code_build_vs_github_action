# Cheaper DAST Alternatives to StackHawk

## Quick Comparison: Budget DAST Options

| Tool | Annual Cost (10 apps) | Setup Difficulty | Quality | Best For |
|------|----------------------|------------------|---------|----------|
| **OWASP ZAP** | **$0 (Free)** | ⚠️ High | ⭐⭐⭐⭐ | Technical teams, tightest budgets |
| **Nuclei** | **$0 (Free)** | Medium | ⭐⭐⭐ | DevOps teams, automation |
| **Arachni** | **$0 (Free)** | Medium-High | ⭐⭐⭐ | Web apps, technical users |
| **w3af** | **$0 (Free)** | High | ⭐⭐ | Security researchers |
| **Nikto** | **$0 (Free)** | Low | ⭐⭐ | Basic server scanning |
| **StackHawk** | $10-15k | Low | ⭐⭐⭐⭐ | Easy integration, paid option |
| **Probely** | $3-8k | Low | ⭐⭐⭐ | Budget-friendly paid option |
| **ImmuniWeb** | $5-10k | Low-Medium | ⭐⭐⭐⭐ | Good value paid option |

---

## Free/Open Source Options

### 1. OWASP ZAP (Zed Attack Proxy) ⭐ BEST FREE OPTION

**Cost:** $0 (completely free, open source)

**Quality:** ⭐⭐⭐⭐ (4/5)

#### Strengths:
- ✅ **Completely free** - no hidden costs
- ✅ Very comprehensive DAST capabilities
- ✅ Actively maintained by OWASP
- ✅ Large community support
- ✅ Can automate in CI/CD
- ✅ API scanning support
- ✅ Authenticated scanning
- ✅ Proxy mode for manual testing
- ✅ Plugin ecosystem
- ✅ Docker container available

#### Weaknesses:
- ⚠️ **Requires significant setup time** (40-80 hours initial)
- ⚠️ Higher false positive rate (needs tuning)
- ⚠️ UI is functional but not modern
- ⚠️ Documentation can be overwhelming
- ⚠️ Need DevOps/security skills to configure
- ⚠️ No official support (community only)

#### What it Tests:
- SQL injection, XSS, CSRF
- Authentication/session issues
- Server misconfigurations
- OWASP Top 10
- Custom scripts possible

#### CI/CD Integration:

**GitHub Actions Example:**
```yaml
- name: ZAP Baseline Scan
  uses: zaproxy/action-baseline@v0.7.0
  with:
    target: 'https://your-app.com'

- name: ZAP Full Scan
  uses: zaproxy/action-full-scan@v0.4.0
  with:
    target: 'https://your-app.com'
```

**Automation Options:**
- ZAP CLI
- ZAP API
- Docker container
- Python/Java API

#### Setup Time:
- **Basic scan:** 4-8 hours
- **Automated in CI/CD:** 20-40 hours
- **Production-ready with tuning:** 60-100 hours

#### Best For:
- Teams with DevOps/security skills
- Companies with tight budgets
- Open source projects
- Learning DAST concepts

#### Realistic Total Cost:
```
License: $0
Engineer time: 60 hours × $75/hour = $4,500 (one-time)
Ongoing maintenance: ~10 hours/year = $750/year

Effective first year cost: ~$5,250
Year 2+: ~$750/year
```

**Still cheaper than StackHawk after year 1!**

---

### 2. Nuclei

**Cost:** $0 (free, open source)

**Quality:** ⭐⭐⭐ (3/5)

#### Strengths:
- ✅ **Completely free**
- ✅ Very fast scanning
- ✅ Template-based (easy to customize)
- ✅ 4000+ vulnerability templates
- ✅ Great for CI/CD automation
- ✅ Active community (ProjectDiscovery)
- ✅ Low false positives
- ✅ Modern, actively developed
- ✅ YAML-based templates (easy to read)

#### Weaknesses:
- ⚠️ Not a full DAST (more focused scanning)
- ⚠️ Less comprehensive than ZAP
- ⚠️ Template-dependent (what you scan depends on available templates)
- ⚠️ No GUI (CLI only)
- ⚠️ Better for specific vulnerabilities, not full app scanning

#### What it Tests:
- CVEs and misconfigurations
- Exposed panels, files
- Specific vulnerabilities
- Technology detection
- Custom checks via templates

#### CI/CD Integration:

**GitHub Actions Example:**
```yaml
- name: Nuclei Scan
  uses: projectdiscovery/nuclei-action@main
  with:
    target: https://your-app.com
    severity: high,critical
```

#### Setup Time:
- **Basic scan:** 1-2 hours
- **CI/CD integration:** 4-8 hours
- **Custom templates:** 10-20 hours

#### Best For:
- Quick vulnerability checks
- Known CVE scanning
- Lightweight CI/CD integration
- API endpoint testing
- Specific vulnerability hunting

#### Realistic Cost:
```
License: $0
Setup: 8 hours × $75 = $600 (one-time)
Maintenance: 2-4 hours/year = $300/year
```

---

### 3. Arachni

**Cost:** $0 (free, open source)

**Quality:** ⭐⭐⭐ (3/5)

#### Strengths:
- ✅ Free and open source
- ✅ Comprehensive web app scanner
- ✅ Web UI available
- ✅ Good reporting
- ✅ Modular design
- ✅ Multiple export formats

#### Weaknesses:
- ⚠️ **No longer actively maintained** (last update 2017)
- ⚠️ Missing modern web app features (SPA support limited)
- ⚠️ Installation can be tricky
- ⚠️ Ruby-based (requires Ruby environment)
- ⚠️ Slower than modern tools

#### What it Tests:
- SQL injection, XSS, CSRF
- File inclusion
- Path traversal
- OWASP Top 10

#### Setup Time:
- **Installation:** 4-8 hours
- **CI/CD:** 12-20 hours
- **Tuning:** 10-15 hours

#### Best For:
- Traditional web applications
- Teams comfortable with older tools
- One-time assessments

#### ⚠️ **Warning:** Consider more actively maintained tools like ZAP instead

---

### 4. Nikto

**Cost:** $0 (free, open source)

**Quality:** ⭐⭐ (2/5)

#### Strengths:
- ✅ Completely free
- ✅ Very easy to use
- ✅ Quick server scanning
- ✅ Good for initial recon
- ✅ Lightweight

#### Weaknesses:
- ⚠️ **Very basic** - not a full DAST
- ⚠️ Server/configuration focused only
- ⚠️ Doesn't test application logic
- ⚠️ Many false positives
- ⚠️ Noisy (generates lots of requests)
- ⚠️ Easily detected

#### What it Tests:
- Server misconfigurations
- Outdated server software
- Default files/folders
- Security headers

#### Use Case:
- Supplement to other tools
- Quick server checks
- Not a replacement for DAST

#### Setup Time: 1-2 hours

---

## Budget Paid Options (Cheaper than StackHawk)

### 5. Probely

**Cost:** $3,000 - $8,000/year (for 10 apps)

**Quality:** ⭐⭐⭐ (3/5)

#### Strengths:
- ✅ **Much cheaper than StackHawk**
- ✅ Good DAST coverage
- ✅ Easy to use
- ✅ API scanning
- ✅ CI/CD integration
- ✅ Good reporting
- ✅ Low false positives

#### Weaknesses:
- ⚠️ Smaller company (less established)
- ⚠️ Fewer integrations than bigger vendors
- ⚠️ Limited advanced features

#### Pricing:
```
Starter: ~$300/month (~$3,600/year)
- 5 targets
- Unlimited scans

Professional: ~$600/month (~$7,200/year)
- 10 targets
- API support
- Integrations
```

#### Best For:
- Small to medium teams
- API-heavy applications
- Budget-conscious with need for support

---

### 6. ImmuniWeb Community (Free Tier) + Paid

**Cost:** $0 - $10,000/year

**Quality:** ⭐⭐⭐⭐ (4/5)

#### Free Tier:
- ✅ **Free web scanning** (limited)
- ✅ SSL/TLS testing
- ✅ Mobile app testing
- ✅ API testing
- ⚠️ Manual scans (not automated)
- ⚠️ Rate limited

#### Paid Tiers:
```
ImmuniWeb SaaS: $5,000 - $10,000/year
- Automated scanning
- CI/CD integration
- Better reporting
- Support
```

#### Strengths:
- ✅ Good quality scanning
- ✅ Free tier for small projects
- ✅ Mobile app support
- ✅ API testing

#### Best For:
- Testing free tier first
- Mixed web + mobile apps
- European companies (GDPR compliant)

---

### 7. Acunetix (Lower Tier)

**Cost:** $4,500 - $8,000/year (standard license)

**Quality:** ⭐⭐⭐⭐ (4/5)

#### Strengths:
- ✅ Comprehensive DAST
- ✅ Good crawling (including SPAs)
- ✅ Network scanning included
- ✅ Good reporting
- ✅ Decent CI/CD integration

#### Weaknesses:
- ⚠️ Still not super cheap
- ⚠️ Can be complex to configure
- ⚠️ Per-target licensing

#### Pricing:
```
Standard: ~$4,500/year (1 target)
Multi-target: ~$6,000-8,000/year (3-5 targets)

Note: Can be negotiated
```

#### Best For:
- Need comprehensive features
- Network + web scanning
- Can't use free tools

---

## Hybrid/Creative Approaches

### 8. Combine Multiple Free Tools

**Cost:** $0 (labor only)

**Strategy:**
```
1. Nuclei → Fast CVE/misconfiguration checks
2. OWASP ZAP → Comprehensive DAST
3. Nikto → Server configuration
4. Custom scripts → Business logic testing
```

**Total Coverage:** ⭐⭐⭐⭐

**Setup Time:** 60-100 hours

**Maintenance:** 20 hours/year

**Effective Cost:**
```
Year 1: ~$7,500 (100 hours setup)
Year 2+: ~$1,500/year (20 hours maintenance)
```

**Best For:**
- Technical teams
- Maximum savings
- Learning opportunity

---

### 9. Managed ZAP Service

Some consultants offer managed ZAP:

**Cost:** $2,000 - $5,000/year

**What you get:**
- Pre-configured ZAP setup
- CI/CD templates
- Tuned for low false positives
- Basic support

**Best For:**
- Want ZAP without setup hassle
- Small budget but need support

---

## Recommended Budget Approaches

### Ultra Budget: Free Only

```
Primary: OWASP ZAP
Supplemental: Nuclei
Quick checks: Nikto

Total cost: ~$5,000 year 1 (setup), ~$750/year ongoing
```

✅ Best for: Startups, bootstrapped companies

---

### Smart Budget: Mix Free + Cheap Paid

```
Primary: Probely ($3,600/year)
Backup/Advanced: OWASP ZAP (free, $2,000 setup)

Total cost: ~$5,600 year 1, ~$4,000/year ongoing
```

✅ Best for: Small teams wanting support + coverage

---

### Best Value: Premium Free Tool

```
Primary: OWASP ZAP (comprehensive setup)
Supplement: Nuclei (fast checks)

Total cost: ~$6,000 year 1 (proper setup), ~$1,000/year ongoing
```

✅ Best for: Technical teams, long-term savings

---

## Complete Cost Comparison (10 Apps, 3 Years)

| Solution | Year 1 | Year 2-3 | 3-Year Total |
|----------|--------|----------|--------------|
| **StackHawk** | $12,000 | $12,000/yr | **$36,000** |
| **Probely** | $7,200 | $7,200/yr | **$21,600** |
| **Acunetix** | $8,000 | $8,000/yr | **$24,000** |
| **ZAP (well setup)** | $6,000 | $1,000/yr | **$8,000** |
| **Nuclei + ZAP** | $6,500 | $1,500/yr | **$9,500** |
| **ImmuniWeb** | $7,000 | $7,000/yr | **$21,000** |

**Savings vs StackHawk:**
- ZAP: **$28,000 saved (78%)**
- Nuclei + ZAP: **$26,500 saved (74%)**
- Probely: **$14,400 saved (40%)**

---

## My Recommendations by Scenario

### Scenario 1: Tightest Budget, Technical Team

**Recommendation:** OWASP ZAP + Nuclei

**Cost:** ~$8,000 over 3 years

**Why:**
- ✅ Maximum savings ($28k vs StackHawk)
- ✅ Comprehensive coverage
- ✅ Your team can handle the complexity
- ✅ Better long-term value

**Setup checklist:**
- [ ] Allocate 60-80 hours for ZAP setup
- [ ] Create CI/CD automation
- [ ] Document processes
- [ ] Train team
- [ ] Set up regular scans

---

### Scenario 2: Want Support, Limited Budget

**Recommendation:** Probely

**Cost:** ~$22k over 3 years

**Why:**
- ✅ Still 40% cheaper than StackHawk
- ✅ Professional support included
- ✅ Easy to use
- ✅ Good for APIs
- ✅ Less setup time

---

### Scenario 3: Need Quick Start, Can Invest Later

**Recommendation:** Start with ZAP, add Probely if needed

**Phase 1 (Months 1-3):**
- Use OWASP ZAP free tier
- Basic automation
- Learn DAST concepts
- Cost: $2,000 setup

**Phase 2 (Months 4+):**
- Evaluate if ZAP is enough
- If too much work → Add Probely
- If working well → Invest in better ZAP setup

---

### Scenario 4: Zero Budget Temporarily

**Recommendation:** ImmuniWeb Free + Nuclei

**Cost:** $0 cash, ~10 hours/month effort

**Approach:**
- Use ImmuniWeb free tier for manual scans
- Use Nuclei for automated checks
- Plan to upgrade when budget available

---

## Setup Guide: OWASP ZAP for CI/CD

### Quick Start (4-8 hours)

```yaml
# .github/workflows/security.yml

name: DAST Scan

on: [push, pull_request]

jobs:
  zap_scan:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: ZAP Baseline Scan
        uses: zaproxy/action-baseline@v0.7.0
        with:
          target: 'https://staging.your-app.com'
          rules_file_name: '.zap/rules.tsv'
          cmd_options: '-a'

      - name: Upload results
        uses: actions/upload-artifact@v3
        with:
          name: zap-report
          path: report_html.html
```

### Production Setup (40-60 hours)

**Components:**
1. Authenticated scanning setup
2. API definition import (OpenAPI)
3. False positive tuning
4. Custom scripts
5. Context configuration
6. Reporting automation
7. Integration with issue tracking

**Deliverables:**
- Automated pipeline
- Low false positive rate
- Comprehensive coverage
- Team training

---

## Final Recommendation for Your Scenario

**For 10 devs, 10 projects, DAST only:**

### Option 1: Maximum Savings 🏆

**OWASP ZAP (comprehensive setup)**

```
Year 1: $6,000 (one-time setup)
Year 2-3: $1,000/year (maintenance)
3-Year Total: $8,000

vs StackHawk ($36,000) = Save $28,000
vs Snyk+StackHawk ($73,000 total) = $65,000 total
```

**Total Security Stack:**
- Snyk Team: $11,760/year
- ZAP: $6,000 one-time
- **Total Year 1: $17,760**
- **Total Years 2-3: $12,760/year**

**3-year total: $43,280** vs **$73,000** (Snyk+StackHawk)
**Save: $29,720 over 3 years**

---

### Option 2: Balance of Cost & Ease

**Probely**

```
Year 1-3: $7,200/year
3-Year Total: $21,600

vs StackHawk = Save $14,400
```

**Total Security Stack:**
- Snyk Team: $11,760/year
- Probely: $7,200/year
- **Total: $18,960/year**

**3-year total: $56,880** vs **$73,000**
**Save: $16,120 over 3 years**

---

### Option 3: Keep StackHawk

If your team lacks DevOps security skills or time:

```
Snyk + StackHawk: $24,000/year
3-year: $73,000

Worth it if:
- No time for ZAP setup
- Need vendor support
- Developer experience is critical
```

---

## Bottom Line

**Cheapest options:**
1. **OWASP ZAP** (free) - $8k over 3 years
2. **Nuclei + ZAP** (free) - $9.5k over 3 years
3. **Probely** (paid) - $21.6k over 3 years
4. **StackHawk** (paid) - $36k over 3 years

**My recommendation: Start with OWASP ZAP.** Allocate 60 hours ($4,500) for proper setup. You'll save $28,000 over 3 years vs StackHawk, and get comprehensive DAST coverage. If it's too much work after trying it, you can always upgrade to Probely or StackHawk.

**Complete Budget Stack:**
- **SonarQube Community** (free) → Code quality + basic SAST
- **Trivy** (free) → Containers + dependencies + IaC
- **Snyk Team** ($11,760/year) → Better SAST + SCA
- **OWASP ZAP** ($6,000 setup) → DAST

**Total Year 1:** $17,760
**Total Years 2-3:** $12,760/year each

That's **90% of Veracode's capabilities at 25-35% of the cost.**
