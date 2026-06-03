# Laravel API Endpoint Request — Finance Senlab Integration

Hi, I need the following API endpoints from the Laravel app so Finance Senlab can create invoices from Sales Orders without a direct DB connection.

---

## Context

Finance Senlab is a separate accounting app. It needs to:
1. Show a list of Sales Orders that are ready to be invoiced
2. Fetch full detail of a specific SO to pre-fill an invoice
3. Notify Laravel when an invoice has been created for an SO

---

## Endpoints Needed

### 1. `GET /api/sales-orders`

Returns a list of all Sales Orders.

**Later** (once status is implemented): add `?status=finished` filter. For now return all.

**Expected response:**
```json
[
  {
    "id": "ulid-string",
    "no_so": "SO/2026/0042",
    "customer_name": "PT. Example",
    "grand_total": 5000000,
    "status": "current-status-value",
    "created_at": "2026-03-01T00:00:00Z"
  }
]
```

---

### 2. `GET /api/sales-orders/{id}`

Returns full detail for one SO, joined with its quotation's financial data.

**Expected response:**
```json
{
  "id": "ulid-string",
  "no_so": "SO/2026/0042",
  "status": "current-status-value",

  "customer": {
    "name": "PT. Example",
    "npwp": "01.234.567.8-901.000",
    "nik": "",
    "tax_name": "PT. Example Indonesia",
    "tax_address": "Jl. Sudirman No. 1, Jakarta"
  },

  "quotation": {
    "quotation_number": "Q/2026/0100",
    "no_po": "PO-CLIENT-001",
    "term_of_payment": "30 days"
  },

  "line_items": [
    {
      "description": "Kalibrasi Alat X — Paket Standard",
      "qty": 1,
      "unit_price": 1500000,
      "subtotal": 1500000
    }
  ],

  "additional_costs": [
    {
      "name": "Biaya Transport",
      "total": 200000
    }
  ],

  "grand_total": 1700000
}
```

> **Notes:**
> - `line_items.description` — please combine `produk_uji.nama` + `paket.nama` into a readable string, or return them separately and we'll combine on our end. Whatever is easier.
> - `customer.npwp`, `tax_name`, `tax_address` — needed for Indonesian tax invoice (Faktur Pajak). If not on the customer record yet, return empty string.
> - `grand_total` should match sum of `line_items[].subtotal` + `additional_costs[].total`

---

### 3. `POST /api/sales-orders/{id}/mark-invoiced`

Called by Finance Senlab immediately after creating an invoice for this SO. Sets the SO status to `invoicing` (or whatever the correct status is on your side).

**Request body:** none required (the ID in the URL is enough)

**Expected response:**
```json
{ "message": "ok" }
```

Or just HTTP 200/204 — we don't use the body.

---

## Auth

What auth mechanism should we use to call these endpoints?
- [ ] Bearer token (Laravel Sanctum / Passport)
- [ ] API key in header (e.g. `X-API-Key: ...`)
- [ ] Internal network only (no auth needed)
- [ ] Other: ___________

Please share the token/key once decided.

---

## Base URL

What is the base URL for the Laravel API?
- Local dev: `http://___________`
- Production: `https://___________`

---

## Questions

1. Does the `customers` table already have `npwp`, `tax_name`, `tax_address`? If not, where is that data stored?
2. For `line_items.description` — is it easier to return a combined string, or separate `produk_uji` + `paket` fields?
3. What is the correct status string to set on `mark-invoiced`? (checking your `status` enum on `sales_orders` or `quotations`)
