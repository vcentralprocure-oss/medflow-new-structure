# HIPAA Compliance Checklist for AI Voice Agents

## 7-Point Vendor Evaluation Checklist

Use this checklist when evaluating AI voice agent vendors for your healthcare practice. Each item is essential for HIPAA compliance.

---

### ☐ 1. Business Associate Agreement (BAA) Willingness
**Critical:** Vendor must sign a BAA without hesitation.

**What to ask:**
- "Will you sign a Business Associate Agreement?"
- "Can you provide your standard BAA template?"
- "Are there any exclusions or limitations in your BAA?"

**Red flags:**
- Hesitation or delay in providing BAA
- Refusal to sign
- Generic "terms of service" instead of proper BAA
- Exclusions for AI/ML training data

**BAA must include:**
- AI model training restrictions
- Data deletion timelines (specify days)
- Breach notification timeframes (24-48 hours)
- Permitted uses and disclosures of PHI
- Subcontractor management provisions

---

### ☐ 2. End-to-End Encryption
**Critical:** All PHI must be encrypted in transit and at rest.

**Required standards:**
- **In Transit:** TLS 1.3 (minimum TLS 1.2)
- **At Rest:** AES-256 encryption
- **Voice Data:** Encrypted call recordings and transcriptions
- **Key Management:** Proper key rotation and secure storage

**What to ask:**
- "What encryption standards do you use for data in transit?"
- "How is data encrypted at rest?"
- "Who manages the encryption keys?"
- "Do you have encryption certifications?"

**Documentation to request:**
- Security architecture documentation
- Encryption implementation details
- Third-party security audit reports

---

### ☐ 3. Audit Logging & Access Controls
**Critical:** You must track all access to PHI.

**Required capabilities:**
- Unique user identification for all system access
- Automatic logoff after inactivity (15 minutes max)
- Role-based access controls (RBAC)
- Immutable audit logs

**Audit logs must capture:**
- User ID
- Timestamp (date and time)
- Action performed
- Data accessed or modified
- Source IP address

**What to ask:**
- "Can you provide detailed audit logs of all PHI access?"
- "How long are logs retained?"
- "Can logs be exported for our review?"
- "Do you support role-based access controls?"

---

### ☐ 4. Data Storage Location & Retention
**Critical:** Know where your PHI lives.

**Requirements:**
- US-based data centers (or EU/adequacy decision countries)
- No storage in prohibited countries (China, Russia, etc.)
- Clear data retention policies
- Secure deletion procedures

**What to ask:**
- "Where are your data centers located?"
- "Do you store or process data outside the US?"
- "What is your data retention policy?"
- "How is data deleted at end of retention?"
- "Do you have disaster recovery sites? Where?"

**Get in writing:**
- Data center locations
- Backup and redundancy locations
- Data retention periods
- Deletion certification process

---

### ☐ 5. AI Model Training Data Policies
**Critical:** Your patient data must NEVER train AI models.

**Requirements:**
- Explicit prohibition on using your data for AI training
- No data aggregation across customers
- Written confirmation in BAA or DPA
- Ability to opt out of improvement programs

**What to ask:**
- "Is our patient data used to train your AI models?"
- "Do you aggregate data across customers?"
- "Can we opt out of any data usage for model improvement?"
- "Will you put training restrictions in the BAA?"

**Red flags:**
- "We use anonymized data" (anonymization is hard to guarantee)
- "Industry standard practices" (vague)
- Opt-out rather than opt-in
- Refusal to put restrictions in writing

**Get this exact language in your BAA:**
> "Vendor shall not use, process, or incorporate Customer's PHI or any derivative thereof for the purpose of training, fine-tuning, or improving Vendor's artificial intelligence or machine learning models."

---

### ☐ 6. Breach Notification Procedures
**Critical:** Fast notification is essential for compliance.

**Requirements:**
- 24-48 hour notification of suspected breaches
- Clear escalation procedures
- Detailed incident reports
- Remediation plans

