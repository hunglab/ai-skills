---
name: rapid-product-rebuild
description: Ship a working product in days to weeks using a high-velocity build approach. Use this skill when the user needs to build fast, is doing a product sprint, wants to go from idea to working software quickly, or is rebuilding a product under time pressure. Trigger when someone says "build this fast", "I need this in a week", "what's the fastest way to ship X", or describes a product they want to launch as quickly as possible. Always apply when speed is the primary constraint.
---

# Rapid Product Rebuild

## The Speed Equation

```
Speed = (Clarity of scope) × (Right tools) × (No premature optimization)
           ÷ (Scope creep) × (Wrong abstractions) × (Perfectionism)
```

Slow builders make decisions twice — once in planning, once in code. Fast builders make them once, in writing, before touching the keyboard.

---

## Phase 0: Pre-Build Decisions (Do This Before Coding — 1–2 Hours)

### 0.1 The Single Sentence
Write one sentence that describes what the product does:
> "[Product] helps [user] do [outcome] by [mechanism]."

If you can't write this, you're not ready to build.

### 0.2 The One-Screen Test
What is the ONE screen that, if it worked perfectly, would be enough to impress your first 10 users? Build that first.

### 0.3 Stack Decision (Pick Once, Don't Revisit)
| Question | Answer | Then use |
|----------|--------|---------|
| Mostly CRUD? | Yes | Next.js + Prisma + Supabase |
| Heavy AI? | Yes | Next.js + FastAPI + OpenAI |
| Real-time? | Yes | Add Supabase Realtime or Pusher |
| Mobile-first? | Yes | React Native + Expo |

Use the most boring, familiar stack. Speed comes from fluency, not novelty.

### 0.4 The 5-Day Plan
```
Day 1: Schema + Auth + scaffolding
Day 2: Core data flow (create/read main entity)  
Day 3: Core workflow (the thing users actually do)
Day 4: Basic UI pass (usable, not beautiful)
Day 5: Deploy + share with 5 real users
```

---

## Speed Patterns

### Pattern 1: Schema-First Development
Define your entire data model before writing application code. Every screen and feature follows from the schema.

1. Write all tables + relationships (use `database-schema-inference` skill)
2. Run migrations
3. Seed with realistic test data
4. Now write application code — the hard decisions are already made

### Pattern 2: API-First, UI-Second
Build and test every API endpoint before building UI. Test with curl or Postman.

Benefits:
- Logic is testable without UI
- UI developers (or AI tools) can work in parallel
- Forces clean separation of concerns

### Pattern 3: Fake It Till You Make It
For complex features, fake the hard part first:

| Real implementation | Fast fake |
|--------------------|-----------|
| Real-time sync | Polling every 5s |
| AI-powered search | Simple text match |
| PDF generation | Render HTML, print to PDF |
| Email sequences | Send immediately, delay logic later |
| Payment flow | Mock checkout, add Stripe later |
| File processing | Block upload until processed |

Launch with fakes. Replace with real implementations after validation.

### Pattern 4: Prebuilt Everything
Never build from scratch what you can configure:

| Functionality | Prebuilt Solution |
|--------------|------------------|
| Auth + user management | Clerk |
| Payments + billing | Stripe + billing portal |
| Email | Resend + email templates |
| File upload + storage | UploadThing or S3 direct upload |
| Rich text editing | TipTap or Lexical |
| Tables + grids | TanStack Table |
| Charts | Recharts or Tremor |
| Admin panel | AdminJS or custom with Shadcn |
| Forms | React Hook Form + Zod |
| AI | Vercel AI SDK |
| Background jobs | Trigger.dev or Inngest |

### Pattern 5: UI Component Libraries
Use a component system — don't write custom CSS from scratch.

Recommended: **Shadcn/ui** (copy-paste components, full control)
Alternative: Tremor (dashboard-focused), DaisyUI (Tailwind-based)

---

## Daily Build Rhythm

```
Morning (30 min):
- Review what you built yesterday
- Write today's tasks as concrete deliverables (not "work on X" but "user can create a project")
- Identify the one thing that, if done, makes today a success

Build session:
- One feature at a time, end-to-end
- Commit when a feature works (not before, not after)
- Write TODO comments for cleanup — never stop to clean mid-feature

End of day (20 min):
- Demo what you built to yourself
- Note what's broken or ugly
- Write tomorrow's task list
```

---

## Blockers & How to Handle Them

| Blocker | Response |
|---------|----------|
| Can't figure out the right architecture | Build the dumbest thing that works. Refactor after validation. |
| Bug you can't fix in 30 min | Hard-code the happy path, file the bug, move on |
| Feature scope expanding | Write it in the cut list, not the codebase |
| Performance issues | Add a TODO, ship anyway, optimize only if users care |
| "I should use a better tool for this" | Finish with current tool, migrate after launch |

**The mantra**: "Shipped and wrong beats unshipped and perfect."

---

## Deployment Checklist (Day 5)

### Minimum to ship:
- [ ] App is deployed (Vercel / Railway / Fly.io)
- [ ] Production environment variables set
- [ ] Database is persistent (not ephemeral)
- [ ] Auth works on production
- [ ] At least one real email sent to a real user
- [ ] Error tracking enabled (Sentry free tier)
- [ ] You've used the app yourself for 10 minutes as a real user

### Do NOT block launch for:
- [ ] Perfect mobile responsiveness
- [ ] Onboarding flow
- [ ] Edge case handling
- [ ] Analytics beyond basic error tracking
- [ ] SEO
- [ ] API documentation
- [ ] Loading skeleton states
