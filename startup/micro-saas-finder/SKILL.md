---
name: micro-saas-finder
description: Discover underserved niches and opportunities for profitable micro-SaaS products. Use this skill when looking for SaaS ideas in a specific niche, trying to find underserved markets, evaluating whether a micro-SaaS opportunity is viable, or researching what small software products could generate sustainable revenue. Trigger when someone says "I want to find a SaaS idea", "help me find a niche", "what micro-SaaS could I build", or is doing opportunity discovery for a small software product.
---

# Micro-SaaS Finder

## What Makes a Good Micro-SaaS?

A micro-SaaS is a small, focused software product that:
- Solves one specific problem for one specific audience
- Can be built by 1–2 people
- Generates $1K–$50K MRR as a sustainable business
- Has low ongoing maintenance burden

### The Ideal Profile:
```
Audience:   A professional/business with a specific workflow problem
Problem:    Repetitive, manual, or error-prone task they do regularly
Solution:   Automate or streamline that specific task
Price:      $29–$299/month (B2B pricing, not consumer)
GTM:        Reach audience where they already gather (community, tool ecosystem)
Moat:       Deep integration with their existing tools, or niche expertise
```

---

## Discovery Methods

### Method 1: App Store / Marketplace Mining

The most reliable signal: if people are selling something via a plugin marketplace, there's real demand.

**Where to look:**
- Zapier / Make app directory → automations people are paying for
- Shopify App Store → e-commerce workflow tools
- Salesforce AppExchange → CRM add-ons
- HubSpot Marketplace → marketing tool extensions
- Notion / Airtable integrations → workflow tools
- Chrome Web Store → browser productivity tools
- VS Code extensions → developer tools
- Figma plugins → design workflow tools

**What to look for:**
- Paid apps with 1,000+ installs and 4+ star ratings → validated demand
- Complaints in reviews → gap to fill
- High-rated apps with bad UX → rebuild opportunity

### Method 2: Community Pain Mining

Go where your target users hang out and read their frustrations.

**Communities by niche:**
```
Developers:         Hacker News, r/webdev, r/programming, Dev.to
Marketers:          r/marketing, Marketing Twitter, SparkToro
E-commerce:         r/shopify, Shopify Community forums
Finance/Accounting: r/accounting, CPAnet forums
HR/Recruiting:      r/recruiting, SHRM community
Legal:              r/legaladvice, lawyer Twitter
Real estate:        BiggerPockets, r/realestateinvesting
Creators:           r/youtubers, Creator Economy forums
```

**Search patterns:**
- "[tool] + alternative"
- "[task] + "is there a tool that"
- "[workflow] + frustrating"
- "I built X because nothing existed for"

### Method 3: Tool Ecosystem Gaps

Find popular tools with documented gaps or missing integrations.

**Process:**
1. Pick a popular B2B SaaS (Notion, Airtable, HubSpot, Slack, Linear)
2. Look at their feature requests: `[tool] + "feature request"` or their public roadmap
3. Find highly upvoted requests that haven't been built
4. Build that as a standalone integration

### Method 4: Job Description Analysis

Companies hiring for a role = they have that problem.

- Companies hiring "Excel Automation Specialist" → build an Excel automation tool
- Companies hiring "Data Entry VA" → build a data entry automation tool
- Companies hiring "Reporting Analyst" → build an automated reporting tool

Search LinkedIn job postings + Upwork/Fiverr gigs for repetitive, described-in-detail tasks.

### Method 5: Existing Business Revenue Signals

Look for businesses already making money in a space you can productize:

- Fiverr/Upwork gigs with 1,000+ orders → automatable workflow
- "X as a service" businesses → software-ize the service
- Spreadsheet templates selling on Etsy/Gumroad → turn it into software
- Highly-priced consulting in a niche → productize the deliverable

---

## Opportunity Scoring

Score each opportunity on these dimensions:

| Criterion | Weight | Score (1–5) | Notes |
|-----------|--------|-------------|-------|
| Audience size | 15% | | Large enough to support $10K MRR? |
| Pain intensity | 25% | | Would they pay to fix this today? |
| Willingness to pay | 20% | | B2B? Professional use? |
| Build complexity | 20% | | Can 1–2 people build in 1–3 months? |
| Competition | 10% | | Is the space empty or crowded? |
| GTM clarity | 10% | | Clear channel to reach these users? |

**Total score** = weighted average × 5

- 4.0+: Strong opportunity, validate and build
- 3.0–3.9: Worth exploring with deeper research
- Below 3.0: Skip or significantly reframe

---

## Validation Before Building

Before writing code, validate with 3 signals:

### Signal 1: Someone is already paying for it
- Find a paid alternative (even an inferior one)
- Find freelancers charging for this work
- Find Excel/Sheets templates being sold

### Signal 2: You can reach the audience
- Identify 3 specific communities or channels
- Can you post there credibly?
- Is there a person with an audience who would promote it?

### Signal 3: You can talk to 5 potential users
- Find 5 real people with this problem
- Have a 20-minute conversation
- At least 2 of 5 should say "when can I buy this?"

---

## Niche Generator

Combine these axes to generate niche ideas:

**Persona** × **Workflow** × **Tool** = Micro-SaaS Niche

| Persona | Workflow | Tool | Potential Product |
|---------|----------|------|------------------|
| E-commerce seller | Inventory sync | Shopify + Amazon | Cross-platform inventory manager |
| Recruiter | Candidate tracking | LinkedIn + ATS | LinkedIn-to-ATS sync tool |
| Content creator | Repurposing | YouTube → text | Auto-repurposing pipeline |
| Accountant | Expense categorization | QuickBooks | AI expense categorizer |
| SaaS founder | Customer success | Intercom | Churn prediction alerts |
| Agency | Client reporting | Google Ads + Analytics | Automated client report generator |

---

## Output: Opportunity Brief

```markdown
## [Product Name Idea]

**Niche**: [Persona] dealing with [specific problem] using [existing tool/workflow]

**Problem statement**: [1-2 sentences describing the pain]

**Solution**: [1 sentence: what your product does]

**Target price**: $[X]/month (billed annually)
**Revenue target**: $[X] MRR at [N] customers

**Validation signals found**:
- [ ] Existing paid alternatives: [list]
- [ ] Community demand: [source + evidence]
- [ ] Build complexity: [Low / Medium / High]

**GTM channel**: [how you'd reach first 100 customers]

**Opportunity score**: [X/5]

**Next step**: [talk to 5 users / build a landing page / research tech requirements]
```
