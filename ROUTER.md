---
name: skill-router
description: Master router for the AI Product Engineering Toolkit. Read this FIRST before any task. It maps user prompts to the correct skill(s) to load. Always consult this router whenever the user's intent touches product building, market analysis, system architecture, startup strategy, AI agent design, or growth engineering — even if they don't use technical terms.
---

# Skill Router

Read the user's prompt → match to one or more skills below → load those `SKILL.md` files via the `view` tool → then respond.

---

## Routing Decision Tree

```
User sends a prompt
        │
        ├─► UNDERSTANDING an existing product or market?
        │       ├── "how does X work / what's their stack"  →  analysis/system-reverse-engineering
        │       ├── "what features does X have"             →  analysis/saas-feature-extraction
        │       ├── "who are the competitors / market map"  →  analysis/competitor-analysis
        │       └── "what do users really want / pain"      →  analysis/pain-point-mining
        │
        ├─► DESIGNING a system or data model?
        │       ├── "how should I architect this SaaS"      →  architecture/saas-architecture-patterns
        │       ├── "API design / endpoints / REST"         →  architecture/api-design-patterns
        │       └── "database schema / data model / tables" →  architecture/database-schema-inference
        │
        ├─► BUILDING something?
        │       ├── "clone / replicate this app"            →  execution/blackbox-app-cloning
        │       ├── "ship fast / MVP / rapid build"         →  execution/rapid-product-rebuild
        │       └── "AI agent / autonomous workflow"        →  execution/ai-agent-builder
        │
        ├─► FINDING an opportunity or idea?
        │       ├── "micro-SaaS / niche / small product"    →  startup/micro-saas-finder
        │       └── "startup idea / validate / score idea"  →  startup/startup-idea-generator
        │
        ├─► STRATEGY or long-term defense?
        │       ├── "moat / defensible / competitive edge"  →  strategy/product-moat-design
        │       └── "AI wrapper / is this defensible AI"    →  strategy/ai-wrapper-detection
        │
        ├─► GROWTH or acquisition?
        │       ├── "virality / sharing / referral"         →  growth/viral-feature-design
        │       └── "growth loop / CAC / compounding"       →  growth/growth-loop-engine
        │
        └─► GENERAL thinking or principles?
                ├── "how to solve / root cause / stuck"     →  foundation/problem-solving-framework
                ├── "feedback loop / second-order effects"  →  foundation/system-thinking
                └── "architectural tradeoff / best practice"→  foundation/engineering-principles
```

---

## Quick Routing Table

| User says… | Load skill(s) |
|-----------|--------------|
| "How does Notion work under the hood?" | `analysis/system-reverse-engineering` |
| "What features does Linear have?" | `analysis/saas-feature-extraction` |
| "Who are the competitors in the CRM space?" | `analysis/competitor-analysis` |
| "Find me pain points for accountants" | `analysis/pain-point-mining` |
| "Design the backend for my SaaS" | `architecture/saas-architecture-patterns` |
| "How should I design this API?" | `architecture/api-design-patterns` |
| "What tables do I need for this product?" | `architecture/database-schema-inference` |
| "I want to clone Calendly" | `execution/blackbox-app-cloning` |
| "Help me ship this in a week" | `execution/rapid-product-rebuild` |
| "Build me an AI agent that does X" | `execution/ai-agent-builder` |
| "Find me a micro-SaaS niche" | `startup/micro-saas-finder` |
| "Is this a good startup idea?" | `startup/startup-idea-generator` |
| "How do I make this defensible?" | `strategy/product-moat-design` |
| "Is this just an AI wrapper?" | `strategy/ai-wrapper-detection` |
| "How do I make my product go viral?" | `growth/viral-feature-design` |
| "Design a growth loop for my product" | `growth/growth-loop-engine` |
| "I don't know where to start on this problem" | `foundation/problem-solving-framework` |
| "Why does this keep breaking?" | `foundation/system-thinking` |
| "Should I build this or buy it?" | `foundation/engineering-principles` |

---

## Power Combos — Multi-Skill Tasks

Some tasks benefit from loading 2–3 skills together. Common combos:

| Task | Skills to load |
|------|---------------|
| **Clone a product** | `system-reverse-engineering` + `saas-feature-extraction` + `blackbox-app-cloning` |
| **Validate a startup idea** | `startup-idea-generator` + `competitor-analysis` + `pain-point-mining` |
| **Design a full SaaS backend** | `saas-architecture-patterns` + `api-design-patterns` + `database-schema-inference` |
| **Grow an existing product** | `growth-loop-engine` + `viral-feature-design` |
| **Evaluate an AI startup** | `ai-wrapper-detection` + `product-moat-design` |
| **Find + validate a niche** | `micro-saas-finder` + `pain-point-mining` + `competitor-analysis` |
| **Build an AI SaaS fast** | `rapid-product-rebuild` + `ai-agent-builder` + `saas-architecture-patterns` |
| **Diagnose a persistent problem** | `problem-solving-framework` → then route to the relevant domain skill |

---

## Routing Rules

1. **Always load at least one skill** — even for general questions, a foundation skill applies.
2. **When in doubt, load the closest skill** — partial relevance beats no skill.
3. **For complex tasks, stack skills** — use the Power Combos above.
4. **Load skills before generating output** — read the SKILL.md first, then respond.
5. **Follow sub-file pointers** — some skills reference `references/` or `agents/` directories; load those when directed.

---

## Skill Directory

```
skills/
├── ROUTER.md                          ← you are here
│
├── foundation/
│   ├── README.md
│   ├── engineering-principles/SKILL.md
│   ├── system-thinking/SKILL.md
│   └── problem-solving-framework/SKILL.md
│
├── analysis/
│   ├── README.md
│   ├── system-reverse-engineering/SKILL.md
│   ├── saas-feature-extraction/SKILL.md
│   ├── competitor-analysis/SKILL.md
│   └── pain-point-mining/SKILL.md
│
├── architecture/
│   ├── README.md
│   ├── saas-architecture-patterns/SKILL.md
│   ├── api-design-patterns/SKILL.md
│   └── database-schema-inference/SKILL.md
│
├── execution/
│   ├── README.md
│   ├── blackbox-app-cloning/SKILL.md
│   ├── rapid-product-rebuild/SKILL.md
│   └── ai-agent-builder/SKILL.md
│
├── startup/
│   ├── README.md
│   ├── micro-saas-finder/SKILL.md
│   └── startup-idea-generator/SKILL.md
│
├── strategy/
│   ├── README.md
│   ├── product-moat-design/SKILL.md
│   └── ai-wrapper-detection/SKILL.md
│
└── growth/
    ├── README.md
    ├── viral-feature-design/SKILL.md
    └── growth-loop-engine/SKILL.md
```
