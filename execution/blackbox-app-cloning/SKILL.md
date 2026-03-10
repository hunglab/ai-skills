---
name: blackbox-app-cloning
description: Clone any web application from its user-facing behavior alone, without access to source code. Use this skill when the user wants to replicate a product, build a competitor, rebuild an app they use, or implement features inspired by an existing tool. Trigger when someone says "I want to build something like X", "clone this app", "replicate this product", or describes features they've seen in another product they want to implement. Always use this skill alongside system-reverse-engineering for the full cloning workflow.
---

# Blackbox App Cloning

## Cloning Philosophy

You don't need source code to clone an app. Everything you need is observable:
- The UX tells you **what** to build
- The network traffic tells you **how** data flows
- User reviews tell you **what matters** and what to skip
- The performance profile tells you **how to architect** it

Your goal isn't a pixel-perfect copy — it's a product that delivers the same user outcomes, possibly better.

---

## Phase 1: Reconnaissance (Before You Write a Line of Code)

### 1.1 Full Feature Mapping
Spend 2–4 hours as a power user. Document:
- Every screen and state
- Every user action available
- Every piece of data shown
- Every integration available
- Behavior at account limits

Use the `saas-feature-extraction` skill to structure this phase.

### 1.2 Network Traffic Analysis
With DevTools open, perform every major action. Capture:
```
Action: [user action]
Request: [METHOD /path + key headers]
Request body: [abbreviated key fields]
Response: [abbreviated key fields]
Latency: [ms]
```

### 1.3 Identify the Core Loop
Every product has a core loop — the thing users do repeatedly.

```
[Entry] → [Core Action] → [Value Delivered] → [Reason to Return]
```

Example (Notion):
```
[Create page] → [Write content] → [Organized knowledge] → [Search/reference later]
```

Your clone must nail the core loop before anything else.

---

## Phase 2: Technical Deconstruction

### 2.1 Data Model Inference
From network responses, reconstruct all entities and relationships.
Use the `database-schema-inference` skill for this phase.

### 2.2 API Contract Mapping
Document every endpoint you observed:
```markdown
| Method | Path | Purpose | Key Request Fields | Key Response Fields |
|--------|------|---------|-------------------|-------------------|
| POST | /api/docs | Create doc | title, workspace_id | id, created_at |
| GET | /api/docs/:id | Get doc | - | id, title, blocks[], owner |
```

### 2.3 Real-time Behavior Detection
- Instant updates without refresh → WebSockets or SSE
- Optimistic UI (update before server confirms) → note for frontend
- Collaborative editing → likely OT or CRDT (complex; plan accordingly)

### 2.4 AI Feature Identification
- Latency > 1s on user actions → likely an AI call
- "Generating..." states → streaming AI response
- Variable output on same input → generative AI, not deterministic logic

---

## Phase 3: Build Planning

### 3.1 Complexity Classification

Classify every feature:

| Complexity | Definition | Timeline |
|-----------|-----------|---------|
| **Simple** | CRUD + display | Hours |
| **Medium** | State machine, business logic, async job | Days |
| **Hard** | Real-time, AI integration, complex data model | Weeks |
| **Very Hard** | Collaborative, inference engine, ML model | Months |

### 3.2 MVP Scope Decision

Rule: **Build the core loop only.**

Ask for every feature: "Would a user leave after one week if this was missing?"
- Yes → MVP
- No → Post-launch

### 3.3 Cut List (Deliberate Exclusions)
Explicitly list what you're NOT building in v1:
```markdown
## Intentionally Excluded from v1:
- Real-time collaboration (use turn-based or auto-save instead)
- Native mobile apps (responsive web only)
- API access (internal only first)
- [Feature X] — complexity not justified by user value at launch
```

---

## Phase 4: Implementation Order

### The Right Build Order

```
1. Data model (schema + migrations)
2. Core API endpoints (CRUD for main entities)
3. Authentication (sign up, log in, session)
4. Core UI (main screens, no polish)
5. Core loop working end-to-end
6. ← STOP and validate with real users ←
7. Supporting features (based on feedback)
8. Polish, performance, edge cases
```

**Never do UI polish before core loop works.**

### Implementation Shortcuts

| Original Product | Clone Shortcut |
|-----------------|---------------|
| Custom auth system | Clerk / Auth0 |
| Custom payments | Stripe |
| File storage | S3 / Cloudflare R2 |
| Email | Resend / SendGrid |
| Search | Algolia / Postgres FTS |
| Real-time | Supabase Realtime / Pusher |
| AI features | OpenAI / Anthropic API |
| Background jobs | Inngest / Trigger.dev |

---

## Phase 5: Differentiation Layer

A clone that's identical to the original is a commodity. Add at least one meaningful differentiator:

| Differentiation Type | Example |
|---------------------|---------|
| Price | 50% cheaper, better free tier |
| UX | Simpler, faster, fewer clicks |
| Niche | Same product for one specific vertical |
| AI depth | Original uses AI cosmetically; you make it core |
| Integration | Native integration original doesn't have |
| Speed | Significantly faster performance |
| Open source | Build trust via transparency |

---

## Clone Project Checklist

### Recon complete:
- [ ] All features documented
- [ ] Network API mapped
- [ ] Data model inferred
- [ ] Core loop identified
- [ ] Tech stack identified
- [ ] Complexity estimates done

### Planning complete:
- [ ] MVP scope defined
- [ ] Cut list created
- [ ] Tech stack chosen
- [ ] Build order set
- [ ] Differentiator defined

### Build milestones:
- [ ] Schema + migrations done
- [ ] Auth working
- [ ] Core loop working end-to-end
- [ ] Real user feedback gathered
- [ ] V1 shipped
