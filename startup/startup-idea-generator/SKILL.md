---
name: startup-idea-generator
description: Generate, score, and validate startup ideas systematically. Use this skill when brainstorming startup ideas, evaluating whether an idea is worth pursuing, stress-testing a startup concept, or generating ideas in a specific domain. Trigger when someone says "help me think of startup ideas", "is this a good startup idea", "generate ideas for X space", or is in early-stage ideation. Also apply when the user has an idea and wants to pressure-test it before building.
---

# Startup Idea Generator

## Where Good Startup Ideas Come From

The best startup ideas share a common origin:

1. **Personal pain** — "I had this problem and nothing solved it"
2. **Expert insight** — "I worked in X industry and saw this broken thing"
3. **Timing** — "This wasn't possible until [new technology/regulation/behavior]"
4. **Market shift** — "Users who used to do X manually now expect software to do it"
5. **Intersection** — "I combined two things that never existed together"

Avoid: "I thought it would be cool" ideas with no clear pain or user.

---

## Idea Generation Frameworks

### Framework 1: The Intersection Matrix

Pick two domains. What's possible at their intersection?

```
AI × [Industry]       → AI-powered [industry] tool
Remote work × [Job]   → Remote-native [job function] software
No-code × [Process]   → [process] automation without engineers
Data × [Profession]   → [profession]'s data intelligence layer
```

**Generate 10 combinations, filter to 2–3 interesting ones.**

### Framework 2: The "Just Like X But For Y" Frame

Take a proven model and apply it to an underserved niche.

- "Stripe, but for [emerging payment use case]"
- "Notion, but for [specific profession]"
- "Calendly, but for [specific industry scheduling problem]"
- "Linear, but for [non-software teams]"

**This is not unoriginal** — most successful B2B SaaS is a better version of an existing idea applied to a new segment.

### Framework 3: The 10x Improvement Frame

Find something that exists but is deeply flawed. Ask: "What would make this 10x better?"

- Existing solution too slow → yours is fast
- Existing solution requires expertise → yours is accessible
- Existing solution is expensive → yours is affordable
- Existing solution is manual → yours is automated
- Existing solution is generic → yours is specialized

### Framework 4: The Workflow Audit

Pick any job role. Map their full weekly workflow. Find the most painful step.

```
Role: [Sales Manager]
Weekly workflow:
  Mon: Review pipeline → [tedious: manual CRM updates]
  Tue: Team 1:1s → [tedious: no call summary, manual notes]
  Wed: Forecast report → [tedious: Excel, 2 hours every week]
  ...
```

Any "tedious" step = potential product.

### Framework 5: The "What I Hacked Together" Frame

Think about solutions you or your team have built internally:
- Internal tools your company uses
- Scripts you wrote to automate your own work
- Zapier automations you built
- Templates you made that others asked for

If you built it yourself because nothing existed, others have the same problem.

---

## Idea Scoring: The TAPE Framework

Score every idea on four dimensions:

### T — Timing
Is this the right moment?
- New enabling technology (GPT-4, new API, regulatory change)
- Behavior shift (remote work, platform shift)
- Market gap created by competitor failure
Score 1–5: 1 = no timing, 5 = perfect timing

### A — Audience Accessibility
Can you reach these users?
- Can you find 100 of them right now?
- Are they in a specific community, platform, or geography?
- Do you have credibility with them?
Score 1–5: 1 = no idea how to reach, 5 = direct access

### P — Pain Intensity
How bad is the problem?
- Are they paying for a worse solution today?
- Would they switch vendors for a better solution?
- Does this cost them time, money, or risk?
Score 1–5: 1 = nice to have, 5 = bleeding pain

### E — Edge (Your Advantage)
Why are you the one to build this?
- Domain expertise
- Existing audience
- Technical advantage
- Relationship with customers
Score 1–5: 1 = no advantage, 5 = unique position

**TAPE Score** = (T + A + P + E) / 4
- 4.0+: Pursue aggressively
- 3.0–3.9: Validate more before building
- Below 3.0: Hard pass

---

## Idea Stress Test

Before committing, run every idea through these challenges:

### The "Why Now?" Test
If this idea is good, why didn't someone build it 3 years ago? What changed?
(If there's no good answer, this is probably a graveyard)

### The "Who Is User #1?" Test
Name a specific real human who would be your first customer.
- What's their job title?
- What company do they work at?
- Why would they pay for this today?
(If you can't name a real person, you don't have an idea yet)

### The "Painkiller or Vitamin?" Test
- Painkiller: Solves an acute pain, user seeks it out, clear ROI
- Vitamin: Nice to have, hard to sell, easily deprioritized

Build painkillers. Vitamins are for later-stage companies with distribution.

### The "What Would Have to Be True?" Test
List 3–5 assumptions your idea requires:
```
Assumption 1: Users will pay for X
Assumption 2: We can acquire users for < $Y CAC
Assumption 3: The technical approach works
```
Rank by risk. Design experiments to kill the riskiest assumptions first.

---

## Idea Output Template

```markdown
## [Idea Name]

**One-liner**: [What it does, for whom, how]

**Problem**: [Specific pain, with evidence]

**Solution**: [Your approach]

**Why now**: [What changed that makes this possible/urgent]

**Target user**: [Specific persona]

**Revenue model**: [How it makes money, rough pricing]

**GTM**: [How you'd get first 100 users]

**TAPE Score**:
- Timing: X/5 — [reason]
- Audience: X/5 — [reason]
- Pain: X/5 — [reason]
- Edge: X/5 — [reason]
- **Total**: X.X/5

**Biggest risk**: [The assumption most likely to kill this]

**First experiment**: [How to test that assumption in < 2 weeks]
```
