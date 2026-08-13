# MedFlow Agents - Project Architecture

**Version:** 1.0  
**Last Updated:** August 13, 2026  
**Status:** AUTHORITATIVE

---

## Executive Summary

This document establishes the **single source of truth** for the MedFlow Agents website architecture. All team members must follow these rules for all future development.

---

## Authoritative Project

| Property | Value |
|----------|-------|
| **Project Name** | `medflow-practicelaunch` |
| **Project ID** | `prj_oouY0Woj7XIRFCe44n9Zj3BkAgPs` |
| **Vercel Team** | vcentralprocure-2350s-projects |
| **Status** | ✅ PRODUCTION |
| **Created** | July 26, 2026 |

### Production Deployment
- **Current Deployment ID:** `dpl_HtBuCsb2nQwEsfs7curDkhDu3mAJ`
- **Vercel URL:** `medflow-practicelaunch-iooio99vm-vcentralprocure-2350s-projects.vercel.app`
- **Custom Domain:** `practicelaunch.medflowagents.com` (temporary)
- **Target Domain:** `medflowagents.com` (pending domain transfer)

---

## Production Domain Strategy

### Primary Domain (Target)
```
https://medflowagents.com/
```

### URL Structure
All content must use this architecture:

```
https://medflowagents.com/                          (Homepage)
https://medflowagents.com/pages/blog/[article].html (Blog articles)
https://medflowagents.com/pages/resources/          (Resources)
https://medflowagents.com/pages/contact.html        (Contact)
https://medflowagents.com/pages/privacy.html        (Privacy)
https://medflowagents.com/pages/terms.html          (Terms)
https://medflowagents.com/assets/                   (Static assets)
```

### Domain Status
| Domain | Project | Status | Action Required |
|--------|---------|--------|-----------------|
| `medflowagents.com` | medflow-new-structure (legacy) | ⚠️ WRONG PROJECT | Transfer to medflow-practicelaunch |
| `www.medflowagents.com` | medflow-new-structure (legacy) | ⚠️ WRONG PROJECT | Transfer to medflow-practicelaunch |
| `practicelaunch.medflowagents.com` | medflow-practicelaunch | ✅ CORRECT | Maintain as alias or redirect |

---

## Legacy Project Reference

### medflow-new-structure (LEGACY ONLY)
| Property | Value |
|----------|-------|
| **Project Name** | `medflow-new-structure` |
| **Project ID** | `prj_ynYWZ2oH4ORmkVgdIsTOPLDRQCTC` |
| **Status** | ⚠️ LEGACY - DO NOT USE FOR PRODUCTION |
| **Created** | August 2, 2026 |
| **Current Domains** | `medflowagents.com`, `www.medflowagents.com` |
| **SSO Protection** | ENABLED (requires authentication) |
| **Last Commit** | da1debf5 "Update business name" |

### Why This Project Exists
- Created during a restructure attempt
- Root domain was assigned here but never transferred
- Has SSO protection preventing public access
- **DO NOT** deploy new content here
- **DO NOT** use for production
- **MAY** be used for reference or historical comparison only

---

## Critical Rules

### Rule 1: NEVER Create Another MedFlow Vercel Project
```
STATUS: MANDATORY
```
- All future MedFlow Agents website work MUST use `medflow-practicelaunch`
- No exceptions for testing, experiments, or new features
- Use preview deployments within this project for testing

### Rule 2: ALL Production Content Must Use medflowagents.com
```
STATUS: MANDATORY
```
- All canonical URLs must use `https://medflowagents.com/`
- All internal links must use root domain paths
- No subdomain references in production content
- Update all hardcoded URLs to use root domain

### Rule 3: Preview Deployments Allowed, Production Stays Fixed
```
STATUS: MANDATORY
```
- Preview deployments: ✅ ALLOWED for testing
- Production domain: ✅ FIXED to medflowagents.com
- Never deploy production content to preview URLs
- Always verify project name before production deployment

### Rule 4: Verify Before Every Deployment
```
STATUS: MANDATORY
```
Pre-deployment checklist:
- [ ] Confirm project name is `medflow-practicelaunch`
- [ ] Confirm project ID is `prj_oouY0Woj7XIRFCe44n9Zj3BkAgPs`
- [ ] Confirm production domain will be `medflowagents.com`
- [ ] Confirm no files will be lost or overwritten
- [ ] Run QA verification after deployment

### Rule 5: Do Not Modify Legacy Project
```
STATUS: MANDATORY
```
- Do NOT delete `medflow-new-structure`
- Do NOT deploy to `medflow-new-structure`
- Do NOT modify domains on `medflow-new-structure` without explicit approval
- Keep for reference until domain transfer is complete

---

## Current Content Inventory

### Verified Pages (medflow-practicelaunch)
| Page | URL Path | Status | Last Updated |
|------|----------|--------|--------------|
| Homepage | `/index.html` | ✅ Live | Aug 13, 2026 |
| Contact | `/pages/contact.html` | ✅ Live | Aug 13, 2026 |
| Privacy | `/pages/privacy.html` | ✅ Live | Aug 13, 2026 |
| Terms | `/pages/terms.html` | ✅ Live | Aug 13, 2026 |
| Pillar Article | `/pages/blog/automating-patient-intake.html` | ✅ Live | Aug 13, 2026 |
| Article #1 | `/pages/blog/missed-call-cost-calculator.html` | ✅ Live | Aug 13, 2026 |

### Assets & Configuration
| Type | Location | Status |
|------|----------|--------|
| CSS | `/styles.css` | ✅ Live |
| JavaScript | `/js/script.js` | ✅ Live |
| Documentation | `/content/` | ✅ In repo |
| Components | `/components/` | ✅ In repo |
| Data/Config | `/data/` | ✅ In repo |

---

## Migration Status

### Completed ✅
- Article #1 deployed to authoritative project
- All pages verified working
- Reciprocal links between pillar and Article #1
- Project architecture documented

### Pending ⏳
- Transfer `medflowagents.com` from legacy to authoritative project
- Transfer `www.medflowagents.com` from legacy to authoritative project
- Update all canonical URLs to use root domain
- Verify root domain serves all content correctly
- Configure `practicelaunch.medflowagents.com` as redirect

### Blocked 🚫
- Article #2 development (pending domain migration approval)
- Any new content creation (pending domain migration approval)

---

## Emergency Contacts & Procedures

### If Wrong Project Deployed
1. **STOP** immediately
2. Do NOT panic
3. Verify which project was affected
4. Contact: [Add your contact here]
5. Document what happened

### If Domain Issues
1. Check Vercel dashboard for domain status
2. Verify DNS configuration
3. Check deployment aliases
4. Contact: [Add your contact here]

---

## Audit Trail

| Date | Action | Performed By |
|------|--------|--------------|
| Aug 13, 2026 | Project architecture audit completed | OpenClaw |
| Aug 13, 2026 | Article #1 deployed to medflow-practicelaunch | OpenClaw |
| Aug 13, 2026 | PROJECT_ARCHITECTURE.md created | OpenClaw |
| [Pending] | Domain transfer from legacy to authoritative | [Pending approval] |

---

## Approval

This architecture is approved by:

- [ ] Technical Lead: _________________ Date: _______
- [ ] Product Owner: _________________ Date: _______

---

**END OF DOCUMENT**

*Any changes to this architecture require explicit written approval.*
