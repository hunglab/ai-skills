# Skill: backend-builder

## Description
A standardized, 5-phase iterative prompting strategy for building production-grade, distributed backend services (Node.js/TypeScript, Python, Go, etc.) with explicit support for event-driven patterns, database entities, background workers, and fault tolerance.

## Activation Rule
When the user invokes "Use skill 'backend-builder'" or calls `@backend-builder` followed by a step number (e.g., "Step 1", "Step 3"), adhere strictly to the guidelines and prompt structure defined for that phase.

---

## Skill Instructions & Phase Definitions

### Phase 1: Infrastructure & Environment Setup
**Trigger:** `Step 1` or `Infrastructure`
**Goal:** Initialize container orchestration, directory layout, base runtime config, and environment variables. Do NOT generate business logic.

**Execution Prompt Template:**
> Project: [Project Name / Description]
> Stack: [Language/Framework] + [Database] + [Broker/Queue]
> Task: Create the base infrastructure for this project.
> Requirements:
> 1. Generate a root `docker-compose.yml` containing:
>    - Database engine (PostgreSQL, MySQL, MongoDB)
>    - Message broker/cache (RabbitMQ, Kafka, Redis)
> 2. Define a clean, modular folder layout.
> 3. Provide `.env.example` with standard connection variables.
> 4. Output configuration files, runtime scripts, and setup commands only.

---

### Phase 2: Data Modeling & Core Repository Layer
**Trigger:** `Step 2` or `Database`
**Goal:** Establish database entities, schemas, migrations, and typed data transfer objects (DTOs) before writing endpoints.

**Execution Prompt Template:**
> Stack: [ORM Name e.g., TypeORM, Prisma, SQLAlchemy]
> Task: Create data models and core repository access layers for [Domain / Module].
> Requirements:
> 1. Define schema/entity for `[EntityName]` with fields:
>    - Primary key, status enums, JSON metadata, `createdAt`, `updatedAt`.
> 2. Generate input validation schemas / DTOs (e.g., `class-validator`, Pydantic).
> 3. Implement core CRUD repository methods.
> 4. Ensure strong typing and validation error handling.

---

### Phase 3: Inbound Layer (API / Message Producer)
**Trigger:** `Step 3` or `Producer`
**Goal:** Build public-facing REST/GraphQL endpoints that validate requests, write initial state to DB, and publish async events.

**Execution Prompt Template:**
> Task: Implement API endpoint and Event Producer for [Feature e.g., Order Creation].
> Requirements:
> 1. Create [POST/PUT/GET] `/api/v1/[endpoint]` taking `[Input DTO]`.
> 2. Route/Controller logic:
>    - Validate incoming request body.
>    - Persist record to DB with status `[INITIAL_STATUS]`.
>    - Dispatch event `[event_name]` to queue/topic `[queue_name]`.
> 3. Return an immediate `[201/200]` response with payload `{ id, status }` without blocking on queue processing.
> 4. Provide unit tests for controller validation and event dispatching.

---

### Phase 4: Async Processing Layer (Consumer / Worker)
**Trigger:** `Step 4` or `Consumer`
**Goal:** Construct background workers that process queue jobs safely with manual ACKs, idempotency checks, and dead-letter routing.

**Execution Prompt Template:**
> Task: Implement Async Worker/Consumer for event `[event_name]`.
> Requirements:
> 1. Subscribe to queue/topic `[queue_name]`.
> 2. Configure reliability guarantees:
>    - Disable Auto-ACK (use Manual Acknowledgements).
>    - Implement **Idempotency** via [Redis / Distributed Lock] on `[unique_key]` to prevent duplicate execution.
> 3. Execution logic:
>    - Process async workload.
>    - Update database record status to `[FINAL_STATUS]`.
>    - Call explicit ACK on success.
> 4. Fault tolerance:
>    - Catch runtime errors.
>    - Call NACK without requeue (Route to Dead Letter Queue / DLQ) on unrecoverable failures.

---

### Phase 5: Verification, Integration & Edge-Case Testing
**Trigger:** `Step 5` or `Testing`
**Goal:** Generate integration scripts and failure-injection tests to verify network resilience, duplicates, and edge cases.

**Execution Prompt Template:**
> Task: Write integration tests and verification scripts for [Feature Name].
> Requirements:
> 1. Provide an E2E test script (curl, pytest, or HTTP client) executing the full flow.
> 2. Verify resilience against:
>    - Worker crash during processing (re-delivery check).
>    - Duplicate event emission (idempotency check).
>    - Malformed payload execution (Dead Letter Queue routing).
> 3. Output terminal commands for monitoring queue depth, logs, and database state.