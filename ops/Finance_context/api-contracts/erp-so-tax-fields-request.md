---
id: ERP-API-001
title: Move tax fields (dpp, ppn, ppn_rate) inside quotation object — GET /api/sales-orders/{id}
type: api-change
priority: high
requested_by: Finance Senlab
affects_endpoint: GET /api/sales-orders/{id}
---

## Context

The endpoint currently returns a top-level `tax` object alongside `quotation`. Since DPP and PPN are derived from the quotation, Finance Senlab would prefer them nested inside `quotation` — all price-related data in one place, easier to trace back to the source.

The current response (confirmed via live test):
```json
{
  "grand_total": 130557280,
  "tax": { "dpp": 116569000, "ppn": 13988280, "ppn_rate": 0.12 },
  "quotation": { "quotation_number": "...", "no_po": "...", "term_of_payment": "..." }
}
```

## Requested Change

Move `dpp`, `ppn`, `ppn_rate` into the `quotation` object and remove the top-level `tax` key:

```json
{
  "id": "...",
  "no_so": "...",
  "status": "...",
  "grand_total": 130557280,

  "quotation": {
    "quotation_number": "00001/SSL/QUO/IV/26",
    "no_po": "324234234",
    "term_of_payment": "...",
    "dpp": 116569000,
    "ppn": 13988280,
    "ppn_rate": 0.12
  },

  "customer": { ... },
  "line_items": [ ... ],
  "additional_costs": [ ... ]
}
```

## Why

- `dpp` and `ppn` belong to the quotation — they should live there, not as a sibling
- Finance Senlab references it as `so.quotation.dpp` which is self-documenting
- Avoids having two separate objects (`tax` + `quotation`) that both describe the same document

## Notes

- `grand_total` stays at the top level — it equals `quotation.dpp + quotation.ppn`
- PPh23 is NOT needed from the ERP — Finance Senlab applies it as an optional toggle per invoice
- The `tax` top-level key can be removed once `quotation` has the fields

## No Change Needed Elsewhere

All other fields (`customer`, `line_items`, `additional_costs`, `grand_total`) stay as-is.
