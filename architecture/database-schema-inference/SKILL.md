---
name: database-schema-inference
description: Infer, design, or reconstruct database schemas from product behavior, API responses, or feature descriptions. Use this skill when designing a data model for a new product, reverse-engineering a competitor's schema, translating product requirements into tables and relationships, or evaluating database design decisions. Trigger when someone asks "how should I structure my database", "what tables do I need", "design a schema for X", or provides a product description and needs a data model.
---

# Database Schema Inference

## Inference Method: From Product to Schema

Every product feature maps to data. Work backwards from what the product does to what it must store.

### Step 1: Identify Entities
An entity is any "thing" the product tracks over time.

**Signal phrases → entities:**
- "users can create [X]" → `X` is an entity
- "each [X] has many [Y]" → X and Y are entities with a relationship
- "[X] belongs to [workspace]" → workspace is an entity; X has a foreign key
- "track the history of [X]" → entity + events/versions table

### Step 2: Define Attributes
For each entity, ask:
- What identifies it? → `id` (primary key)
- What describes it? → name, description, type, status
- Who owns it? → `user_id`, `workspace_id`
- When was it created/modified? → `created_at`, `updated_at`
- Can it be deleted? → `deleted_at` (soft delete) or hard delete
- Does it have settings? → `settings JSONB` (for flexible config)

### Step 3: Map Relationships
- **One-to-many**: User has many Projects → `projects.user_id`
- **Many-to-many**: Projects have many Tags → `project_tags(project_id, tag_id)` join table
- **One-to-one**: User has one Profile → `profiles.user_id UNIQUE`
- **Hierarchical**: Comments on Comments → `comments.parent_id`

---

## Core SaaS Schema Patterns

### Multi-Tenant Foundation
```sql
-- Organizations / Workspaces (top-level tenant)
CREATE TABLE organizations (
  id           TEXT PRIMARY KEY DEFAULT gen_id('org'),
  name         TEXT NOT NULL,
  slug         TEXT UNIQUE NOT NULL,
  plan         TEXT NOT NULL DEFAULT 'free',  -- free, pro, enterprise
  settings     JSONB NOT NULL DEFAULT '{}',
  created_at   TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at   TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  deleted_at   TIMESTAMPTZ
);

-- Users
CREATE TABLE users (
  id           TEXT PRIMARY KEY DEFAULT gen_id('usr'),
  email        TEXT UNIQUE NOT NULL,
  name         TEXT,
  avatar_url   TEXT,
  created_at   TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  last_seen_at TIMESTAMPTZ
);

-- Organization Members (many-to-many with role)
CREATE TABLE organization_members (
  org_id     TEXT NOT NULL REFERENCES organizations(id),
  user_id    TEXT NOT NULL REFERENCES users(id),
  role       TEXT NOT NULL DEFAULT 'member',  -- owner, admin, member, viewer
  invited_by TEXT REFERENCES users(id),
  joined_at  TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  PRIMARY KEY (org_id, user_id)
);
```

### Audit & Events Pattern
```sql
-- Append-only event log
CREATE TABLE events (
  id           TEXT PRIMARY KEY DEFAULT gen_id('evt'),
  org_id       TEXT NOT NULL REFERENCES organizations(id),
  user_id      TEXT REFERENCES users(id),
  resource_type TEXT NOT NULL,  -- 'project', 'document', etc.
  resource_id  TEXT NOT NULL,
  action       TEXT NOT NULL,   -- 'created', 'updated', 'deleted', 'shared'
  changes      JSONB,           -- before/after delta
  metadata     JSONB,
  created_at   TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE INDEX events_resource ON events(resource_type, resource_id);
CREATE INDEX events_org_time ON events(org_id, created_at DESC);
```

### Versioning / History Pattern
```sql
-- Current state
CREATE TABLE documents (
  id           TEXT PRIMARY KEY,
  org_id       TEXT NOT NULL,
  title        TEXT NOT NULL,
  current_version INT NOT NULL DEFAULT 1,
  created_at   TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at   TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

-- Version history
CREATE TABLE document_versions (
  id           TEXT PRIMARY KEY,
  document_id  TEXT NOT NULL REFERENCES documents(id),
  version      INT NOT NULL,
  content      TEXT NOT NULL,
  created_by   TEXT REFERENCES users(id),
  created_at   TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  UNIQUE(document_id, version)
);
```

