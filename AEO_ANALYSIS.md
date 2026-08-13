# AI Booster Plugin - Reverse Engineering Analysis

## Executive Summary

The AI Booster WordPress plugin is an **AEO (Answer Engine Optimization)** tool that generates JSON-LD schema markup to improve visibility in AI-powered search results. This analysis extracts the methodology and translates it into MedFlow's static HTML/Vercel architecture.

---

## 1. What Schema It Actually Generates

### Core Schema Types (Fetched from SerpSling API)

The plugin fetches schema type definitions from `api.serpsling.com/api/schema/types` and supports:

| Schema Type | Purpose | AEO Relevance |
|-------------|---------|---------------|
| **Article** | Blog posts, news articles | HIGH - Core content markup |
| **BlogPosting** | Individual blog posts | HIGH - Specific article type |
| **WebPage** | Generic pages | MEDIUM - Basic page context |
| **Organization** | Company/brand info | HIGH - Entity recognition |
| **LocalBusiness** | Physical business locations | HIGH - Local AI search |
| **FAQPage** | FAQ sections | VERY HIGH - Direct answers |
| **HowTo** | Step-by-step guides | VERY HIGH - Procedure markup |
| **Service** | Service offerings | HIGH - Service discovery |
| **Product** | Products (if applicable) | MEDIUM - Not primary for MedFlow |
| **BreadcrumbList** | Navigation breadcrumbs | HIGH - Site structure |
| **VideoObject** | Video content | MEDIUM - Future consideration |
| **ImageObject** | Image metadata | LOW - Secondary |

