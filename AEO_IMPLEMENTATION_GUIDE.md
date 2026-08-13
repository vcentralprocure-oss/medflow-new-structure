# MedFlow AEO Layer - Implementation Guide

## Overview

This guide documents how to implement Answer Engine Optimization (AEO) schema markup in MedFlow's static HTML/Vercel architecture, reverse-engineered from the AI Booster WordPress plugin methodology.

---

## What We Built

### Schema Templates (in `/data/schemas/`)

| File | Purpose | Usage |
|------|---------|-------|
| `organization.json` | Site-wide entity recognition | All pages |
| `article.json` | Blog posts and articles | Article pages |
| `breadcrumb.json` | Navigation structure | All pages |
| `faq.json` | FAQ sections | Articles with Q&A |
| `howto.json` | Step-by-step guides | Calculator, tutorials |
| `webpage.json` | Generic pages | Contact, privacy, terms |

### Schema Implementation Status

| Page | Organization | Article | Breadcrumb | FAQ | HowTo | Status |
|------|------------|---------|------------|-----|-------|--------|
| Homepage | ✅ | - | - | - | - | ✅ Complete |
| Article #1 (Calculator) | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ Complete |
| Pillar Article | ✅ | ✅ | ✅ | ✅ | - | ✅ Complete |
| Insights Hub | - | - | - | - | - | ⏳ Pending |
| Contact | - | - | - | - | - | ⏳ Pending |
| Privacy | - | - | - | - | - | ⏳ Pending |
| Terms | - | - | - | - | - | ⏳ Pending |

---

## How to Add Schema to a New Page

### Step 1: Determine Page Type

| Page Type | Primary Schema | Secondary Schema |
|-----------|---------------|------------------|
| Homepage | Organization + WebSite | Service |
| Article/Guide | Organization + Article | Breadcrumb + FAQ + HowTo |
| Calculator/Tool | Organization + Article | Breadcrumb + HowTo |
| Generic Page | Organization + WebPage | Breadcrumb |

### Step 2: Copy Template

Use the appropriate template from `/data/schemas/` as your starting point.

### Step 3: Customize Variables

Replace template variables with actual content:

```json
// Template variables to replace:
"{{TITLE}}" → "Actual Article Title"
"{{DESCRIPTION}}" → "Actual meta description"
"{{DATE_PUBLISHED}}" → "2026-08-13"
"{{CANONICAL_URL}}" → "https://medflowagents.com/pages/blog/article.html"
```

### Step 4: Inject into HTML

Add the schema in the `<head>` section, after stylesheets:

```html
<link rel="stylesheet" href="styles.css">

<!-- AEO Schema Markup -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@graph": [
    // ... schema objects
  ]
}
</script>
</head>
```

### Step 5: Validate

