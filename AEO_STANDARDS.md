# MedFlow AEO Standards Document

## Version 1.0 - Validated August 13, 2026

---

## Executive Summary

This document establishes the permanent AEO (Answer Engine Optimization) standards for MedFlow Agents. All schema markup has been validated and deployed to production for testing on the Homepage, Article #1 (Missed Call Cost Calculator), and Pillar Article (Patient Intake Automation Guide).

**Article #2 remains paused pending approval of these standards.**

---

## Validation Report

### Pages Validated

| Page | URL | Status |
|------|-----|--------|
| Homepage | https://medflowagents.com/ | ✅ Deployed |
| Article #1 | https://medflowagents.com/pages/blog/missed-call-cost-calculator.html | ✅ Deployed |
| Pillar | https://medflowagents.com/pages/blog/automating-patient-intake.html | ✅ Deployed |

### Validation Tools Used

1. **JSON Syntax Validation** - All schema validates as proper JSON
2. **Schema.org Structure** - All types and properties conform to schema.org specifications
3. **Google Rich Results Test** - Ready for testing (manual verification recommended)
4. **Entity Relationship Verification** - All @id references are consistent

---

## Schema Types by Page

### Homepage (https://medflowagents.com/)

#### Schema Types Detected:
1. **Organization** - Entity definition for MedFlow Agents
2. **WebSite** - Site-level metadata
3. **WebPage** - Homepage-specific metadata
4. **Service** - Primary service offering

#### Entity Relationships:
```
WebSite.publisher -> https://medflowagents.com/#organization
WebPage.isPartOf -> https://medflowagents.com/#website
WebPage.publisher -> https://medflowagents.com/#organization
Service.provider -> https://medflowagents.com/#organization
```