### Schema Structure Pattern

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Article Title",
  "description": "Meta description",
  "author": {
    "@type": "Organization",
    "name": "MedFlow Agents"
  },
  "publisher": {
    "@type": "Organization",
    "name": "MedFlow Agents",
    "logo": {
      "@type": "ImageObject",
      "url": "https://medflowagents.com/assets/logos/logo.png"
    }
  },
  "datePublished": "2026-08-13",
  "dateModified": "2026-08-13",
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://medflowagents.com/pages/blog/article.html"
  }
}
```

---

## 2. AEO/LLM-Relevant Parts

### HIGH PRIORITY (Critical for AI Search)

#### 2.1 Entity Recognition Schema
```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Organization",
      "@id": "https://medflowagents.com/#organization",
      "name": "MedFlow Agents",
      "url": "https://medflowagents.com",
      "logo": "https://medflowagents.com/assets/logo.png",
      "sameAs": [
        "https://linkedin.com/company/medflowagents"
      ]
    }
  ]
}
```

**Why it matters:** LLMs use entity recognition to understand WHO is providing the information. This establishes authority and trust.

#### 2.2 Article with Author & Publisher
```json
{
  "@type": "Article",
  "author": {
    "@type": "Organization",
    "name": "MedFlow Agents"
  },
  "publisher": {
    "@type": "Organization",
    "name": "MedFlow Agents"
  }
}
```

**Why it matters:** Clear authorship signals expertise and accountability to AI systems.

#### 2.3 FAQPage Schema (Very High Impact)
```json
{
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "How much do missed calls cost a medical practice?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Missed calls cost medical practices $125-200 per call..."
      }
    }
  ]
}
```

**Why it matters:** Direct Q&A format is EXACTLY how AI assistants answer user queries. This schema type has the highest probability of being used for featured snippets and AI answers.

#### 2.4 HowTo Schema (Very High Impact)
```json
{
  "@type": "HowTo",
  "name": "How to Calculate Missed Call Costs",
  "step": [
    {
      "@type": "HowToStep",
      "name": "Enter daily call volume",
      "text": "Input your average daily inbound calls..."
    }
  ]
}
```

**Why it matters:** Step-by-step procedures are prime content for AI assistants helping users complete tasks.

#### 2.5 BreadcrumbList Schema
```json
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
    }
  ]
}
```

**Why it matters:** Helps AI understand site structure and content hierarchy.

### MEDIUM PRIORITY (Supporting Context)

#### 2.6 WebPage Schema
- Provides basic page context
- Links to main entity
- Establishes page purpose

#### 2.7 LocalBusiness Schema
- Important if MedFlow targets specific geographic markets
- Helps with "near me" AI queries

### LOW PRIORITY (Nice to Have)

#### 2.8 VideoObject / ImageObject
- Only if rich media is primary content
- Secondary for text-heavy medical content

---

## 3. WordPress-Only Parts to Discard

### 3.1 Database/Post System
```php
// DISCARD - WordPress CPT (Custom Post Type) system
get_post( $schema_id )
get_post_meta( $schema_id, '_ai_booster_schema_type', true )
```

**MedFlow Alternative:** Static JSON-LD in HTML files, updated at build time.

### 3.2 Admin UI
```php
// DISCARD - WordPress admin interface
admin/partials/schema-edit.php
admin/partials/rules-list.php
```

**MedFlow Alternative:** No admin UI needed. Schema is hand-crafted or generated at build time.

### 3.3 Transient Caching
```php
// DISCARD - WordPress transient system
get_transient( $cache_key )
set_transient( $cache_key, $schemas, self::CACHE_TTL )
```

**MedFlow Alternative:** Static files are inherently cached by CDN. No dynamic caching needed.

### 3.4 Rule Engine
```php
// DISCARD - Complex rule matching system
AI_Booster_Rule_Matcher::get_schemas_for_post( $post_id )
```

**MedFlow Alternative:** Direct schema inclusion in each HTML file. No runtime matching.

### 3.5 API License Check
```php
// DISCARD - SerpSling API dependency
$license->is_valid()
AI_Booster_API::authenticated_request()
```

**MedFlow Alternative:** Self-hosted schema definitions. No external API dependency.

### 3.6 WordPress Hooks
```php
// DISCARD - WordPress action/filter system
add_action( 'wp_head', array( $this, 'output_schemas' ), 1 )
```

**MedFlow Alternative:** Direct `<script>` tags in HTML `<head>`.

### 3.7 Context Resolution
```php
// DISCARD - WordPress-specific URL resolution
is_front_page()
is_singular()
get_queried_object_id()
```

**MedFlow Alternative:** Hardcoded page types in static files.

---

## 4. What Can Be Reproduced in MedFlow's Architecture

### 4.1 Static JSON-LD Injection

**WordPress Way:**
```php
add_action( 'wp_head', function() {
    echo '<script type="application/ld+json">' . $schema . '</script>';
});
```

**MedFlow Way:**
```html
<!DOCTYPE html>
<html>
<head>
    <script type="application/ld+json">
    {
      "@context": "https://schema.org",
      "@type": "Article",
      "headline": "..."
    }
    </script>
</head>
```

### 4.2 Schema Templates

Create reusable schema templates as HTML comments or separate JSON files:

```html
<!-- Schema: Article -->
<script type="application/ld+json" id="schema-article">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "{{TITLE}}",
  "description": "{{DESCRIPTION}}",
  "author": {
    "@type": "Organization",
    "name": "MedFlow Agents"
  },
  "publisher": {
    "@type": "Organization",
    "name": "MedFlow Agents",
    "logo": {
      "@type": "ImageObject",
      "url": "https://medflowagents.com/assets/logos/logo.png"
    }
  },
  "datePublished": "{{DATE_PUBLISHED}}",
  "dateModified": "{{DATE_MODIFIED}}",
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "{{CANONICAL_URL}}"
  }
}
</script>
```

### 4.3 Build-Time Schema Generation

Use a simple build script or manual process to inject schemas:

```javascript
// build-schema.js - Run at build time
const fs = require('fs');
const path = require('path');

const articleTemplate = JSON.parse(fs.readFileSync('schemas/article.json', 'utf8'));