Test with Google's tools:
- [Rich Results Test](https://search.google.com/test/rich-results)
- [Schema Validator](https://validator.schema.org/)

---

## Schema Patterns by Page Type

### Pattern 1: Homepage

```json
{
  "@context": "https://schema.org",
  "@graph": [
    { "@type": "Organization" },
    { "@type": "WebSite" },
    { "@type": "WebPage" },
    { "@type": "Service" }
  ]
}
```

### Pattern 2: Article/Guide

```json
{
  "@context": "https://schema.org",
  "@graph": [
    { "@type": "Organization" },
    { "@type": "Article" },
    { "@type": "BreadcrumbList" },
    { "@type": "FAQPage" }
  ]
}
```

### Pattern 3: Interactive Tool/Calculator

```json
{
  "@context": "https://schema.org",
  "@graph": [
    { "@type": "Organization" },
    { "@type": "Article" },
    { "@type": "BreadcrumbList" },
    { "@type": "HowTo" },
    { "@type": "FAQPage" }
  ]
}
```

---

## Article #2 Schema Template (Ready to Use)

When creating Article #2 (HIPAA Compliance Checklist), use this schema structure:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Organization",
      "@id": "https://medflowagents.com/#organization"
      // ... (copy from existing pages)
    },
    {
      "@type": "Article",
      "headline": "HIPAA Compliance Checklist for AI Voice Agents: 7-Point Vendor Evaluation",
      "description": "Complete HIPAA compliance checklist for evaluating AI voice agent vendors. Includes BAA requirements, security standards, and red flags to avoid.",
      "author": {
        "@type": "Organization",
        "name": "MedFlow Agents"
      },
      "publisher": {
        "@type": "Organization",
        "name": "MedFlow Agents"
      },
      "datePublished": "{{DATE}}",
      "dateModified": "{{DATE}}",
      "mainEntityOfPage": {
        "@type": "WebPage",
        "@id": "https://medflowagents.com/pages/blog/hipaa-compliance-checklist.html"
      }
    },
    {
      "@type": "BreadcrumbList",
      "itemListElement": [
        {
          "@type": "ListItem",
          "position": 1,
          "name": "Home",
          "item": "https://medflowagents.com/"
        },
        {
          "@type": "ListItem",
          "position": 2,
          "name": "Insights",
          "item": "https://medflowagents.com/pages/insights/"
        },
        {
          "@type": "ListItem",
          "position": 3,
          "name": "HIPAA Compliance Checklist",
          "item": "https://medflowagents.com/pages/blog/hipaa-compliance-checklist.html"
        }
      ]
    },
    {
      "@type": "FAQPage",
      "mainEntity": [
        {
          "@type": "Question",
          "name": "What is a Business Associate Agreement (BAA)?",
          "acceptedAnswer": {
            "@type": "Answer",
            "text": "A BAA is a contract between a covered entity (healthcare provider) and a business associate (AI vendor) that establishes how protected health information (PHI) will be handled, secured, and reported. It's required by HIPAA for any vendor that accesses PHI."
          }
        },
        {
          "@type": "Question",
          "name": "What security certifications should AI healthcare vendors have?",
          "acceptedAnswer": {
            "@type": "Answer",
            "text": "AI healthcare vendors should have SOC 2 Type II certification, HIPAA compliance attestation, and preferably HITRUST CSF certification. These demonstrate adherence to security and privacy standards required for handling PHI."
          }
        },
        {
          "@type": "Question",
          "name": "What are red flags when evaluating AI voice agent vendors?",
          "acceptedAnswer": {
            "@type": "Answer",
            "text": "Red flags include: unwillingness to sign a BAA, no encryption at rest or in transit, data stored outside the US, no audit logging, vague security practices, no SOC 2 certification, and inability to provide compliance documentation."
          }
        }
      ]
    },
    {
      "@type": "HowTo",
      "name": "How to Evaluate HIPAA-Compliant AI Voice Agent Vendors",
      "description": "7-step process for evaluating AI voice agent vendors for HIPAA compliance and security standards.",
      "totalTime": "PT30M",
      "step": [
        {
          "@type": "HowToStep",
          "position": 1,
          "name": "Request Business Associate Agreement",
          "text": "Ask the vendor for their standard BAA template. Review termination clauses, breach notification requirements, and data handling provisions."
        },
        {
          "@type": "HowToStep",
          "position": 2,
          "name": "Verify Security Certifications",
          "text": "Request proof of SOC 2 Type II certification and HIPAA compliance attestation. Verify certificates are current and from reputable auditors."
        },
        {
          "@type": "HowToStep",
          "position": 3,
          "name": "Review Data Handling Practices",
          "text": "Confirm data is encrypted at rest and in transit, stored in US-based data centers, and subject to regular security audits."
        },
        {
          "@type": "HowToStep",
          "position": 4,
          "name": "Check Audit and Logging Capabilities",
          "text": "Ensure the system provides comprehensive audit logs of all PHI access, modifications, and system events with retention policies."
        },
        {
          "@type": "HowToStep",
          "position": 5,
          "name": "Assess Breach Notification Procedures",
          "text": "Review the vendor's breach notification policy. HIPAA requires notification within 60 days of discovery."
        },
        {
          "@type": "HowToStep",
          "position": 6,
          "name": "Evaluate Staff Training Programs",
          "text": "Confirm the vendor provides HIPAA training for all employees with access to PHI and maintains training records."
        },
        {
          "@type": "HowToStep",
          "position": 7,
          "name": "Document Your Evaluation",
          "text": "Maintain records of your vendor evaluation process, including BAA execution, certification verification, and security assessment findings."
        }
      ]
    }
  ]
}
```

---

## Validation Checklist

Before deploying any page with schema:

- [ ] JSON is valid (no syntax errors)
- [ ] All required fields are populated
- [ ] URLs use absolute paths (https://...)
- [ ] Dates are in ISO 8601 format (YYYY-MM-DD)
- [ ] Organization @id is consistent across all pages
- [ ] Breadcrumb URLs match actual page hierarchy
- [ ] FAQ questions are actual questions (not statements)
- [ ] HowTo steps are sequential and actionable
- [ ] Test with Google's Rich Results Test
- [ ] Test with Schema.org Validator

---

## No Technical Dependencies

This implementation requires:
- ✅ Static HTML files
- ✅ JSON-LD script tags
- ✅ No JavaScript frameworks
- ✅ No build tools (optional)
- ✅ No databases
- ✅ No APIs
- ✅ No WordPress
- ✅ No plugins

---

## Maintenance

### When to Update Schema

| Event | Action |
|-------|--------|
| New article published | Add schema following Article pattern |
| Article updated | Update `dateModified` field |
| Site rebranding | Update Organization schema on all pages |
| New service added | Add Service schema to homepage |
| URL structure changes | Update all `@id` and `item` references |

### Annual Review

- [ ] Verify all dates are current
- [ ] Check for broken URLs in schema
- [ ] Update Organization info if changed
- [ ] Add new schema types if content evolves
- [ ] Re-validate all pages

---

## Resources

- **Schema.org Documentation**: https://schema.org/docs/schemas.html
- **Google's Structured Data Guide**: https://developers.google.com/search/docs/appearance/structured-data
- **Rich Results Test**: https://search.google.com/test/rich-results
- **Schema Validator**: https://validator.schema.org/
- **JSON-LD Playground**: https://json-ld.org/playground/

---

## Summary

The MedFlow AEO layer is now implemented with:

1. ✅ **Schema templates** in `/data/schemas/`
2. ✅ **Organization schema** on all major pages
3. ✅ **Article + FAQ + HowTo** on Article #1
4. ✅ **Article + FAQ** on Pillar article
5. ✅ **Service + WebSite** on Homepage
6. ✅ **Ready-to-use template** for Article #2

**No new technical dependencies. No WordPress. Just structured data in static HTML.**
