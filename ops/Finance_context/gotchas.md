# Gotchas — Known Failure Modes

Running list of things that look right but aren't. Add an entry whenever something bites you during implementation. Feed confirmed patterns back here after closing an issue.

---

## Go / GORM

- **Soft deletes don't cascade.** GORM's `DeletedAt` only marks the row — related records are not touched. Handle cascades manually in the service layer.
- **`db.Save()` updates all fields, including zero values.** Use `db.Model(&item).Updates(map)` when doing partial updates to avoid wiping fields.
- **`gorm:"-"` fields are ignored on read too.** If you need a computed field populated from a JOIN, use a raw query or a separate struct — not a tagged `-` field on the main model.
- **`BeforeCreate` does not run on batch inserts.** ULID generation via `BeforeCreate` only fires on single-record `db.Create(&item)`. For bulk inserts, generate ULIDs manually before calling `db.CreateInBatches`.
- **SQLite vs PostgreSQL search.** `Paginate` uses `LIKE` on SQLite and `ILIKE` on Postgres. Test search behaviour against the right dialect — they behave differently on case and unicode.
- **`db.First` panics on no result if you ignore the error.** Always check `errors.Is(err, gorm.ErrRecordNotFound)` explicitly.

## Svelte 5

- **`$effect` runs twice in development.** Svelte 5 runs effects twice in dev mode to catch side-effect bugs. Don't use effect run-count as a signal.
- **`$state` arrays need full reassignment to trigger reactivity on item mutation.** Mutating `arr[0].field = x` does not trigger a re-render. Reassign: `arr = arr.map(...)` or use `$state` on each item.
- **`{#each}` without a key causes wrong DOM reuse.** Always provide a key: `{#each items as item (item.id)}`.
- **`$props()` destructuring must happen at the top of `<script>`.** Destructuring inside a function or block will not be reactive.
- **`on:click` is Svelte 4 syntax — it silently does nothing in Svelte 5.** Use `onclick={handler}` attribute syntax. No warning is thrown, so this is easy to miss.

## Architecture

- **Controllers that access `db` directly break the layer contract.** All DB access goes through repositories. If a controller needs data, it calls a service — never `db.Find(...)` inline.
- **Balanced ledger is only enforced in `JournalService`.** If you create a `Journal` by calling `db.Create` directly (e.g. in a migration or seed), no balance check runs. Always go through the service.
- **`CompanyTransaction` is auto-created by `syncBankFromEntries`.** Never create `CompanyTransaction` records manually — they are a side effect of journal entry creation. Creating them manually will desync the bank statement.
- **`Voucher.ID` is an external int64, not a ULID.** Do not call `GenerateULID()` on Voucher. The ID comes from the external system.

## API / HTTP

- **`response.status === 204` returns an empty body.** The `api<T>()` wrapper handles this, but raw `fetch` calls will fail to parse JSON on 204. Always use the wrapper.
- **Cookie auth is stateful — no invalidation on password change.** The session token is the User ID. If a user is deleted and re-created with the same ID (impossible with ULIDs, but worth knowing), the old cookie still works until cleared.

## External API (Laravel ERP)

- **Wrapper mismatch also silently produces zero values.** If you deserialize `{"id":"...","no_so":"..."}` into `struct { Data SODetail \`json:"data"\` }`, the result is a zero-value SODetail with no error. The list endpoint wraps in `{"data":[...]}` but the detail endpoint returns the object directly — they are not symmetric. Verify each endpoint's envelope shape independently.
- **JSON field name mismatches silently produce zero values.** Go's `encoding/json` does not error on unknown or missing fields — if a struct tag doesn't exactly match the API response key, the field unmarshals as zero/empty with no warning. Verify tags against actual API payloads before assuming a field is empty. (`SOCustomer.Name` had `json:"nama"` instead of `json:"name"` and was bitten by this.)
- **`MarkSOInvoiced` is best-effort — failure doesn't roll back the invoice.** It is called after the local transaction commits. If Laravel is down, the SO stays in its previous status but the invoice already exists locally. The two systems can desync silently; reconcile manually or add a retry mechanism later.