function injectSchema(htmlFile, schemaData) {
    let html = fs.readFileSync(htmlFile, 'utf8');
    const schema = { ...articleTemplate, ...schemaData };
    const schemaScript = `<script type="application/ld+json">${JSON.stringify(schema, null, 2)}</script>`;
    
    // Inject before </head>
    html = html.replace('</head>', schemaScript + '\n</head>');
    fs.writeFileSync(htmlFile, html);
}
```

### 4.4 Manual Schema Management

For MedFlow's scale (6 pages, growing to ~12), manual schema management is practical:

1. Create schema templates in `/data/schemas/`
2. Copy template to each HTML file
3. Customize per-page fields (title, description, dates)
4. Validate with Google's Rich Results Test

---

## 5. Instructions for Building MedFlow AEO Layer

### 5.1 Create Schema Template Files

Create `/data/schemas/` directory with:

```
/data/schemas/
├── organization.json       # Site-wide entity
├── article.json            # Blog posts
├── breadcrumb.json         # Navigation
├── faq.json                # FAQ sections
├── howto.json              # Step-by-step guides
├── webpage.json            # Generic pages
└── service.json            # Service descriptions
```

### 5.2 Organization Schema (Site-Wide)

**File:** `/data/schemas/organization.json`

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "@id": "https://medflowagents.com/#organization",
  "name": "MedFlow Agents",
  "alternateName": "Vidahub Products",
  "url": "https://medflowagents.com",
  "logo": {
    "@type": "ImageObject",
    "url": "https://medflowagents.com/assets/logos/logo.png",
    "width": 512,
    "height": 512
  },
  "description": "AI Operations Support for Home Health, Senior Living & Urgent Care",
  "sameAs": [
    "https://linkedin.com/company/medflowagents"
  ],
  "contactPoint": {
    "@type": "ContactPoint",
    "telephone": "+1-972-433-5696",
    "contactType": "customer service",
    "availableLanguage": "English"
  }
}
```

### 5.3 Article Schema Template

**File:** `/data/schemas/article.json`

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "{{TITLE}}",
  "description": "{{DESCRIPTION}}",
  "image": "{{IMAGE_URL}}",
  "author": {
    "@type": "Organization",
    "name": "MedFlow Agents",
    "url": "https://medflowagents.com"
  },
  "publisher": {
    "@type": "Organization",
    "name": "MedFlow Agents",
    "logo": {
      "@type": "ImageObject",
      "url": "https://medflowagents.com/assets/logos/logo.png"
    }
  },
  "datePublished": "{{DATE_PUBLISHED}}",
  "dateModified": "{{DATE_MODIFIED}}",
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "{{CANONICAL_URL}}"
  },
  "isPartOf": {
    "@type": "WebSite",
    "@id": "https://medflowagents.com/#website",
    "name": "MedFlow Agents",
    "url": "https://medflowagents.com"
  }
}
```

### 5.4 FAQ Schema Template

**File:** `/data/schemas/faq.json`

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "{{QUESTION_1}}",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "{{ANSWER_1}}"
      }
    }
  ]
}
```

### 5.5 Breadcrumb Schema Template

**File:** `/data/schemas/breadcrumb.json`

```json
{
  "@context": "https://schema.org",
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
      "name": "{{PARENT_NAME}}",
      "item": "{{PARENT_URL}}"
    },
    {
      "@type": "ListItem",
      "position": 3,
      "name": "{{CURRENT_NAME}}",
      "item": "{{CURRENT_URL}}"
    }
  ]
}
```

---

## 6. Applying to Article #1 and Article #2

### 6.1 Article #1: Missed Call Cost Calculator

**Current Schema:** Basic Article + BreadcrumbList

