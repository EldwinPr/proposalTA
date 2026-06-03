# Prompt — Laravel Customer Tax Fields

Paste into the Laravel repo's AI assistant (Orchestrator role).

---

```
Act as the Orchestrator. Create an issue and draft a plan.md for this:

Add 4 nullable tax fields to the `customers` table for Finance Senlab integration:

| Field | Type |
|-------|------|
| `npwp` | varchar(30) nullable |
| `nik` | varchar(20) nullable |
| `tax_name` | varchar(255) nullable |
| `tax_address` | text nullable |

Finance Senlab mirrors `customers` 1:1 by ULID — it reads these fields from the SO detail API response to avoid double entry. Include them in the `customer` object on `GET /api/sales-orders/{id}`.

Scope: migration, model fillable, customer form (optional section), API resource.
Out of scope: NPWP validation, making fields required, any Finance-side changes.

Acceptance criteria:
- [ ] Migration adds 4 nullable columns to `customers`
- [ ] Fields appear in customer create/edit form
- [ ] `GET /api/sales-orders/{id}` includes all 4 fields under `customer`
- [ ] Existing records unaffected
```
