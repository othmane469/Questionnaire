# K-NET Architecture Discovery Questionnaire

**Purpose:** This document will help define the technical architecture and constraints for K-NET by capturing business requirements, technical constraints, and strategic decisions.

**Instructions:** Fill in your answers below each question. Use as much detail as possible - even "I don't know yet" is valuable information.

**Date Started:** [FILL IN]
**Last Updated:** [FILL IN]
**Version:** 1.1

---

## Table of Contents

1. [Business & Customer Context](#a-business--customer-context)
2. [Technical Constraints](#b-technical-constraints)
3. [Device & Integration Landscape](#c-device--integration-landscape)
4. [Financial & Risk Model](#d-financial--risk-model)
5. [Scale & Performance](#e-scale--performance)
6. [Team & Resources](#f-team--resources)
7. [Security & Trust](#g-security--trust)
8. [Competitive Differentiation](#h-competitive-differentiation)
9. [Strategic Questions](#i-strategic-questions)
10. [Priority Definitions](#j-priority-definitions)
11. [User Experience & Interface](#k-user-experience--interface)
12. [Reporting & Analytics](#l-reporting--analytics)
13. [Training & Onboarding](#m-training--onboarding)
14. [Environmental & Physical Factors](#n-environmental--physical-factors)
15. [Customer Lifecycle Management](#o-customer-lifecycle-management)
16. [Testing & Quality Assurance](#p-testing--quality-assurance)
17. [Disaster Recovery & Business Continuity](#q-disaster-recovery--business-continuity)
18. [Localization & Language Support](#r-localization--language-support)
19. [Third-Party Developer Access](#s-third-party-developer-access)

---

## A. Business & Customer Context

### A1. Target Users

**Question:** Who are the PRIMARY users of K-NET in order of priority?

**Your Answer:**
```
Priority 1: [FILL IN - e.g., KardaTech internal operations team]
Priority 2: [FILL IN - e.g., Partner installers (licensees)]
Priority 3: [FILL IN - e.g., End customers (businesses with solar)]
Priority 4: [FILL IN - e.g., Banks/Investors]
Priority 5: [FILL IN - e.g., ONEE/ANRE (regulatory reporting)]
```

**Question:** For each primary user, what is their #1 daily pain point that K-NET solves?

**Your Answer:**
> **Priority 1 User ([FILL IN]):**
> [FILL IN - Describe their main pain point]
>
> **Priority 2 User ([FILL IN]):**
> [FILL IN - Describe their main pain point]
>
> **Priority 3 User ([FILL IN]):**
> [FILL IN - Describe their main pain point]

---

### A2. Revenue Model

**Question:** How do you make money from K-NET?

**Options:**
- [ ] One-time license fee
- [ ] Monthly SaaS subscription
- [ ] Per-transaction fee
- [ ] % of financed projects
- [ ] Other: [FILL IN]

**Your Answer:**
```
Primary Revenue Model: [FILL IN]

Secondary Revenue Streams: [FILL IN]

Pricing Structure (if known): [FILL IN]
```

**Notes:** _This affects multi-tenancy design, usage metrics we need to track, and billing integration requirements._

---

### A3. Data Ownership

**Question:** Who owns the data in K-NET when licensed to an installer?

**Your Answer:**
```
Choose one:
[ ] KardaTech owns everything
[ ] Each installer owns their data
[ ] Customer owns their data
[ ] Hybrid - explain: [FILL IN]
```

**Additional Details:**
```
Can KardaTech use aggregated data for: [FILL IN]
- Benchmarking? [YES/NO]
- Product improvement? [YES/NO]
- Selling insights? [YES/NO]
- Marketing? [YES/NO]
```

**Notes:** _This affects database architecture, privacy model, compliance requirements, and what data you can monetize._

---

## B. Technical Constraints

### B1. Real-Time Requirements

**Question:** What does "real-time" mean for K-NET in different scenarios?

**Your Answer:**

| Scenario | Latency Tolerance | Is Critical? | Business Impact if Missed |
|----------|-------------------|-------------|--------------------------|
| Dashboard refresh for customer | [FILL IN - e.g., < 5 seconds] | [YES/NO] | [FILL IN] |
| Detecting inverter failure | [FILL IN - e.g., < 1 minute] | [YES/NO] | [FILL IN] |
| Billing calculation | [FILL IN - e.g., Can wait until EOD] | [YES/NO] | [FILL IN] |
| Bank reporting | [FILL IN - e.g., Can wait days] | [YES/NO] | [FILL IN] |
| Grid signals (future V2G) | [FILL IN] | [YES/NO] | [FILL IN] |

**Additional Context:**
```
[FILL IN - Any other real-time scenarios not listed above]
```

---

### B2. Control vs. Visibility

**Question:** Can K-NET send commands to devices, or just read data?

**Your Answer:**

| Capability | Timeline | Priority |
|------------|----------|----------|
| Read production data | [NOW / FUTURE / NEVER] | [HIGH / MED / LOW] |
| Send curtailment commands | [NOW / FUTURE / NEVER] | [HIGH / MED / LOW] |
| Dispatch batteries | [NOW / FUTURE / NEVER] | [HIGH / MED / LOW] |
| Control EV chargers | [NOW / FUTURE / NEVER] | [HIGH / MED / LOW] |
| Disconnect assets remotely | [NOW / FUTURE / NEVER] | [HIGH / MED / LOW] |

**Risk Assessment:**
```
What happens if K-NET sends a wrong command?
[FILL IN - Describe liability, safety concerns, etc.]
```

**Notes:** _Control capabilities dramatically increase security complexity and liability exposure._

---

### B3. Offline Scenarios

**Question:** What happens when a site loses internet connectivity?

**Your Answer:**

```
How long can a site be offline before it's a problem?
[FILL IN - e.g., 4 hours, 1 day, 1 week]

Should devices buffer data locally?
[YES / NO / MAYBE - If yes, for how long?]

Do you need edge computing (local processing)?
[YES / NO / MAYBE - If yes, what processing?]

What happens if offline during billing period?
[FILL IN - e.g., Prorate? Estimate? Catch up later?]
```

**Technical Considerations:**
```
[FILL IN - Any concerns about local storage at customer sites?]
[FILL IN - What about security of offline data?]
```

---

## C. Device & Integration Landscape

### C1. Hardware Ecosystem

**Question:** What devices does K-NET need to integrate with TODAY?

**Your Answer:**

**Inverters:**
```
Brands/Models in Morocco:
- [FILL IN - e.g., Huawei SUN2000 series]
- [FILL IN]
- [FILL IN]

Protocols/APIs:
- [FILL IN - e.g., Modbus RTU over RS485]
- [FILL IN - e.g., proprietary HTTP API]
- [FILL IN]
```

**Smart Meters:**
```
Brands/Models:
- [FILL IN - e.g., Schlumberger]
- [FILL IN]

Protocols:
- [FILL IN - e.g., Pulse output]
- [FILL IN - e.g., Modbus]
- [FILL IN]
```

**Communication Infrastructure:**
```
Connectivity options:
- [ ] RS485 wired
- [ ] Ethernet
- [ ] WiFi
- [ ] 4G/LTE
- [ ] LoRaWAN
- [ ] Other: [FILL IN]
```

---

**Question:** What devices do you EXPECT to support in the next 1-2 years?

**Your Answer:**
```
Batteries:
[FILL IN - Any specific brands or requirements?]

EV Chargers:
[FILL IN - Bidirectional (V2G) or unidirectional only?]

Heat Pumps / HVAC:
[FILL IN]

Industrial Controllers:
[FILL IN - PLC types, SCADA systems, etc.]
```

---

### C2. External System Integrations

**Question:** What external systems must K-NET integrate with?

**Your Answer:**

**Banking Systems:**
```
Target Banks:
- [FILL IN - e.g., Attijariwafa Bank]
- [FILL IN]

Green Invest Platform:
[YES / NO / MAYBE - If yes, what's the integration point?]

Other financing platforms:
[FILL IN]
```

**Payment Systems:**
```
Payment Gateways:
- [FILL IN - e.g., CMI, PayPal, local providers]

Direct Debit:
[YES / NO - If yes, which system?]

Bank APIs:
[FILL IN - Any specific banking APIs or protocols?]
```

**Utility/Government Systems:**
```
ONEE Integration:
[YES / NO - If yes, what data is exchanged?]

ANRE Reporting:
[YES / NO - If yes, what's the reporting format and frequency?]

AMEE Portal:
[YES / NO - Any integration required?]
```

**Carbon/ESG Systems:**
```
Carbon Registries:
[FILL IN - e.g., Gold Standard, Verra, UNFCCC]

ESG Reporting Platforms:
[FILL IN - e.g., for client ESG reports]

MRV Platforms:
[FILL IN - Any specific Measurement, Reporting, Verification platforms?]
```

---

## D. Financial & Risk Model

### D1. Liability & Error Margins

**Question:** What happens if K-NET says "X kWh produced" but it's actually "Y"?

**Your Answer:**

```
Who eats the difference?
[FILL IN - e.g., KardaTech absorbs up to 5%, then customer?]

What's the acceptable error margin?
[FILL IN - Percentage or absolute value]

How are disputes resolved?
[FILL IN - e.g., Manual review, third-party audit, arbitration?]

Do you need insurance for this?
[YES / NO / Already have it]
If YES, what type of insurance?
[FILL IN]
```

**Error Scenarios:**
```
Scenario 1: K-NET under-reports by 10%
[FILL IN - What happens? Who loses what?]

Scenario 2: K-NET over-reports by 10%
[FILL IN - What happens? Who is liable?]

Scenario 3: K-NET is offline for 48 hours
[FILL IN - How do you estimate production? What's the fallback?]
```

---

### D2. Billing Complexity

**Question:** How complex are the contract pricing models?

**Your Answer:**

**Pricing Structure:**
```
Flat rate per kWh?
[YES / NO - If no, explain]

Tiered pricing?
[YES / NO - If yes, describe tiers]

Time-of-use pricing?
[YES / NO - Different rates for different times?]

Performance guarantees?
[YES / NO - Penalties for underproduction?]
```

**Advanced Pricing Features:**
```
Inflation indexation:
[YES / NO - If yes, which index and how often?]

Currency fluctuation handling:
[FILL IN - Any multi-currency contracts?]

Minimum guarantees:
[YES / NO - Must pay minimum even if underproduction?]

Seasonal adjustments:
[YES / NO - Different rates by season?]
```

**Complex Pricing Formula:**
```
Paste your MOST complex contract pricing formula here:

[FILL IN - Include all variables, conditions, edge cases]

This helps us design the pricing engine architecture.
```

---

### D3. Regulatory Compliance

**Question:** What are the hard regulatory requirements?

**Your Answer:**

**Data Residency:**
```
Must data be stored in Morocco?
[YES / NO - If yes, all data or just PII?]

Any specific data center certifications required?
[FILL IN - e.g., ISO 27001, local hosting only?]
```

**Audit Trail:**
```
What audit trail is required?
[FILL IN - e.g., Every financial transaction must be traceable]

Retention period for audit logs?
[FILL IN - e.g., 7 years for financial data]
```

**Reporting Requirements:**
```
Frequency of regulatory reports?
[FILL IN - e.g., Monthly, quarterly, annually]

What data must be reported?
[FILL IN]

To whom?
[FILL IN - e.g., ANRE, ONEE, tax authority]
```

**Banking Regulations (if handling payments):**
```
Are you considered a payment processor?
[YES / NO / MAYBE]

If YES, what banking licenses are required?
[FILL IN]

Any AML/KYC requirements?
[FILL IN]
```

---

## E. Scale & Performance

### E1. Growth Trajectory

**Question:** What are realistic growth targets?

**Your Answer:**

| Metric | Year 1 | Year 2 | Year 3 | Year 5 |
|--------|--------|--------|--------|--------|
| Number of Assets (sites) | [FILL IN] | [FILL IN] | [FILL IN] | [FILL IN] |
| Total Installed Capacity (MW) | [FILL IN] | [FILL IN] | [FILL IN] | [FILL IN] |
| Number of End Customers | [FILL IN] | [FILL IN] | [FILL IN] | [FILL IN] |
| Number of Partner Installers | [FILL IN] | [FILL IN] | [FILL IN] | [FILL IN] |
| Data Points Per Day | [FILL IN] | [FILL IN] | [FILL IN] | [FILL IN] |

**Growth Assumptions:**
```
What drives these numbers?
[FILL IN - e.g., Market size, sales capacity, regulatory changes]

What could accelerate growth?
[FILL IN]

What could slow growth?
[FILL IN]
```

---

### E2. Data Retention

**Question:** How long must different types of data be retained?

**Your Answer:**

| Data Type | Retention Period | Hot/Warm/Cold Storage | Reason |
|-----------|------------------|-----------------------|---------|
| Raw meter readings (second-level) | [FILL IN] | [FILL IN] | [FILL IN] |
| Raw meter readings (minute-level) | [FILL IN] | [FILL IN] | [FILL IN] |
| Aggregated hourly data | [FILL IN] | [FILL IN] | [FILL IN] |
| Aggregated daily data | [FILL IN] | [FILL IN] | [FILL IN] |
| Financial records | [FILL IN] | [FILL IN] | [FILL IN] |
| Contracts and legal docs | [FILL IN] | [FILL IN] | [FILL IN] |
| Customer PII | [FILL IN] | [FILL IN] | [FILL IN] |
| Audit logs | [FILL IN] | [FILL IN] | [FILL IN] |
| Alerts and notifications | [FILL IN] | [FILL IN] | [FILL IN] |

**Storage Definitions:**
```
Hot storage: [FILL IN - e.g., Frequently accessed, fast retrieval]
Warm storage: [FILL IN - e.g., Occasionally accessed, slower OK]
Cold storage: [FILL IN - e.g., Archive only, cheapest option]
```

**Notes:** _This dramatically affects infrastructure costs and database architecture choices._

---

## F. Team & Resources

### F1. Development Team

**Question:** Who builds and maintains K-NET?

**Your Answer:**

**Current Team:**
```
Backend Developers: [FILL IN - Number and skill level]
Frontend Developers: [FILL IN - Number and skill level]
Data Engineers: [FILL IN - Number and skill level]
DevOps/SRE: [FILL IN - Number and skill level]
Product/Project Management: [FILL IN]
QA/Testing: [FILL IN]
```

**Technology Expertise:**
```
What technologies does the team know well?
- [FILL IN - e.g., Python, React, PostgreSQL, etc.]

What technologies are you willing to learn?
[FILL IN]

What technologies will you NOT use?
[FILL IN - e.g., No Microsoft stack, no proprietary tools, etc.]
```

**External Partners:**
```
Do you use offshore development?
[YES / NO - If yes, where and for what?]

Any development agencies or consultants?
[FILL IN]
```

**Hiring Plans:**
```
Budget for additional hires in next 12 months?
[FILL IN - Number of roles and seniority]

Roles you plan to hire:
- [FILL IN]
- [FILL IN]
- [FILL IN]
```

---

### F2. Operations & Support

**Question:** Who operates K-NET?

**Your Answer:**

**Operations Team:**
```
Do you have a dedicated DevOps/SRE team?
[YES / NO - If no, who handles operations?]

24/7 on-call requirements?
[YES / NO - If yes, who is on call?]

What happens if the system goes down at 3 AM?
[FILL IN - Who is notified? What's the response time?]
```

**Customer Support:**
```
Who handles customer support requests?
[FILL IN - Internal team, outsourced, automated?]

How do customers report issues?
[FILL IN - Email, phone, chat, in-app?]

What's the target response time?
[FILL IN - e.g., 4 hours for critical issues]
```

---

### F3. Infrastructure Budget

**Question:** What's the budget for infrastructure?

**Your Answer:**

```
Monthly infrastructure budget (Year 1):
[FILL IN - e.g., 10,000 MAD/month]

Expected growth in infrastructure costs:
[FILL IN - e.g., Double each year as we scale]

Any constraints on:
Cloud providers: [FILL IN - e.g., AWS only, Azure OK, no GCP?]
Region hosting: [FILL IN - e.g., Must be in Morocco]
Vendor lock-in: [FILL IN - Concerns about being locked in?]
Open source preference: [FILL IN - Prefer open source over paid tools?]
```

---

### F4. Timeline & Deadlines

**Question:** What are the hard deadlines?

**Your Answer:**

```
First pilot project needs K-NET by:
[FILL IN - Date]

Must license to first partner by:
[FILL IN - Date]

Bank integration required by:
[FILL IN - Date]

Regulatory compliance deadline:
[FILL IN - Date]

Other critical dates:
- [FILL IN]
- [FILL IN]
- [FILL IN]
```

**Timeline Reality Check:**
```
Are these dates flexible or immovable?
[FILL IN]

What's the consequence of missing a deadline?
[FILL IN]

Which deadline is MOST critical?
[FILL IN]
```

---

## G. Security & Trust

### G1. Threat Model

**Question:** What are you MOST worried about?

**Your Answer:**

**Rank these threats from 1 (most worried) to 5 (least worried):**

```
[ ] Data breach - Customer information exposed
[ ] Data manipulation - Someone fakes production numbers
[ ] Service downtime - Can't bill, customers can't see data
[ ] Fraud - Fake sites/assets created
[ ] Insider threats - Employee misusing access
[ ] Ransomware - System held hostage
[ ] IP theft - Competitors copying K-NET
[ ] Regulatory fines - Non-compliance penalties
```

**Top 3 Threats - Elaborate:**
```
#1 Most Worried: [FILL IN]
Why: [FILL IN]
Mitigation: [FILL IN]

#2 Second Most Worried: [FILL IN]
Why: [FILL IN]
Mitigation: [FILL IN]

#3 Third Most Worried: [FILL IN]
Why: [FILL IN]
Mitigation: [FILL IN]
```

---

### G2. Banking Integration Security

**Question:** If banks rely on K-NET data for lending decisions, what security standards are required?

**Your Answer:**

```
Do banks need SOC 2 Type II certification?
[YES / NO / MAYBE - If unsure, have they mentioned it?]

Do banks need penetration testing results?
[YES / NO / MAYBE - How often?]

Do banks need their own auditors to validate K-NET?
[YES / NO - If yes, at whose cost?]

What's the minimum security standard you MUST meet?
[FILL IN - e.g., ISO 27001, specific banking regulations?]
```

**Data Integrity:**
```
How do you prove data hasn't been tampered with?
[FILL IN - e.g., Blockchain, digital signatures, audit trails?]

Can a customer challenge their data?
[YES / NO - If yes, what's the resolution process?]
```

---

### G3. Access Control

**Question:** Who needs access to what data?

**Your Answer:**

**User Roles:**
```
Define each role and what they can see/do:

Role: KardaTech Admin
Can see: [FILL IN]
Can do: [FILL IN]

Role: KardaTech Operations
Can see: [FILL IN]
Can do: [FILL IN]

Role: Partner Installer Admin
Can see: [FILL IN - Only their customers?]
Can do: [FILL IN]

Role: End Customer
Can see: [FILL IN - Only their own site?]
Can do: [FILL IN]

Role: Bank/Investor (anonymous)
Can see: [FILL IN - Aggregated data only?]
Can do: [FILL IN]

Role: ONEE/ANRE Auditor
Can see: [FILL IN]
Can do: [FILL IN]
```

---

## H. Competitive Differentiation

### H1. What Can't You Buy?

**Question:** What must K-NET do that off-the-shelf products can't?

**Your Answer:**

```
Why can't you use existing tools like:
- Solar monitoring platforms (SolarEdge, SMA, etc.)
[FILL IN - What's missing?]

- Fintech platforms (Stripe, etc.)
[FILL IN - Why not suitable?]

- Generic IoT platforms (AWS IoT, Azure IoT, etc.)
[FILL IN - What's the gap?]
```

**K-NET's Unique Capabilities:**
```
Capability 1: [FILL IN - What ONLY K-NET can do?]
Why it's hard to replicate: [FILL IN]

Capability 2: [FILL IN]
Why it's hard to replicate: [FILL IN]

Capability 3: [FILL IN]
Why it's hard to replicate: [FILL IN]
```

---

### H2. What CAN You Buy?

**Question:** What will you use third-party services for?

**Your Answer:**

**Consider These Categories:**

```
Mapping/GIS:
[ ] Google Maps
[ ] Mapbox
[ ] OpenStreetMap
[ ] Other: [FILL IN]

Weather Data:
[ ] OpenWeatherMap
[ ] MeteoFrance
[ ] Local provider: [FILL IN]
[ ] Other: [FILL IN]

Payment Processing:
[ ] Stripe
[ ] PayPal
[ ] CMI (Center Monétique Interbancaire)
[ ] Local bank APIs
[ ] Other: [FILL IN]

Notifications:
[ ] SendGrid (email)
[ ] Twilio (SMS)
[ ] Local SMS gateway
[ ] Push notifications only
[ ] Other: [FILL IN]

Authentication:
[ ] Auth0
[ ] Firebase Auth
[ ] Keycloak
[ ] Build custom
[ ] Other: [FILL IN]

Analytics:
[ ] Google Analytics
[ ] Mixpanel
[ ] Amplitude
[ ] Build custom
[ ] Other: [FILL IN]
```

**Integration Philosophy:**
```
Do you prefer:
[ ] Buy over build (use SaaS whenever possible)
[ ] Build over buy (keep everything in-house)
[ ] Hybrid (build core, buy peripherals)

Reasoning: [FILL IN]
```

---

## I. Strategic Questions

### I1. The "Why K-NET?" Question

**Question:** In 2 years, if someone asks "Why did KardaTech win?" what's the answer?

**Your Answer:**

```
The primary reason for success will be:

[FILL IN - Choose one and elaborate]

[ ] Better User Experience
    Why: [FILL IN]
    Example: [FILL IN]

[ ] More Accurate Data
    Why: [FILL IN]
    Example: [FILL IN]

[ ] Banks Trust It More
    Why: [FILL IN]
    Example: [FILL IN]

[ ] Faster Deployment
    Why: [FILL IN]
    Example: [FILL IN]

[ ] Lower Cost
    Why: [FILL IN]
    Example: [FILL IN]

[ ] Something Else: [FILL IN]
    Why: [FILL IN]
    Example: [FILL IN]
```

---

### I2. The "Failed Scenario"

**Question:** What would cause K-NET to fail?

**Your Answer:**

```
Risk 1: [FILL IN - e.g., Too complex to use]
Probability: [HIGH/MED/LOW]
Mitigation: [FILL IN]

Risk 2: [FILL IN - e.g., Can't scale technically]
Probability: [HIGH/MED/LOW]
Mitigation: [FILL IN]

Risk 3: [FILL IN - e.g., Too expensive to operate]
Probability: [HIGH/MED/LOW]
Mitigation: [FILL IN]

Risk 4: [FILL IN]
Probability: [HIGH/MED/LOW]
Mitigation: [FILL IN]

Risk 5: [FILL IN]
Probability: [HIGH/MED/LOW]
Mitigation: [FILL IN]
```

**Early Warning Signs:**
```
What metrics would tell you K-NET is failing?
[FILL IN - e.g., Low partner adoption, high support tickets, etc.]

What's the check cadence?
[FILL IN - e.g., Review these metrics monthly]
```

---

## J. Priority Definitions

### J1. The "One Thing" Questions

**Question:** If you could only get ONE thing right, what is it?

**Your Answer:**
```
[FILL IN - What is THE most important thing?]

Why is this more important than everything else?
[FILL IN]

What would you sacrifice to get this right?
[FILL IN]
```

---

**Question:** What's the ONE feature that, if missing, makes K-NET pointless?

**Your Answer:**
```
[FILL IN - The critical must-have feature]

Why is this non-negotiable?
[FILL IN]

What happens without it?
[FILL IN]
```

---

### J2. MVP Scope

**Question:** What's the minimum viable product for K-NET?

**Your Answer:**

**For MVP, what MUST be included:**
```
1. [FILL IN]
2. [FILL IN]
3. [FILL IN]
4. [FILL IN]
5. [FILL IN]
```

**What can wait until V2:**
```
1. [FILL IN]
2. [FILL IN]
3. [FILL IN]
4. [FILL IN]
5. [FILL IN]
```

**What will you NEVER build:**
```
1. [FILL IN]
2. [FILL IN]
3. [FILL IN]
```

---

### J3. Success Metrics

**Question:** How will you measure K-NET's success?

**Your Answer:**

**Technical Metrics:**
```
System uptime target: [FILL IN - e.g., 99.9%]
Data accuracy target: [FILL IN - e.g., 99.5%]
API response time target: [FILL IN - e.g., < 200ms p95]
```

**Business Metrics:**
```
Time to onboard a new partner: [FILL IN]
Time to deploy a new site: [FILL IN]
Customer support tickets per 100 sites: [FILL IN]
Customer NPS score: [FILL IN]
```

**Financial Metrics:**
```
Cost per site per month: [FILL IN]
Break-even number of sites: [FILL IN]
LTV/CAC ratio target: [FILL IN]
```

---

## K. User Experience & Interface

### K1. Platform Focus

**Question:** What is the primary interface platform for each user type?

**Your Answer:**

| User Type | Primary Device | Secondary Device | Field/Remote Use? |
|-----------|----------------|------------------|-------------------|
| KardaTech Admin | [Desktop/Tablet/Mobile] | [FILL IN] | [YES/NO] |
| KardaTech Operations | [Desktop/Tablet/Mobile] | [FILL IN] | [YES/NO] |
| Partner Installer | [Desktop/Tablet/Mobile] | [FILL IN] | [YES/NO] |
| Installer Technicians | [Desktop/Tablet/Mobile] | [FILL IN] | [YES/NO] |
| End Customer | [Desktop/Tablet/Mobile] | [FILL IN] | [YES/NO] |
| Bank/Investor | [Desktop/Tablet/Mobile] | [FILL IN] | [YES/NO] |

**Mobile Requirements:**
```
Do you need native mobile apps (iOS/Android)?
[YES / NO - If yes, which platforms take priority?]

Is a responsive web app sufficient?
[YES / NO / MAYBE]

Offline mobile capability needed?
[YES / NO - If yes, what features must work offline?]
```

---

### K2. User Technical Proficiency

**Question:** How technically sophisticated are your users?

**Your Answer:**

```
Rate each user group's technical level (1-5, where 1=non-technical, 5=expert engineer):

KardaTech Admin: [1-5]
Partner Installer Admin: [1-5]
Installer Field Technicians: [1-5]
End Customer (business owner): [1-5]
Bank/Investor Analyst: [1-5]

What does this mean for UI design?
[FILL IN - e.g., Need lots of tooltips/wizards vs. power user shortcuts]
```

**Accessibility Considerations:**
```
Any accessibility requirements?
[ ] Screen reader support
[ ] High contrast mode
[ ] Larger text options
[ ] Keyboard navigation only
[ ] Other: [FILL IN]
```

---

### K3. Dashboard Style & Information Density

**Question:** What should the main dashboard look like for each user type?

**Your Answer:**

**For KardaTech Operations:**
```
Primary view needs to show:
[ ] Map view of all sites
[ ] List of alerts/issues
[ ] Performance charts
[FILL IN - What's the most important information at a glance?]

Information density preference:
[ ] Minimal/Clean - only critical info
[ ] Moderate - key metrics + drill-down
[ ] Dense - lots of data visible at once
```

**For End Customers:**
```
Primary view needs to show:
[ ] Current production (big numbers)
[ ] Financial savings/revenue
[ ] Environmental impact (CO2 avoided)
[ ] Performance over time
[FILL IN - What do they care about most?]

Emotional tone:
[FILL IN - e.g., Reassuring? Data-driven? Gamified? Professional?]
```

---

## L. Reporting & Analytics

### L1. Standard Reports

**Question:** What reports MUST K-NET generate out of the box?

**Your Answer:**

| Report Name | Who Needs It? | Frequency | Format | Key Data Points |
|-------------|---------------|-----------|---------|-----------------|
| [FILL IN - e.g., Monthly Production] | [FILL IN] | [Daily/Weekly/Monthly] | [PDF/Excel/Email] | [FILL IN] |
| [FILL IN] | [FILL IN] | [FILL IN] | [FILL IN] | [FILL IN] |
| [FILL IN] | [FILL IN] | [FILL IN] | [FILL IN] | [FILL IN] |
| [FILL IN] | [FILL IN] | [FILL IN] | [FILL IN] | [FILL IN] |

**Report Distribution:**
```
How are reports delivered?
[ ] Available in-app only
[ ] Emailed automatically
[ ] Downloadable on demand
[ ] Sent via webhook/API
[ ] Other: [FILL IN]

Can users customize reports?
[YES / NO - If yes, what level of customization?]
```

---

### L2. Custom Reporting & Exports

**Question:** What flexibility do users need to create their own reports?

**Your Answer:**

```
Can users export raw data?
[YES / NO - If yes, what formats? (CSV, Excel, JSON, etc.)]

Can users build custom dashboards?
[YES / NO - If yes, what tools? (Drag-and-drop builder, SQL query, etc.)]

Do users need to schedule custom reports?
[YES / NO]

Do users need to share reports with non-users?
[YES / NO - If yes, how? (Public link, email forwarding, etc.)]
```

**Data Export Limits:**
```
Are there limits on what data can be exported?
[FILL IN - e.g., Can export all historical data? Last 12 months only?]

Any compliance restrictions on data export?
[FILL IN - e.g., Customer PII cannot be exported in Excel]
```

---

### L3. Analytics & Insights

**Question:** What advanced analytics does K-NET need to provide?

**Your Answer:**

**Predictive Analytics:**
```
Do you need to predict:
[ ] Future production based on weather
[ ] Equipment failure likelihood
[ ] Customer churn risk
[ ] Revenue forecasting
[ ] Other: [FILL IN]

How far ahead must predictions be accurate?
[FILL IN - e.g., Next 24 hours, next week, next month?]
```

**Benchmarking & Comparison:**
```
Can users compare their site performance against:
[ ] Their own historical data
[ ] Other similar sites (anonymized)
[ ] Industry averages
[ ] Regional benchmarks

Is benchmarking a competitive differentiator?
[YES / NO - If yes, explain why]
```

---

## M. Training & Onboarding

### M1. User Onboarding Flow

**Question:** How does a new user get up to speed with K-NET?

**Your Answer:**

**For Partner Installers:**
```
Onboarding process:
1. [FILL IN - e.g., Account creation]
2. [FILL IN - e.g., Training session]
3. [FILL IN - e.g., Test site setup]
4. [FILL IN]

Who is responsible for training?
[FILL IN - Internal team, documentation, video tutorials, etc.]

What's the target time from signup to first productive use?
[FILL IN - e.g., Same day, 1 week, 1 month?]
```

**For End Customers:**
```
Who trains the end customer?
[FILL IN - Partner installer? KardaTech? Self-service?]

What do they need to understand?
[FILL IN - Key concepts they must learn]

Can K-NET be used without training?
[YES / NO - If no, what's the minimum training required?]
```

---

### M2. Documentation & Help Resources

**Question:** What help resources will be available?

**Your Answer:**

```
In-application help:
[ ] Tooltip definitions
[ ] Context-sensitive help buttons
[ ] Interactive tutorial/wizard
[ ] Searchable knowledge base
[ ] Chatbot/AI assistant
[ ] Live chat support

External resources:
[ ] PDF user manual
[ ] Video tutorial library
[ ] FAQ page
[ ] Community forum
[ ] Email/phone support
[ ] In-person training available

What's your philosophy on documentation?
[FILL IN - e.g., Comprehensive docs vs. intuitive UI that needs minimal docs?]
```

---

### M3. Certification & Advanced Training

**Question:** Do you need certified installers or power users?

**Your Answer:**

```
Do installers need certification to use K-NET?
[YES / NO - If yes, who certifies them?]

Are there different user skill levels?
[YES / NO - If yes, what privileges change with skill level?]

Do you plan to offer training as a revenue stream?
[YES / NO / MAYBE]
```

---

## N. Environmental & Physical Factors

### N1. Operating Environment

**Question:** What physical conditions will K-NET hardware/software face?

**Your Answer:**

**Location Considerations:**
```
Where will K-NET hardware be deployed?
[ ] Climate-controlled server rooms
[ ] Industrial facilities (dust, heat, vibration)
[ ] Outdoor installations (weather exposure)
[ ] Residential/office settings
[ ] Other: [FILL IN]

What temperatures must equipment withstand?
[FILL IN - e.g., -5°C to 45°C in Morocco summers?]

Any environmental hazards?
[FILL IN - e.g., Dust, humidity, salt air (coastal), etc.]
```

**Power Considerations:**
```
What happens if site loses power (beyond just internet)?
[FILL IN - Does local hardware need UPS?]

How long should on-site equipment run without grid power?
[FILL IN - e.g., 4 hours with battery backup?]
```

---

### N2. Hardware Durability & Maintenance

**Question:** What are the hardware reliability requirements?

**Your Answer:**

```
Expected hardware lifespan:
[FILL IN - e.g., 5 years, 10 years?]

How often can physical maintenance happen?
[FILL IN - e.g., Quarterly site visits acceptable? Remote-only preferred?]

What happens if hardware fails?
[FILL IN - Replacement process, spare parts inventory, etc.]

Do you need remote hardware diagnostics?
[YES / NO - Ability to check hardware health remotely?]
```

---

## O. Customer Lifecycle Management

### O1. Onboarding New Sites

**Question:** What's the process from signed contract to active monitoring?

**Your Answer:**

```
Step-by-step site activation:
1. [FILL IN - e.g., Hardware installation]
2. [FILL IN - e.g., Device configuration]
3. [FILL IN - e.g., Network setup]
4. [FILL IN - e.g., First data sync]
5. [FILL IN - e.g., Customer handoff]

Who does each step?
[FILL IN - KardaTech? Partner installer? Customer?]

How long does site activation typically take?
[FILL IN - e.g., Same day, 1 week?]

Can sites be activated in bulk?
[YES / NO - If yes, how?]
```

---

### O2. Contract Renewals & Upgrades

**Question:** How are long-term customer relationships managed?

**Your Answer:**

```
Contract length:
[FILL IN - e.g., 1 year, 3 years, 5 years?]

Renewal process:
[ ] Automatic renewal
[ ] Manual renewal required
[ ] Reminder sent X days before expiration
[ ] Other: [FILL IN]

What happens at renewal?
[FILL IN - Rate renegotiation? Hardware upgrade? Term extension?]

Can customers upgrade/downgrade mid-contract?
[YES / NO - If yes, what's allowed?]
```

---

### O3. Offboarding & Data Handover

**Question:** What happens when a customer leaves?

**Your Answer:**

```
What data does the customer get to keep?
[FILL IN - All historical data? Last 12 months? Nothing?]

What's the data handover format?
[FILL IN - Export to CSV? PDF reports? API access for 30 days?]

Who handles device decommissioning?
[FILL IN - KardaTech? Customer? Partner?]

Are there offboarding fees?
[YES / NO - If yes, what covers?]
```

---

### O4. Account Changes & Transfers

**Question:** What if a customer is acquired, or ownership changes?

**Your Answer:**

```
How is account transfer handled?
[FILL IN - What's the process?]

What data/history transfers with the account?
[FILL IN]

Who retains rights to historical production data?
[FILL IN - Original owner? New owner? Both?]

Any notifications required?
[FILL IN - e.g., Notify bank? Update contracts?]
```

---

## P. Testing & Quality Assurance

### P1. Testing Philosophy

**Question:** What level of testing is required for K-NET?

**Your Answer:**

```
How critical is software quality?
[FILL IN - On a scale from "move fast and break things" to "NASA-level testing"]

What types of testing are non-negotiable?
[ ] Unit tests for all business logic
[ ] Integration tests for device communications
[ ] End-to-end UI automation
[ ] Load/performance testing
[ ] Security penetration testing
[ ] Other: [FILL IN]

What's your acceptable bug tolerance?
[FILL IN - e.g., Zero critical bugs in production, minor bugs OK?]
```

---

### P2. Testing Cadence & Process

**Question:** How often is K-NET tested?

**Your Answer:**

```
When does testing happen?
[ ] Before every release
[ ] Continuous automated testing
[ ] Quarterly full regression testing
[ ] Annual security audit
[ ] Other: [FILL IN]

Who does testing?
[FILL IN - Dedicated QA team? Developers test their own code? Third-party auditors?]

What happens if a critical bug is found in production?
[FILL IN - Hotfix process, rollback procedures, etc.]
```

---

### P3. Penetration Testing & Security Audits

**Question:** What security validation is required?

**Your Answer:**

```
Penetration testing frequency:
[FILL IN - e.g., Annually? After major changes? Before bank integration?]

Who performs security audits?
[FILL IN - Internal team? Third-party firm? Bank auditors?]

What standards must be met?
[FILL IN - e.g., OWASP Top 10? Banking security standards?]

Are test results shared with customers/banks?
[YES / NO - If yes, what level of detail?]
```

---

## Q. Disaster Recovery & Business Continuity

### Q1. Recovery Objectives

**Question:** How quickly must K-NET recover from a disaster?

**Your Answer:**

```
RTO (Recovery Time Objective):
[FILL IN - e.g., "System must be back online within 4 hours"]

RPO (Recovery Point Objective):
[FILL IN - e.g., "Can lose maximum 1 hour of data"]

What defines a "disaster"?
[FILL IN - e.g., Data center outage, region-wide failure, ransomware, etc.]

What's an acceptable yearly downtime budget?
[FILL IN - e.g., Maximum 8 hours planned + 4 hours unplanned per year]
```

---

### Q2. Backup Strategy

**Question:** How are backups handled?

**Your Answer:**

```
Backup frequency:
[ ] Real-time replication
[ ] Hourly backups
[ ] Daily backups
[ ] Weekly backups
[ ] Other: [FILL IN]

Backup storage:
[FILL IN - Same region? Different region? Different cloud provider? On-premises?]

How long are backups kept?
[FILL IN]

Are backups encrypted?
[YES / NO - If yes, how?]

Can backups be restored by non-technical staff?
[YES / NO - If no, who can restore?]
```

---

### Q3. Business Continuity Plans

**Question:** What if KardaTech experiences a major incident?

**Your Answer:**

```
Who is responsible for disaster recovery?
[FILL IN - Internal team? Managed service provider?]

What happens if:
Primary data center is destroyed?
[FILL IN]

Key technical staff are unavailable?
[FILL IN]

Ransomware attack encrypts all data?
[FILL IN]

Do customers need a business continuity SLA?
[YES / NO - If yes, what penalties for downtime?]
```

---

## R. Localization & Language Support

### R1. Language Requirements

**Question:** What languages does K-NET support?

**Your Answer:**

```
Required languages for launch:
[FILL IN - e.g., French, English, Arabic]

Planned languages for future:
[FILL IN - e.g., Spanish for expansion?]

Can users switch languages?
[YES / NO - If yes, per-user or per-organization?]

Is RTL (right-to-left) support needed for Arabic?
[YES / NO - Full RTL or minimal support?]
```

---

### R2. Regional Customization

**Question:** What else varies by region?

**Your Answer:**

```
Date/time formats:
[FILL IN - e.g., DD/MM/YYYY vs MM/DD/YYYY]

Number/currency formats:
[FILL IN - e.g., MAD vs € vs $, decimal separators, etc.]

Units of measurement:
[FILL IN - e.g., kW vs MW, Celsius vs Fahrenheit, etc.]

Cultural considerations:
[FILL IN - e.g., Color meanings, iconography, etc.]

Regulatory variations by region:
[FILL IN - e.g., Different rules for Morocco vs future markets]
```

---

## S. Third-Party Developer Access

### S1. API Availability

**Question:** Can external developers integrate with K-NET?

**Your Answer:**

```
Will you offer a public API?
[YES / NO / MAYBE]

Who needs API access?
[ ] Partner installers building custom integrations
[ ] Banks pulling data directly
[ ] Third-party developers building apps
[ ] Other: [FILL IN]

Is API access a revenue feature?
[FILL IN - Free? Paid tier? Enterprise only?]
```

---

### S2. API Capabilities & Restrictions

**Question:** What can/can't developers do via API?

**Your Answer:**

```
API capabilities:
[FILL IN - Read-only data access? Write operations? Webhooks?]

Rate limits:
[FILL IN - Requests per minute/day? Different by tier?]

Authentication method:
[FILL IN - API keys? OAuth? JWT?]

Approval process:
[FILL IN - Self-service? Manual review? NDAs required?]
```

**Data Access Restrictions:**
```
Can developers access:
[ ] Raw production data
[ ] Aggregated/anonymized data only
[ ] Customer PII (if authorized)
[ ] Financial data (if authorized)

What data is NEVER available via API?
[FILL IN]
```

---

### S3. API Documentation & Support

**Question:** How do developers learn to use the API?

**Your Answer:**

```
Documentation approach:
[ ] Full API reference with examples
[ ] Quick start guide + reference
[ ] Code samples in multiple languages
[ ] Interactive API explorer (Swagger/Postman)
[ ] Other: [FILL IN]

Developer support:
[ ] Community forum
[ ] Email support
[ ] Paid support tier
[ ] No support, self-service only

SDK availability:
[FILL IN - Do you provide official libraries? (Python, JavaScript, etc.)]
```

---

## Next Steps

Once you've completed this questionnaire:

**Step 1:** Review with the full founding team
**Step 2:** Identify gaps and unknowns that need research
**Step 3:** Prioritize answers that are critical for MVP
**Step 4:** Share with me for architecture proposal

---

## Notes & Comments

```
[Use this space for any additional thoughts, concerns, or context
 that doesn't fit into the structured questions above]




```

---

**Document Status:**
- [ ] Not started
- [ ] In progress
- [ ] Completed
- [ ] Reviewed with team

**Next Review Date:** [FILL IN]