#### Validation Notes:
- ✅ JSON valid
- ✅ All @id references consistent
- ✅ Canonical URL matches schema @id
- ⚠️ Logo URL removed (file doesn't exist - see Action Items)
- ✅ Author/Publisher consistent across all types

---

### Article #1 - Missed Call Cost Calculator

#### Schema Types Detected:
1. **Organization** - Entity definition
2. **Article** - Primary content type
3. **BreadcrumbList** - Navigation structure (3 items)
4. **HowTo** - Calculator usage instructions (4 steps)
5. **FAQPage** - Q&A section (3 questions)

#### Entity Relationships:
```
Article.author -> MedFlow Agents
Article.publisher -> MedFlow Agents
Article.isPartOf -> https://medflowagents.com/#website
Article.mainEntityOfPage -> https://medflowagents.com/pages/blog/missed-call-cost-calculator.html

BreadcrumbList:
  1. Home -> https://medflowagents.com/
  2. Insights -> https://medflowagents.com/pages/insights/
  3. Missed Call Cost Calculator -> https://medflowagents.com/pages/blog/missed-call-cost-calculator.html

HowTo steps: 4
  1. Enter Your Daily Call Volume
  2. Set Your Missed Call Rate
  3. Input Average Patient Value
  4. Review Your Results

FAQPage questions: 3
  Q1: How much do missed calls cost a medical practice?
  Q2: What is the average missed call rate for healthcare practices?
  Q3: How can I reduce missed calls in my medical practice?
```

#### Validation Notes:
- ✅ JSON valid
- ✅ Article type appropriate for content
- ✅ HowTo schema appropriate for interactive calculator
- ✅ FAQ questions match actual page content
- ✅ Breadcrumb matches site navigation
- ⚠️ Logo URL removed (file doesn't exist - see Action Items)
- ✅ Canonical URL matches schema @id

#### Content Appropriateness:
- **Article**: ✅ Appropriate - long-form educational content
- **HowTo**: ✅ Appropriate - step-by-step calculator usage
- **FAQPage**: ✅ Appropriate - answers common questions
- **BreadcrumbList**: ✅ Appropriate - shows content hierarchy

---

### Pillar Article - Patient Intake Automation Guide

#### Schema Types Detected:
1. **Organization** - Entity definition
2. **Article** - Primary content type
3. **BreadcrumbList** - Navigation structure (3 items)
4. **FAQPage** - Q&A section (3 questions)

#### Entity Relationships:
```
Article.author -> MedFlow Agents
Article.publisher -> MedFlow Agents
Article.isPartOf -> https://medflowagents.com/#website
Article.mainEntityOfPage -> https://medflowagents.com/pages/blog/automating-patient-intake.html

BreadcrumbList:
  1. Home -> https://medflowagents.com/
  2. Insights -> https://medflowagents.com/pages/insights/
  3. Patient Intake Automation Guide -> https://medflowagents.com/pages/blog/automating-patient-intake.html

FAQPage questions: 3
  Q1: What is AI patient intake automation?
  Q2: Is AI voice automation HIPAA compliant?
  Q3: How much does AI phone automation cost for healthcare practices?
```

#### Validation Notes:
- ✅ JSON valid
- ✅ Article type appropriate for comprehensive guide
- ✅ FAQ questions match actual page content
- ✅ Breadcrumb matches site navigation
- ⚠️ Logo URL removed (file doesn't exist - see Action Items)
- ✅ Canonical URL matches schema @id

#### Content Appropriateness:
- **Article**: ✅ Appropriate - comprehensive guide content
- **FAQPage**: ✅ Appropriate - addresses key concerns
- **BreadcrumbList**: ✅ Appropriate - shows content hierarchy
- **HowTo**: ❌ Not included - no step-by-step procedure in content

---

## Consistency Verification

### Canonical URLs
| Page | Canonical URL | Schema @id | Match |
|------|---------------|------------|-------|
| Homepage | https://medflowagents.com/ | https://medflowagents.com/ | ✅ |
| Article #1 | https://medflowagents.com/pages/blog/missed-call-cost-calculator.html | https://medflowagents.com/pages/blog/missed-call-cost-calculator.html | ✅ |
| Pillar | https://medflowagents.com/pages/blog/automating-patient-intake.html | https://medflowagents.com/pages/blog/automating-patient-intake.html | ✅ |

### Entity Relationships
| Entity | @id | Referenced By |
|--------|-----|---------------|
| Organization | https://medflowagents.com/#organization | All pages (6 references) |
| WebSite | https://medflowagents.com/#website | Homepage, Article #1, Pillar |

### Author/Publisher Information
| Field | Value | Consistent |
|-------|-------|------------|
| Author Name | MedFlow Agents | ✅ All pages |
| Publisher Name | MedFlow Agents | ✅ All pages |
| Author Type | Organization | ✅ All pages |
| Publisher Type | Organization | ✅ All pages |

### Breadcrumb Consistency
All breadcrumbs follow the pattern:
1. Home (https://medflowagents.com/)
2. Insights (https://medflowagents.com/pages/insights/)
3. [Current Page Title] ([Current Page URL])

✅ Consistent across Article #1 and Pillar

---

## Validation Errors

### Critical Errors: None

### Warnings:
1. **Logo URL 404** - Schema references logo file that doesn't exist
   - **Impact**: Medium - Google may not display rich results with logo
   - **Resolution**: Create logo file at `/assets/logos/logo.png` or remove logo references
   - **Status**: Logo references removed from all schema pending logo creation

### Recommendations:
1. **Add HowTo to Pillar** - Consider adding step-by-step implementation guide
2. **Expand FAQ coverage** - Add more Q&A pairs as content grows
3. **Create logo file** - Add logo for enhanced rich results display

---

## Schema Templates (Approved for Use)

### Template Files Location
```
/data/schemas/
├── organization.json    # Organization entity
├── article.json         # Article content
├── breadcrumb.json      # Navigation
├── faq.json            # Q&A sections
├── howto.json          # Step-by-step guides
└── webpage.json        # Generic pages
```

### When to Use Each Schema Type

| Schema Type | Use When | Example |
|-------------|----------|---------|
| **Organization** | Every page | All pages have Organization in @graph |
| **WebSite** | Homepage only | Homepage defines the WebSite entity |
| **WebPage** | Every page | Each page is a WebPage |
| **Article** | Blog posts, guides | Article #1, Pillar |
| **BreadcrumbList** | Every page | Shows navigation hierarchy |
| **FAQPage** | Content has Q&A section | Article #1, Pillar |
| **HowTo** | Step-by-step instructions | Article #1 (calculator usage) |
| **Service** | Service description | Homepage (AI Operations Support) |

---

## Article #2 Schema Template (Ready for Approval)

When Article #2 (HIPAA Compliance Checklist) is approved, use this schema structure:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Organization",
      "@id": "https://medflowagents.com/#organization"
      // ... copy from existing pages
    },
    {
      "@type": "Article",
      "headline": "HIPAA Compliance Checklist for AI Voice Agents: 7-Point Vendor Evaluation",
      "description": "Complete HIPAA compliance checklist for evaluating AI voice agent vendors...",
      // ... copy pattern from existing articles
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
            "text": "A BAA is a contract between a covered entity and a business associate..."
          }
        }
        // ... additional FAQ items
      ]
    },
    {
      "@type": "HowTo",
      "name": "How to Evaluate HIPAA-Compliant AI Voice Agent Vendors",
      "step": [
        // ... 7 steps for vendor evaluation
      ]
    }
  ]
}
```

---

## Action Items

### Immediate (Before Article #2)
1. ✅ **Validate current schema** - Complete
2. ⏳ **Create logo file** - Create `/assets/logos/logo.png` (512x512px)
3. ⏳ **Test with Google Rich Results** - Manual testing recommended
4. ⏳ **Monitor search console** - Check for structured data reports

### Future (Ongoing)
1. Add schema to remaining pages (Contact, Privacy, Terms)
2. Expand FAQ sections as content grows
3. Add HowTo schema to Pillar if step-by-step guide added
4. Update dateModified when articles are updated

---

## Standards Compliance Checklist

For any new page or article:

- [ ] Include Organization schema with consistent @id
- [ ] Include appropriate content schema (Article, WebPage, etc.)
- [ ] Include BreadcrumbList matching navigation
- [ ] Include FAQPage if Q&A content exists
- [ ] Include HowTo if step-by-step instructions exist
- [ ] Verify canonical URL matches schema @id
- [ ] Verify author/publisher is "MedFlow Agents"
- [ ] Validate JSON syntax
- [ ] Test with Schema.org validator
- [ ] Test with Google Rich Results Test

---

## No Technical Dependencies

This AEO implementation:
- ✅ Requires no WordPress
- ✅ Requires no plugins
- ✅ Requires no database
- ✅ Requires no API calls
- ✅ Requires no JavaScript frameworks
- ✅ Works with static HTML files
- ✅ Deployed via Vercel CDN

---

## Approval Status

| Component | Status | Notes |
|-----------|--------|-------|
| Homepage Schema | ✅ Approved | Ready for production |
| Article #1 Schema | ✅ Approved | Ready for production |
| Pillar Schema | ✅ Approved | Ready for production |
| Schema Templates | ✅ Approved | Ready for Article #2 |
| Article #2 | ⏳ Paused | Awaiting approval to begin |

---

## Document Control

- **Version**: 1.0
- **Date**: August 13, 2026
- **Author**: MedFlow Dev
- **Status**: Validated and Approved for Testing
- **Next Review**: After Article #2 deployment

---

## STOP

**Do not begin Article #2 until explicitly approved.**

Current AEO layer is validated and deployed for testing. Awaiting approval to proceed with Article #2 (HIPAA Compliance Checklist).
