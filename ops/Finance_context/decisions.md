# Architecture Decision Records (ADRs)

---

## ADR-001 — ULID Primary Keys
**Status:** Accepted  
**Date:** ~2024

**Decision:** Use ULID strings (`char(26)`) as primary keys for all application-owned models instead of auto-increment integers.

**Reason:** ULIDs are sortable, URL-safe, and collision-resistant without a DB sequence. They allow IDs to be generated in the application layer (in `BeforeCreate`) rather than requiring a DB round-trip.

**Exception:** `Voucher.ID` is `int64` because it mirrors an external system's BigInt PK.

---

## ADR-002 — Monolith: Go Serves Compiled Svelte
**Status:** Accepted  
**Date:** ~2024

**Decision:** The Go binary serves the compiled Svelte SPA from `./static/`. There is no separate frontend server in production.

**Reason:** Simplifies deployment — one binary, one port (`8080`). The SPA fallback (`404 → index.html`) enables hash-based client-side routing. Development uses separate hot-reload servers (`air` + `vite`) that are merged only on build.

---

## ADR-003 — Maker-Checker via AdjustmentTicket
**Status:** Accepted  
**Date:** ~2024

**Decision:** All mutations to financial records (invoices, journals, transactions) must go through an `AdjustmentTicket`. No direct edits are allowed.

**Reason:** Audit trail and four-eyes control required by Indonesian accounting compliance. The ticket stores the proposed JSON payload; approval atomically applies it and records the approver.

---

## ADR-004 — Balanced Ledger Enforcement in Service Layer
**Status:** Accepted  
**Date:** ~2024

**Decision:** `JournalService` validates `sum(Debit) == sum(Credit)` before any journal is committed. This check lives in the service, not the DB constraint.

**Reason:** Go-level validation provides better error messages than DB triggers, and the double-entry invariant is a business rule rather than a storage rule.

---

## ADR-005 — Cookie-Based Session Auth (No JWT)
**Status:** Accepted  
**Date:** ~2024

**Decision:** Authentication uses an `HttpOnly` `session_token` cookie whose value is the `User.ID`. The middleware looks up the user from DB on every request.

**Reason:** Simple to implement for an internal tool. No token expiry complexity. The DB lookup is cheap given the small user base.

**Trade-off:** Stateful sessions — logging out one session doesn't invalidate others unless the user ID changes. Acceptable for internal use.

---

## ADR-006 — Generic BaseRepository and BaseService
**Status:** Accepted  
**Date:** ~2024

**Decision:** Common CRUD and pagination are provided by `BaseRepository[T]` and `BaseService[T]` using Go generics. Specific repositories embed or compose these.

**Reason:** Eliminates copy-paste boilerplate across 10+ entities. The `search:"true"` struct tag drives dynamic WHERE clauses in `Paginate` without code duplication.

---

## ADR-007 — Hash-Based SPA Routing
**Status:** Accepted  
**Date:** ~2024

**Decision:** Frontend uses `svelte-spa-router` with hash (`#/path`) routing instead of history-mode.

**Reason:** Avoids the need to configure the Go server for every client-side route. The server only needs a single `index.html` fallback for unknown paths, which already exists.

---

## ADR-008 — SQLite for Dev, PostgreSQL for Production
**Status:** Accepted  
**Date:** ~2024

**Decision:** Local development uses SQLite (`system.db`). Production uses PostgreSQL via Docker Compose.

**Reason:** SQLite requires zero infrastructure for a dev environment. GORM's dialect abstraction allows the same code to target both. The `Paginate` method uses `ILIKE` for Postgres and `LIKE` for SQLite automatically.