**What to ask:**
- "What is your breach notification timeframe?"
- "Who is our point of contact for security incidents?"
- "What information will you provide in a breach notification?"
- "Do you have cyber insurance?"

**BAA should specify:**
- Notification timeframe (aim for 24 hours)
- Method of notification (phone + email)
- Information to be included in notification
- Vendor's responsibility for breach remediation costs

---

### ☐ 7. Third-Party Security Certifications
**Critical:** Independent validation of security claims.

**Certifications to look for:**

| Certification | Priority | What It Validates |
|--------------|----------|-------------------|
| SOC 2 Type II | Essential | Security, availability, confidentiality controls |
| HITRUST CSF | Gold Standard | Healthcare-specific security framework |
| ISO 27001 | Strong | Information security management |
| HIPAA Seal | Table Stakes | Self-reported HIPAA compliance |

**What to ask:**
- "What security certifications do you hold?"
- "Can you provide your latest SOC 2 report?"
- "When was your last security audit?"
- "Who performed the audit?"

**Request documentation:**
- SOC 2 Type II report (within last 12 months)
- HITRUST CSF certification (if claimed)
- Penetration test results
- Vulnerability scan reports

---

## Red Flags: When to Walk Away

**Immediate disqualifiers:**
- ☐ Refusal to sign BAA
- ☐ Storing PHI outside US without safeguards
- ☐ Using consumer AI models (ChatGPT, Claude, Gemini standard tiers)
- ☐ No audit logging capabilities
- ☐ Vague answers about AI training data
- ☐ Missing all security certifications
- ☐ Price significantly below market (compliance costs money)

**Warning signs:**
- ☐ "Bank-level security" without specifics
- ☐ Pressure to sign quickly
- ☐ No healthcare-specific experience
- ☐ Can't provide compliance documentation
- ☐ Recent data breaches (check news)

---

## BAA Negotiation Tips

### Before you start:
1. Have your healthcare attorney review the BAA
2. Know your state's specific requirements
3. Prepare a list of non-negotiables

### Key provisions to negotiate:

**AI Training Restrictions**
```
Vendor shall not use Customer's PHI for AI/ML model training,
fine-tuning, or algorithm improvement without explicit written consent.
```

**Data Deletion Timeline**
```
Vendor shall permanently delete all Customer PHI within 30 days
of contract termination or upon Customer's written request.
```

**Breach Notification**
```
Vendor shall notify Customer within 24 hours of discovering
any suspected breach of PHI.
```

**Indemnification**
```
Vendor shall indemnify Customer for all costs, fines, and penalties
resulting from Vendor's breach of HIPAA or this Agreement.
```

---

## Cost Expectations

HIPAA compliance adds 20-40% to base pricing:

| Practice Size | Monthly Cost Range | Notes |
|--------------|-------------------|-------|
| Small (1-5 providers) | $200-500 | Basic features, limited call volume |
| Medium (6-20 providers) | $500-1,500 | Full features, moderate volume |
| Large (21+ providers) | $1,500-3,000+ | Enterprise features, high volume |

**Factors affecting cost:**
- Call volume
- Number of phone lines
- Features (scheduling, intake, follow-up)
- Integration requirements
- Support level

---

## Next Steps

1. **Print this checklist** and use it during vendor demos
2. **Request documentation** for all 7 points
3. **Involve your compliance officer** in the evaluation
4. **Have your attorney review** the BAA before signing
5. **Schedule annual reviews** of vendor compliance

---

## Resources

- [HHS HIPAA Guidance](https://www.hhs.gov/hipaa/for-professionals/index.html)
- [HIPAA Security Rule](https://www.hhs.gov/hipaa/for-professionals/security/index.html)
- [Business Associate Agreements](https://www.hhs.gov/hipaa/for-professionals/covered-entities/sample-business-associate-agreement-provisions/index.html)

---

*This checklist is for informational purposes and does not constitute legal advice. Consult with a healthcare attorney for guidance specific to your practice.*

**Document Version:** 1.0  
**Last Updated:** August 18, 2026  
**Source:** MedFlow Agents - https://medflowagents.com