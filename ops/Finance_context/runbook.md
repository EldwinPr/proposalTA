# Runbook — Common Implementation Recipes

Step-by-step guides for the most repeated patterns in this codebase. Follow these exactly to stay consistent with existing code.

---

## Add a New Entity (full stack)

### 1. Model (`app/models/{domain}.go`)
```go
type MyEntity struct {
    ID        string         `gorm:"primaryKey;type:char(26)" json:"id"`
    // ... fields with json + search tags
    CreatedAt time.Time      `json:"created_at"`
    UpdatedAt time.Time      `json:"updated_at"`
    DeletedAt gorm.DeletedAt `gorm:"index" json:"-"`
}

func (m *MyEntity) BeforeCreate(tx *gorm.DB) error {
    if m.ID == "" { m.ID = GenerateULID() }
    return nil
}
```
- Tag searchable string fields with `search:"true"`
- Use `gorm:"-"` for computed fields (never written to DB)
- Use `gorm:"<-:false"` for read-only computed columns

### 2. Register AutoMigrate (`main.go`)
Add `&models.MyEntity{}` to the `db.AutoMigrate(...)` call.

### 3. Repository (`app/repositories/myentity_repository.go`)
```go
type MyEntityRepository struct {
    repositories.BaseRepository[models.MyEntity]
}

func NewMyEntityRepository(db *gorm.DB) *MyEntityRepository {
    return &MyEntityRepository{BaseRepository: repositories.NewBaseRepository[models.MyEntity](db)}
}
```
Only add methods beyond CRUD if the base doesn't cover the use case.

### 4. Service (`app/services/myentity_service.go`)
```go
type MyEntityService struct {
    services.BaseService[models.MyEntity]
}

func NewMyEntityService(db *gorm.DB, repo *repositories.MyEntityRepository) *MyEntityService {
    return &MyEntityService{BaseService: services.NewBaseService[models.MyEntity](db, repo)}
}
```
Multi-step writes always use `s.Transaction(func(tx *gorm.DB) error { ... })`.

### 5. Controller (`app/controllers/myentity_controller.go`)
```go
type MyEntityController struct{ svc *services.MyEntityService }

func NewMyEntityController(svc *services.MyEntityService) *MyEntityController {
    return &MyEntityController{svc: svc}
}
```
Parse request → call service → write JSON response. Never touch `db` directly.

### 6. Routes (`app/routes/myentity.go` + `app/routes.go`)
```go
// app/routes/myentity.go
func RegisterMyEntityRoutes(mux *http.ServeMux, mw *middleware.Middleware, ctrl *controllers.MyEntityController) {
    mux.HandleFunc("GET /api/myentities", mw.Auth(ctrl.Index))
    mux.HandleFunc("POST /api/myentities", mw.Auth(ctrl.Create))
}
```
Wire in `app/routes.go`: instantiate repo → service → controller → call `RegisterMyEntityRoutes`.

### 7. Frontend page (`web/src/pages/MyEntity.svelte`)
- Fetch data with `api<T>('/api/myentities')`
- Register the route in `web/src/App.svelte`
- Before writing: `mcp__svelte__get-documentation` for any Svelte 5 feature used

---

## Add a New API Endpoint to an Existing Entity

1. Add method to the controller
2. Add the route line in `app/routes/{domain}.go`
3. No other files need touching unless the endpoint requires new service logic

---

## Add a New Field to an Existing Model

1. Add the field to the struct in `app/models/`
2. GORM AutoMigrate will add the column on next startup — no migration file needed
3. If the field is searchable, add `search:"true"`
4. Update the frontend form/display as needed
5. If the field affects an existing service calculation (e.g. tax total), update the service

---

## Add a New Frontend Page

1. Create `web/src/pages/MyPage.svelte`
2. Register in `web/src/App.svelte`:
   ```js
   import MyPage from './pages/MyPage.svelte'
   // in routes object:
   '/my-path': MyPage
   ```
3. Add nav link in `web/src/lib/Sidebar.svelte` under the appropriate group
4. Use `api<T>()` for all HTTP calls — never raw `fetch`
5. Use existing shared components — see `ops/context/map.yaml` for the full inventory
6. Run `mcp__svelte__svelte-autofixer` after writing

### Shared component quick-reference

| Need | Component |
|---|---|
| Paginated table with search/sort | `DataTable` — pass `endpoint` for server-side or `items` for client-side |
| Status / label chip | `Badge` — types: `default success error warning blue cyan violet rose amber indigo primary` |
| Action button | `Button` — variants: `primary outline ghost` |
| Centred modal overlay | `Modal` — props: `isOpen title subtitle`, slots: `children footer` |
| Confirm before destructive action | `ConfirmDialog` |
| Money formatting | `formatCurrency(n)` from `lib/utils` |
| Date formatting | `formatDate(s)` from `lib/utils` |
| HTTP calls | `api<T>(path, options)` from `lib/api` |
| Toast notifications | `toast.success/error/info(msg)` from `lib/toast.svelte` |

---

## Add a Maker-Checker Flow to an Existing Entity

1. Staff action creates an `AdjustmentTicket` with:
   - `Type`: `CREATE | UPDATE | VOID`
   - `TargetTable`: the table name string
   - `TargetID`: the record ID (null for CREATE)
   - `Payload`: JSON of the proposed change
2. Manager approves via `TicketService.Approve(id, approver)`
3. `TicketService` reads the payload, applies it in a transaction, sets ticket `POSTED`
4. Never apply the payload change directly — always go through `TicketService`

---

## Add a New External API Call (Laravel)

1. Add a typed method to `app/remote/client.go`
2. Define the response struct in `app/remote/types.go` (no GORM tags — these are API response shapes only)
3. Call the client method from a service — never from a controller directly
4. Add any new env vars to `.env.example`
5. Double-check json tags against the actual API payload field names — mismatches silently zero-out fields (see gotchas)

---

## Close an Issue

```
1. ops/issues/{id}/plan.md      → status: done
2. ops/issues.yaml              → status: done, fill summary
3. ops/log.md                   → append [DONE][ID] summary — YYYY-MM-DD
4. ops/active.json              → next issue or {"issue": null, "status": null}
```
