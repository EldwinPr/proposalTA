# Laravel API Endpoint Request — Customer List (FEAT-003)

Finance Senlab needs to read customer master data from Laravel instead of managing it locally. Two endpoints are needed.

---

## Endpoints Needed

### 1. `GET /api/customers`

Returns all customers. Response must be wrapped in a `data` key (same pattern as the SO list).

**Expected response:**
```json
{
  "data": [
    {
      "id": "01jt4k2m3n5p6q7r8s9t0uvwxy",
      "name": "PT. Sentral Sistem Kalibrasi",
      "npwp": "01.234.567.8-901.000",
      "nik": ""
    },
    {
      "id": "01jt4k2m3n5p6q7r8s9t0uvwxz",
      "name": "CV. Maju Bersama",
      "npwp": "",
      "nik": "3273012345670001"
    }
  ]
}
```

Field spec:

| Field | Type | Notes |
|---|---|---|
| `id` | string | Customer UUID/ULID from Laravel — Finance Senlab stores this as `erp_id` |
| `name` | string | Legal company/person name |
| `npwp` | string | NPWP formatted with dots/dashes, or empty string `""` if none |
| `nik` | string | 16-digit NIK for individual taxpayers, or empty string `""` if none |

---

### 2. `GET /api/customers/{id}`

Returns a single customer with full tax detail. **Return the object directly — no `data` wrapper** (same pattern as `GET /api/sales-orders/{id}`).

**Expected response:**
```json
{
  "id": "01jt4k2m3n5p6q7r8s9t0uvwxy",
  "name": "PT. Sentral Sistem Kalibrasi",
  "npwp": "01.234.567.8-901.000",
  "nik": "",
  "tax_name": "PT. SENTRAL SISTEM KALIBRASI",
  "tax_address": "Jl. Raya Pasar Minggu No. 18, Jakarta Selatan 12780"
}
```

Field spec: all fields from the list, plus:

| Field | Type | Notes |
|---|---|---|
| `tax_name` | string | Name as printed on NPWP/SKT — may differ from `name`, or empty string `""` |
| `tax_address` | string | Address as registered on NPWP, or empty string `""` |

---

## Auth

Same Bearer token as the existing SO endpoints (`Authorization: Bearer {ERP_API_KEY}`).

---

## Notes

- `npwp`, `nik`, `tax_name`, `tax_address` — if not filled yet on the customer record, return empty string `""` not `null`. Go's JSON decoder will treat `null` as a zero value but it avoids ambiguity.
- Finance Senlab does **not** write back to these endpoints — read-only from our side.
- `id` is the critical link field. Finance Senlab stores it as `erp_id` on its local `CustomerCredit` record to avoid re-matching by name/NPWP on every request.