### Tagging / Labeling Pattern
```sql
CREATE TABLE tags (
  id     TEXT PRIMARY KEY,
  org_id TEXT NOT NULL REFERENCES organizations(id),
  name   TEXT NOT NULL,
  color  TEXT,
  UNIQUE(org_id, name)
);

-- Generic tag join table (reuse across resource types)
CREATE TABLE resource_tags (
  tag_id        TEXT NOT NULL REFERENCES tags(id),
  resource_type TEXT NOT NULL,
  resource_id   TEXT NOT NULL,
  created_by    TEXT REFERENCES users(id),
  created_at    TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  PRIMARY KEY (tag_id, resource_type, resource_id)
);
```

### AI Content / Embeddings Pattern
```sql
CREATE TABLE ai_generations (
  id           TEXT PRIMARY KEY DEFAULT gen_id('gen'),
  org_id       TEXT NOT NULL,
  user_id      TEXT REFERENCES users(id),
  resource_type TEXT,          -- what resource triggered this
  resource_id  TEXT,
  model        TEXT NOT NULL,  -- 'gpt-4o', 'claude-3-5-sonnet', etc.
  prompt_hash  TEXT,           -- hash of input for caching
  input_tokens INT,
  output_tokens INT,
  cost_usd     NUMERIC(10, 6),
  latency_ms   INT,
  status       TEXT NOT NULL DEFAULT 'pending',
  output       TEXT,
  error        TEXT,
  created_at   TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

-- For vector search (using pgvector)
CREATE TABLE embeddings (
  id           TEXT PRIMARY KEY,
  org_id       TEXT NOT NULL,
  resource_type TEXT NOT NULL,
  resource_id  TEXT NOT NULL,
  content      TEXT NOT NULL,   -- the text that was embedded
  embedding    vector(1536),    -- OpenAI ada-002 dimensions
  model        TEXT NOT NULL,
  created_at   TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE INDEX embeddings_vector ON embeddings 
  USING ivfflat (embedding vector_cosine_ops);
```

---

## Inference from API Responses

Given an API response, reconstruct the schema:

```json
// Input: API response
{
  "id": "task_abc",
  "title": "Build login page",
  "status": "in_progress",
  "priority": "high",
  "assignee": { "id": "usr_xyz", "name": "Alice" },
  "project_id": "proj_123",
  "labels": ["frontend", "auth"],
  "due_date": "2024-02-01",
  "completed_at": null,
  "created_at": "2024-01-15T10:00:00Z"
}
```

→ Inferred schema:
```sql
CREATE TABLE tasks (
  id           TEXT PRIMARY KEY,    -- "task_abc"
  title        TEXT NOT NULL,
  status       TEXT NOT NULL,       -- enum: 'todo', 'in_progress', 'done'
  priority     TEXT,                -- enum: 'low', 'medium', 'high', 'urgent'
  assignee_id  TEXT REFERENCES users(id),  -- nested object → FK
  project_id   TEXT NOT NULL REFERENCES projects(id),
  due_date     DATE,
  completed_at TIMESTAMPTZ,         -- null = not done; set = done
  created_at   TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

-- labels is an array → many-to-many
CREATE TABLE task_labels (
  task_id  TEXT NOT NULL REFERENCES tasks(id),
  label    TEXT NOT NULL,
  PRIMARY KEY (task_id, label)
);
-- or if labels are a shared entity: use resource_tags pattern
```

---

## Schema Design Checklist

- [ ] Every table has a primary key (prefixed string ID recommended)
- [ ] Every table has `created_at` TIMESTAMPTZ
- [ ] Mutable tables have `updated_at` TIMESTAMPTZ
- [ ] Soft-deletable tables have `deleted_at` TIMESTAMPTZ (nullable)
- [ ] Multi-tenant tables have `org_id` with an index
- [ ] Enums are stored as strings, not integers
- [ ] Foreign keys are named `[table_singular]_id`
- [ ] Indexes on all foreign keys
- [ ] Indexes on all columns used in WHERE clauses
- [ ] Composite indexes for common multi-column queries
- [ ] JSONB used sparingly (for truly variable/flexible data only)
- [ ] No unbounded arrays stored in columns (use join tables)
