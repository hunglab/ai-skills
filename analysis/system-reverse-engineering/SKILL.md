---
name: system-reverse-engineering
description: Deconstruct how any software product or system works from the outside in — without access to source code. Use this skill when the user wants to understand how a product is built, what tech stack it uses, how its data model is structured, or how its features are implemented. Trigger when someone says "how does X work under the hood", "what's their architecture", "how do they implement Y feature", or wants to clone or understand a competitor. Always use this skill before attempting to clone or rebuild any product.
---

# System Reverse Engineering

## Mental Model: The Onion

Every product is an onion. You peel layers from the outside in:

```
Layer 1: UX surface (visible to everyone)
Layer 2: API behavior (observable with network tools)
Layer 3: Data model (inferred from API shapes)
Layer 4: Business logic (inferred from behavior + edge cases)
Layer 5: Infrastructure (inferred from performance + job postings + tech signals)
Layer 6: Architecture patterns (inferred from all the above)
```

You almost never need to go all the way to Layer 6. Most cloning requires only Layers 1–4.

---

## Step 1: UX Surface Mapping

**Goal**: Catalog every screen, flow, and interaction.

### What to document:
- All navigation paths and entry points
- Every form, input, and output element
- State transitions (what changes when user does X)
- Loading states, empty states, error states
- User roles and permission boundaries
- Pricing tiers and feature gating

### Tools:
- Manual walkthrough + screenshots
- Loom/screen recording for flows
- Figma or Whimsical to map flows

### Output: Feature inventory + user journey map

---

## Step 2: API Behavior Analysis

**Goal**: Understand the data contract between frontend and backend.

### Method:
1. Open browser DevTools → Network tab
2. Perform every major action in the product
3. Record: URL structure, HTTP method, request payload, response shape
4. Note: authentication headers, pagination patterns, error formats

### What to look for:
```
GET  /api/v2/workspaces/:id/members     → team data model
POST /api/v1/completions                → AI integration pattern
GET  /search?q=...&type=...&page=...    → search + pagination design
WS   wss://app.example.com/live/:id    → realtime architecture
```

### Signals:
- `/v1/`, `/v2/` in URLs → they version their API
- GraphQL endpoint → flexible querying, complex data model
- Webhooks documented → event-driven architecture
- OAuth endpoints → third-party integrations
- `/admin/` routes → internal tooling exists

---

## Step 3: Data Model Inference

**Goal**: Reconstruct the likely database schema.

### Method:
From API responses, extract entity shapes. Every JSON object is likely a database table (or a view over one).

### Example inference:
```json
// API response
{
  "id": "proj_abc123",
  "name": "My Project",
  "owner_id": "usr_xyz",
  "workspace_id": "ws_def",
  "created_at": "...",
  "settings": { "visibility": "private" },
  "members": [...]
}
```
→ Table: `projects(id, name, owner_id, workspace_id, created_at, settings_json)`
→ Relationship: projects belong_to workspaces, projects belong_to users (owners)
→ Join table: `project_members`

### Look for:
- ID prefixes (`proj_`, `usr_`, `ws_`) → namespaced IDs, likely single DB
- Nested objects → either joins or JSON columns
- `_at` timestamps → event audit trail exists
- `status` enums → finite state machine in business logic
- Soft deletes → `deleted_at` field instead of hard deletes

---

## Step 4: Business Logic Inference

**Goal**: Understand the rules and workflows the product enforces.

### Method: Probe edge cases deliberately.
- What happens when you hit limits?
- What's allowed vs. blocked at each permission tier?
- What triggers notifications or async jobs?
- What can't be undone?

### Patterns to look for:
| Behavior | Likely Implementation |
|----------|----------------------|
| Instant search results | Client-side filter or indexed full-text search |
| Results appear after 2–3s | Server-side AI or heavy query |
| "Processing..." state | Async job queue (Sidekiq, BullMQ, Celery) |
| Real-time updates | WebSockets or SSE |
| File processing | Background worker + object storage |
| Email at specific times | Cron job or scheduled task |

---

## Step 5: Tech Stack Detection

### Signals:
- **Job postings**: Most reliable signal for backend tech ("5 years Rails experience")
- **Error messages**: Stack traces leak framework names
- **Response headers**: `X-Powered-By`, `Server`, `Set-Cookie` naming patterns
- **JavaScript bundle**: `__NEXT_DATA__` → Next.js; `__nuxt` → Nuxt; `window.Ember` → Ember
- **CSS classes**: Tailwind utility classes, Bootstrap grid classes
- **Analytics/monitoring**: Sentry DSN, Datadog RUM, Segment write key in JS
- **BuiltWith / Wappalyzer**: Browser extensions that detect tech stack automatically

### Common Stack Patterns:
```
Startup (fast):     Next.js + Supabase + Vercel + OpenAI
Mid-size:           React + Node/FastAPI + Postgres + AWS
Enterprise:         React + Java/Go + Postgres + Kubernetes
AI-native:          Next.js + Python backend + Pinecone + OpenAI
```

---

## Step 6: Synthesize Architecture Diagram

Draw the inferred architecture:

```
[Browser/Mobile]
      ↕ HTTPS
[CDN / Edge (Vercel/Cloudflare)]
      ↕
[API Server (REST or GraphQL)]
      ↕              ↕              ↕
[Primary DB]   [Cache (Redis)]  [AI Service]
(Postgres)                      (OpenAI API)
      ↕
[Background Jobs]    [Object Storage]
(queued tasks)       (files/assets)
      ↕
[Email/Notification Service]
```

---

## Output Template

```markdown
## [Product Name] — Reverse Engineering Report

### Feature Inventory
- [list all features observed]

### Inferred Data Model
- [Entity: fields]

### API Patterns
- [method + URL + purpose]

### Tech Stack (inferred)
- Frontend: 
- Backend: 
- Database: 
- AI: 
- Infra: 

### Architecture Summary
[paragraph]

### Implementation Complexity
- Simple (1-2 devs, 1-2 weeks): [features]
- Medium (small team, 1-2 months): [features]  
- Hard (requires specialization): [features]

### Key Unknowns
- [things you couldn't infer]
```
