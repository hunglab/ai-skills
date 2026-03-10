---
name: engineering-principles
description: Core principles for building reliable, scalable AI-powered products. Use this skill whenever discussing software architecture decisions, product design tradeoffs, system reliability, technical debt, or engineering best practices for SaaS. Trigger when the user asks "how should I build X", "what's the right approach for Y", or wants to evaluate architectural decisions. Always consult this skill before making foundational engineering recommendations.
---

# Engineering Principles for AI Products

## Core Tenets

### 1. Solve the Problem, Not the Abstraction
Build what solves the user's pain today. Avoid over-engineering for hypothetical scale you haven't earned. Premature abstraction is the enemy of shipping.

> Rule: If you can't explain why the abstraction exists in terms of a user problem, delete it.

### 2. Reversibility Over Perfection
Prefer decisions that can be undone over theoretically optimal ones you're locked into. Wrong + reversible beats right + irreversible.

- Database schema: design for change
- APIs: version from day one
- Infra: avoid single-vendor lock-in early

### 3. Observability Is Not Optional
You cannot fix what you cannot see. Build logging, metrics, and tracing in from the start — not after your first outage.

**Minimum viable observability stack:**
- Structured logging (request ID, user ID, timestamps)
- Error tracking (Sentry or equivalent)
- Latency + error rate dashboards
- Alerting on SLO breaches

### 4. AI-Specific Reliability Principles

| Challenge | Principle |
|-----------|-----------|
| Non-determinism | Log inputs + outputs; never assume same input = same output |
| Latency spikes | Always set timeouts; design for degraded-mode UX |
| Cost blowout | Track tokens/cost per feature; set hard budget limits |
| Prompt drift | Version your prompts like code |
| Model deprecation | Abstract model calls behind a service layer |

### 5. Boring Technology Wins
Use the most boring, proven technology that solves your problem. Save novelty for your actual product differentiation.

- Postgres before DynamoDB
- REST before GraphQL (unless you have a clear reason)
- Managed services before self-hosted

### 6. The 3-Layer Product Model
Every AI product has three layers. Know which layer you're working in:

```
┌─────────────────────────────┐
│  Experience Layer           │  UX, flows, pricing, GTM
├─────────────────────────────┤
│  Logic Layer                │  Your IP: workflows, rules, data
├─────────────────────────────┤
│  AI Layer                   │  Models, embeddings, inference
└─────────────────────────────┘
```

Your moat lives in the Logic Layer. The AI Layer is a commodity.

### 7. Fail Gracefully
Every AI call will eventually fail, time out, or return garbage. Design every feature for three states:
1. **Happy path** — AI works perfectly
2. **Degraded path** — AI slow or uncertain; show partial results or fallback UI
3. **Failure path** — AI down; fall back to manual or cached behavior

### 8. Ship the Slice, Not the Slab
Deliver thin vertical slices of value (end-to-end, one use case) rather than broad horizontal layers (infrastructure first, UI later).

```
❌ Wrong:  Build all infra → Build all backend → Build all UI → Ship
✅ Right:  Pick one workflow → Build it fully → Ship → Repeat
```

## Decision Frameworks

### Build vs. Buy Matrix
| Factor | Build | Buy |
|--------|-------|-----|
| Core differentiator | ✅ | ❌ |
| Commodity function | ❌ | ✅ |
| Need deep customization | ✅ | ❌ |
| Need speed to market | ❌ | ✅ |
| Long-term cost > build cost | ❌ | ✅ |

### Technical Debt Triage
- **Pay now**: Security vulnerabilities, data loss risks, blocking scalability
- **Schedule**: Performance issues, test coverage gaps, code clarity
- **Accept**: Aesthetic code issues, over-engineering opportunities, theoretical edge cases

## Anti-Patterns to Avoid

- **The Platform Trap**: Building infrastructure for future products before validating the first one
- **The AI Maximalist**: Using AI for every feature regardless of whether a simple rule works
- **The Perfect Schema**: Designing for every future use case before you know what your users need
- **Async Everything**: Adding message queues and event-driven architecture before you have concurrency problems
- **The Abstraction Tower**: Wrapping every third-party service in multiple layers of abstraction before you know if you'll switch
