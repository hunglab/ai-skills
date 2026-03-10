---
name: saas-architecture-patterns
description: Design and evaluate SaaS product architectures using proven patterns. Use this skill when planning how to build a SaaS product, choosing between architectural approaches, designing multi-tenant systems, handling scaling decisions, or structuring a new backend. Trigger when someone asks "how should I architect X", "what's the best way to build a SaaS", "how does multi-tenancy work", or is making foundational technical decisions for a product.
---

# SaaS Architecture Patterns

## Core SaaS Architecture Layers

```
┌──────────────────────────────────────────────┐
│  Presentation Layer                          │
│  (Web App, Mobile App, Embeds, API consumers)│
├──────────────────────────────────────────────┤
│  API Gateway / BFF Layer                     │
│  (Auth, Rate limiting, Routing)              │
├──────────────────────────────────────────────┤
│  Application Layer                           │
│  (Business logic, Workflows, AI calls)       │
├──────────────────────────────────────────────┤
│  Data Layer                                  │
│  (Primary DB, Cache, Search, Object Storage) │
├──────────────────────────────────────────────┤
│  Async Layer                                 │
│  (Job queues, Event bus, Webhooks)           │
├──────────────────────────────────────────────┤
│  Infrastructure Layer                        │
│  (Cloud provider, CDN, Monitoring)           │
└──────────────────────────────────────────────┘
```

---

## Multi-Tenancy Patterns

Choose based on isolation requirements and scale:

### Pattern 1: Shared DB, Shared Schema
All tenants in same tables. `tenant_id` column on every table.

```sql
SELECT * FROM projects WHERE tenant_id = 'acme' AND id = 123;
```

✅ Simple to build, cheap to operate, easy to cross-query
❌ No data isolation, noisy neighbor risk, harder compliance (HIPAA, SOC2)

**Best for**: B2C or SMB SaaS with low compliance requirements

### Pattern 2: Shared DB, Separate Schemas
One database, one schema per tenant.

```sql
SET search_path TO acme_corp;
SELECT * FROM projects WHERE id = 123;
```

✅ Logical isolation, easier compliance, simple migrations
❌ Schema sprawl at scale (100+ tenants = complexity), no row-level cross-tenant queries

**Best for**: Mid-market SaaS, moderate compliance needs

### Pattern 3: Separate Database per Tenant
Each enterprise customer gets their own database.

✅ True isolation, compliance-friendly, per-tenant backups
❌ Expensive, complex provisioning, hard to run cross-tenant analytics

**Best for**: Enterprise-only, regulated industries (healthcare, finance, gov)

### Hybrid (Most Common at Scale)
SMB tenants on shared schema. Enterprise tenants on dedicated databases.

---

## Authentication & Authorization Patterns

### Auth stack:
```
Authentication (who are you?)  → Clerk / Auth0 / Supabase Auth / custom JWT
Authorization (what can you do?) → RBAC / ABAC / custom middleware
```

### RBAC (Role-Based Access Control)
```
User → has Role → Role has Permissions → Permission gates Action
```

```
Roles:        owner, admin, editor, viewer, guest
Permissions:  read, write, delete, invite, billing
Resources:    workspace, project, document, member, settings
```

Store as: `role_permissions(role, resource, action)` table

### Resource-Level Permissions (for advanced use cases)
```
user_id + resource_type + resource_id + permission_level
```
Allows: "Alice can edit Doc A but only view Doc B"

---

## API Design Patterns

### RESTful Resource API (default choice)
```
GET    /workspaces/:id/projects        → list projects
POST   /workspaces/:id/projects        → create project
GET    /projects/:id                   → get project
PATCH  /projects/:id                   → update project
DELETE /projects/:id                   → delete project
```

### Action-Based Endpoints (for non-CRUD operations)
```
POST /projects/:id/publish
POST /documents/:id/summarize
POST /invoices/:id/send
```

### Versioning strategy:
- URL versioning: `/api/v1/`, `/api/v2/` — simple, visible
- Header versioning: `API-Version: 2024-01-01` — cleaner URLs
- Default: URL versioning for public APIs

---

## Background Job Patterns

### When to use async jobs:
- AI API calls (latency unpredictable)
- Email sending
- File processing (PDF, CSV, images)
- Third-party webhook delivery
- Batch operations
- Report generation

### Job queue options by scale:

| Scale | Tool | Notes |
|-------|------|-------|
| Early | Supabase pg_cron / Inngest | Serverless, no infra |
| Growing | BullMQ (Redis) | Node.js standard |
| At scale | Celery (Python) / Sidekiq (Ruby) | Battle-tested |
| Large scale | SQS + Lambda | AWS-native |

### Job design principles:
- **Idempotent**: Safe to run twice (network retries happen)
- **Atomic**: Either fully completes or fully rolls back
- **Observable**: Log start, end, duration, errors
- **Retryable**: Auto-retry with exponential backoff

---

## Caching Strategy

```
Request → [Cache hit?] → Yes → Return cached
                      → No  → Compute/fetch → Store in cache → Return
```

### What to cache:
| Data type | TTL | Where |
|-----------|-----|-------|
| User session | 24h | Redis |
| API responses (stable) | 5–60min | Redis / CDN |
| DB query results | 1–5min | Redis |
| Static assets | 1yr | CDN |
| AI outputs | varies | DB + Redis |

### Cache invalidation strategies:
- **TTL-based**: Expires automatically (simple, may serve stale)
- **Event-based**: Invalidate on write (fresh, complex)
- **Version-based**: Append version to key (safest, most overhead)

---

## SaaS Stack Templates

### Lean Startup Stack (< 1,000 users)
```
Frontend:  Next.js → Vercel
Backend:   Next.js API Routes + Prisma
Auth:      Clerk
Database:  Supabase (Postgres)
AI:        OpenAI API
Jobs:      Inngest
Email:     Resend
Payments:  Stripe
Monitoring: Sentry + Vercel Analytics
```

### Growth Stack (1K–100K users)
```
Frontend:  Next.js / React → Vercel / AWS CloudFront
Backend:   Node.js (Express/Fastify) or FastAPI
Auth:      Auth0 or custom JWT
Database:  RDS Postgres + Redis (ElastiCache)
AI:        OpenAI + Anthropic + custom fine-tunes
Jobs:      BullMQ or Celery
Email:     SendGrid / Postmark
Payments:  Stripe
Search:    Algolia or Postgres FTS
Storage:   S3
Monitoring: Datadog or Grafana stack
```

### Enterprise Stack (100K+ users)
```
Frontend:  React → AWS CloudFront
Backend:   Go / Java microservices
Auth:      Okta / custom IdP + SAML/SCIM
Database:  Aurora Postgres + Redis cluster + per-tenant DBs
AI:        Multi-model with fallback + fine-tuned models
Jobs:      SQS + Lambda / Kafka
Email:     SES
Payments:  Stripe + invoicing
Search:    Elasticsearch
Storage:   S3 with lifecycle policies
Monitoring: Full Datadog stack + PagerDuty
```
