# Coding Conventions

## Backend (Go)

### Architecture Layers
Strictly follow **Controller → Service → Repository**. Controllers never touch `*gorm.DB` directly. Repositories never contain business logic.

```
HTTP request → Controller (parse) → Service (logic + tx) → Repository (GORM)
```

### File Naming
- Controllers: `app/controllers/{entity}_controller.go`
- Services: `app/services/{entity}_service.go`
- Repositories: `app/repositories/{entity}_repository.go`
- Models: `app/models/{domain}.go` (group related models in one file)
- Routes: `app/routes/{domain}.go` + registered in `app/routes.go`

### Models
- All primary keys are ULID strings (`char(26)`), generated via `GenerateULID()` in `BeforeCreate`.
- Exception: `Voucher.ID` is `int64` (external system FK — no ULID).
- All mutable models use GORM soft deletes (`gorm.DeletedAt`).
- Computed/aggregated fields use `gorm:"-"` or `gorm:"<-:false"` and are never written to DB.
- Use `json:"-"` for fields that must never be serialized (e.g. `Password`).

### Generics
- `BaseRepository[T]` provides: `FindAll`, `FindByID`, `Create`, `Update`, `Delete`, `Paginate`.
- `BaseService[T]` provides: `GetByID`, `Transaction`.
- Extend via embedding; override only what needs domain-specific behaviour.

### Search
Tag model fields with `search:"true"` to include them in the generic paginated search. Column name is resolved by priority: `gorm:"column:"` → `json` tag → snake_case field name.

### Transactions
All multi-step writes must run inside `service.Transaction(func(tx *gorm.DB) error { ... })`. Never commit partial state.

### Balanced Ledger
Every journal creation must validate `sum(Debit) == sum(Credit)` before committing. Services enforce this; controllers must not bypass it.

### Clearance Levels
```
0  = Staff     — read-only most resources
10 = Manager   — approve/reject tickets, post payments
20 = Developer — full access (bypasses clearance checks)
```
Apply via `mw.RequireClearance(level, handler)` in route registration.

### Error Responses
Return plain text errors with appropriate HTTP status codes. JSON error bodies use `{"error": "message"}`.

### Maker-Checker (AdjustmentTicket)
All edits to financial records go through `AdjustmentTicket`:
1. Staff creates a ticket (`PENDING`) with a JSON payload of the proposed change.
2. Manager/Dev approves → service applies the payload and sets `POSTED`.
3. Rejection sets `REJECTED`; no data is mutated.

---

## Frontend (Svelte 5)

### Routing
Hash-based SPA via `svelte-spa-router`. Pages live in `web/src/pages/`. Routes registered in `web/src/App.svelte`.

### API Calls
All HTTP calls go through `web/src/lib/api.ts:api<T>(path, options)`. Never use `fetch` directly in components.

### Auth State
Session state is in `web/src/lib/auth.svelte.ts`. Check `$auth.user` for the logged-in user and `$auth.user.clearance` for role gating in the UI.

### Component Style
- Use Svelte 5 runes (`$state`, `$derived`, `$effect`) — not legacy stores inside components.
- Keep pages thin: data fetching + layout only. Extract repeated UI into `web/src/lib/` components.

---

## General

- **No auto-increment IDs** anywhere (except external Voucher FKs).
- **No raw SQL** in controllers or services — use GORM query builder.
- **No `fmt.Println`** in production paths — use structured logging or omit.
- **XLSX export** uses the `excelize` library; column order must match `JournalEntry` sheet spec.