**Enhanced Schema Should Include:**

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Organization",
      "@id": "https://medflowagents.com/#organization"
      // ... organization details
    },
    {
      "@type": "Article",
      "headline": "Missed Call Cost Calculator...",
      // ... article details
    },
    {
      "@type": "BreadcrumbList",
      // ... breadcrumbs
    },
    {
      "@type": "HowTo",
      "name": "How to Calculate Missed Call Costs",
      "description": "Step-by-step guide to calculating revenue loss from missed calls",
      "totalTime": "PT5M",
      "estimatedCost": {
        "@type": "MonetaryAmount",
        "currency": "USD",
        "value": "0"
      },
      "tool": [
        {
          "@type": "HowToTool",
          "name": "Missed Call Cost Calculator"
        }
      ],
      "step": [
        {
          "@type": "HowToStep",
          "position": 1,
          "name": "Enter Daily Call Volume",
          "text": "Input your average daily inbound calls",
          "url": "https://medflowagents.com/pages/blog/missed-call-cost-calculator.html#dailyCalls"
        },
        {
          "@type": "HowToStep",
          "position": 2,
          "name": "Set Missed Call Rate",
          "text": "Enter your percentage of missed calls (industry average is 32-34%)",
          "url": "https://medflowagents.com/pages/blog/missed-call-cost-calculator.html#missedRate"
        }
        // ... additional steps
      ]
    }
  ]
}
```

### 6.2 Article #2: HIPAA Compliance Checklist (Future)

**Recommended Schema:**

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Organization",
      "@id": "https://medflowagents.com/#organization"
    },
    {
      "@type": "Article",
      "headline": "HIPAA Compliance Checklist for AI Voice Agents",
      // ... article details
    },
    {
      "@type": "BreadcrumbList",
      // ... breadcrumbs
    },
    {
      "@type": "FAQPage",
      "mainEntity": [
        {
          "@type": "Question",
          "name": "What is a Business Associate Agreement (BAA)?",
          "acceptedAnswer": {
            "@type": "Answer",
            "text": "A BAA is a contract between a covered entity and a business associate that establishes the permitted uses and disclosures of protected health information (PHI)..."
          }
        }
        // ... additional FAQ items
      ]
    },
    {
      "@type": "HowTo",
      "name": "How to Evaluate HIPAA-Compliant AI Vendors",
      "step": [
        {
          "@type": "HowToStep",
          "position": 1,
          "name": "Verify BAA Willingness",
          "text": "Confirm the vendor will sign a Business Associate Agreement"
        }
        // ... additional steps
      ]
    }
  ]
}
```

---

## 7. Implementation Checklist

### Phase 1: Foundation (Immediate)
- [ ] Create `/data/schemas/` directory
- [ ] Create `organization.json` with MedFlow entity
- [ ] Add Organization schema to all pages
- [ ] Validate with Google's Rich Results Test

### Phase 2: Article Enhancement (Before Article #2)
- [ ] Enhance Article #1 with HowTo schema
- [ ] Add FAQ schema to Article #1 (extract from content)
- [ ] Create schema templates for future articles
- [ ] Document schema injection process

### Phase 3: Article #2 (When Approved)
- [ ] Create Article #2 with full schema stack
- [ ] Include FAQPage schema for common HIPAA questions
- [ ] Include HowTo schema for vendor evaluation process
- [ ] Cross-link schemas between Article #1 and Article #2

---

## 8. No Technical Dependencies Created

### What We're NOT Adding:
- ❌ WordPress plugin
- ❌ Database
- ❌ Admin interface
- ❌ API calls to SerpSling
- ❌ Dynamic schema generation
- ❌ Complex rule engine
- ❌ Caching system
- ❌ JavaScript frameworks

### What We ARE Adding:
- ✅ Static JSON-LD in HTML
- ✅ Schema templates in `/data/schemas/`
- ✅ Manual customization per page
- ✅ Build-time validation (optional)

---

## 9. Validation Tools

### Google's Rich Results Test
https://search.google.com/test/rich-results

### Schema.org Validator
https://validator.schema.org/

### JSON-LD Playground
https://json-ld.org/playground/

---

## 10. Summary

The AI Booster plugin's core value is its **schema methodology**, not its WordPress infrastructure. The AEO-relevant parts are:

1. **Entity Recognition** (Organization schema)
2. **Content Structure** (Article, HowTo, FAQ schemas)
3. **Site Architecture** (BreadcrumbList schema)
4. **Authority Signals** (Author, Publisher markup)

All of this can be implemented in MedFlow's static architecture by:
- Creating schema templates
- Injecting JSON-LD into HTML files
- Validating with Google's tools
- Maintaining manually (practical for ~12 pages)

**No new technical dependencies. No WordPress. No plugins. Just structured data in static HTML.**
