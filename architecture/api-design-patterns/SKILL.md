---
name: api-design-patterns
description: Design clean, consistent, and scalable APIs. Use this skill when designing REST or GraphQL APIs, writing API documentation, reviewing API contracts, versioning APIs, or handling common API design challenges like pagination, filtering, error handling, and authentication. Trigger when someone says "how should I design this API", "what's the right endpoint structure", "help me with API design", or is building any backend service with a public or internal API.
---

# API Design Patterns

## REST API Design Principles

### Resource Naming
- Use nouns, not verbs: `/users` not `/getUsers`
- Plural for collections: `/projects`, `/members`
- Nested for relationships: `/workspaces/:id/projects`
- Max 2 levels of nesting; deeper = use query params

```
✅ GET /workspaces/abc/projects
❌ GET /workspaces/abc/projects/xyz/tasks/123/comments/456/replies
✅ GET /comments/456/replies  (flatten deep nesting)
```

### HTTP Methods
| Method | Use | Idempotent? | Body? |
|--------|-----|-------------|-------|
| GET | Retrieve | ✅ | ❌ |
| POST | Create | ❌ | ✅ |
| PUT | Replace entirely | ✅ | ✅ |
| PATCH | Partial update | ❌ | ✅ |
| DELETE | Remove | ✅ | ❌ |

### Status Codes
```
200 OK              → Success (GET, PATCH, PUT)
201 Created         → Resource created (POST)
204 No Content      → Success, no body (DELETE)
400 Bad Request     → Invalid input (client error)
401 Unauthorized    → Not authenticated
403 Forbidden       → Authenticated but not allowed
404 Not Found       → Resource doesn't exist
409 Conflict        → State conflict (duplicate, version mismatch)
422 Unprocessable   → Valid format, invalid semantics
429 Too Many Reqs   → Rate limited
500 Server Error    → Your fault
```

---

## Request & Response Conventions

### Response Envelope
```json
// Single resource
{
  "data": { "id": "proj_123", "name": "My Project", ... },
  "meta": { "request_id": "req_abc" }
}

// Collection
{
  "data": [ {...}, {...} ],
  "meta": {
    "total": 243,
    "page": 2,
    "per_page": 25,
    "has_more": true
  }
}

// Error
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Name is required",
    "field": "name",
    "request_id": "req_abc"
  }
}
```

### Consistent Field Conventions
```json
{
  "id": "proj_abc123",          // prefixed, string (not integer)
  "created_at": "2024-01-15T10:30:00Z",  // ISO 8601 UTC
  "updated_at": "2024-01-20T14:22:00Z",
  "deleted_at": null,           // null if not deleted (soft delete)
  "status": "active",           // enum strings, not integers
  "owner_id": "usr_xyz",        // foreign keys use _id suffix
  "metadata": {}                // escape hatch for extensibility
}
```

---

## Pagination Patterns

### Offset Pagination (simple, good for small datasets)
```
GET /projects?page=2&per_page=25

Response:
{
  "data": [...],
  "meta": { "total": 243, "page": 2, "per_page": 25 }
}
```
❌ Inconsistent if data changes between pages; slow at high offsets

### Cursor Pagination (correct choice for large/live data)
```
GET /projects?limit=25&cursor=eyJpZCI6IjEyMyJ9

Response:
{
  "data": [...],
  "meta": {
    "next_cursor": "eyJpZCI6IjE0OCJ9",
    "has_more": true
  }
}
```
✅ Stable pagination even if data changes; efficient at any offset

---

## Filtering & Sorting

```
GET /projects?status=active&owner_id=usr_xyz&created_after=2024-01-01
GET /projects?sort=created_at&order=desc
GET /projects?fields=id,name,status    (sparse fieldsets)
GET /projects?q=search+term            (full-text search)
```

### Filter naming conventions:
- Equality: `?status=active`
- Comparison: `?created_after=`, `?updated_before=`, `?price_min=`, `?price_max=`
- Array: `?status[]=active&status[]=paused` or `?status=active,paused`
- Nested: `?filter[user.role]=admin`

---

## Authentication Patterns

### API Keys (for server-to-server)
```
Authorization: Bearer sk_live_abc123...
```
- Prefix keys by env: `sk_live_`, `sk_test_`
- Hash before storing (never store raw)
- Support key rotation without downtime
- Scope keys to specific permissions

### JWT (for user sessions)
```
Authorization: Bearer eyJhbGciOiJIUzI1NiJ9...
```
- Short expiry (15min–1hr) + refresh tokens
- Include: `sub` (user ID), `tenant_id`, `role`, `exp`, `iat`
- Never store sensitive data in JWT payload (it's base64, not encrypted)

---

## Versioning

### URL versioning (recommended for public APIs)
```
/api/v1/projects
/api/v2/projects
```

### Header versioning (cleaner URLs)
```
API-Version: 2024-01-15
```

### Versioning rules:
- **Non-breaking changes** (additive): No version bump needed
  - Adding new fields to responses
  - Adding new optional request fields
  - Adding new endpoints
- **Breaking changes**: Require new version
  - Removing/renaming fields
  - Changing field types
  - Changing endpoint behavior

---

## Rate Limiting

### Headers to return:
```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 834
X-RateLimit-Reset: 1704067200   (Unix timestamp)
Retry-After: 30                 (on 429)
```

### Rate limit strategies:
- Per API key
- Per user + tier (free = 100/hr, pro = 10k/hr)
- Per endpoint (AI endpoints rate-limited separately)
- Sliding window preferred over fixed window

---

## Webhooks Design

```json
// Webhook payload structure
{
  "id": "evt_abc123",
  "type": "project.created",
  "created_at": "2024-01-15T10:30:00Z",
  "api_version": "2024-01-01",
  "data": {
    "object": { ...full resource... }
  }
}
```

### Delivery guarantees:
- Sign payloads: `X-Signature: sha256=<hmac>`
- Retry with exponential backoff (1min, 5min, 30min, 2hr, 24hr)
- Store delivery attempts + response codes
- Allow users to replay failed events

---

## API Documentation Standard

Every endpoint should document:
```
[Method] [Path]

Summary: [one line]

Request:
  Path params: [name, type, required, description]
  Query params: [name, type, required, description]
  Body: [JSON schema or example]

Response:
  200: [example response]
  400: [example error]
  401: ...

Example:
  Request: curl -X POST ...
  Response: { ... }
```

Use: OpenAPI 3.0 spec → auto-generate from code annotations where possible
