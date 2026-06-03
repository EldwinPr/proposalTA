# Entity Status Definitions

Reference for all domain entity statuses. Source of truth: TASK-02.

---

## Sales Order (`sales_orders.status`)

| Status | Description |
|---|---|
| `open` | SO created, awaiting processing |
| `proses` | Sampling in progress |
| `invoicing` | Finance has created an invoice |
| `pembayaran` | Invoice paid |
| `selesai` | All fulfilled, closed |
| `batal` | Cancelled |

---

## Sales Order Detail (`sales_order_details.status`)

| Status | Description |
|---|---|
| `open` | SOD created, not yet scheduled |
| `persiapan` | Pengambilan planned, containers being prepared |
| `pengambilan` | Sample actively being collected in the field |
| `disimpan` | Sample received and stored at the lab |
| `diuji_sebagian` | At least one sample under this SOD has finished testing, but not all |
| `penyeliaan` | All samples submitted by analyst — awaiting penyelia review |
| `selesai` | All samples accepted by penyelia — truly final |
| `batal` | Cancelled |

---

## Pengambilan (`pengambilan.status`)

| Status | Description |
|---|---|
| `persiapan` | Pengambilan created, not yet started |
| `pengambilan` | COC issued, field sampling underway |
| `selesai` | All sampling done |
| `batal` | Cancelled |

---

## Sample (`samples.status`)

| Status | Description |
|---|---|
| `open` | Sample record created (SO generated) |
| `persiapan` | Container assigned, being prepared |
| `pengambilan` | Being collected in the field |
| `disimpan` | Received and stored at the lab (set on Terima Sampel) |
| `diuji_sebagian` | At least one `pengujian` ticket for this sample is selesai, but not all |
| `penyeliaan` | All `pengujian` tickets in penyeliaan — awaiting penyelia review |
| `selesai` | All `pengujian` tickets accepted by penyelia — truly final |
| `tolak` | Rejected at lab intake |
| `batal` | Cancelled |

---

## Sample Parameter (`sample_parameter.status`)

Source of truth for the individual parameter lifecycle.

| Status | Description |
|---|---|
| `open` | Created with the SO |
| `persiapan` | Pengambilan planned |
| `pengambilan` | Being collected in the field |
| `disimpan` | Sample received at lab, awaiting queue |
| `pengujian` | Pengujian ticket taken by analyst |
| `penyeliaan` | Analyst submitted result — awaiting penyelia review (buffer) |
| `selesai` | Accepted by penyelia — truly final state |
| `tolak` | Rejected by penyelia — needs rework |
| `batal` | Cancelled |

---

## Pengujian (`pengujian.status`)

One ticket = one sample × one machine.

| Status | Description |
|---|---|
| `open` | Ticket created at Terima Sampel, in queue |
| `pengujian` | Analyst has taken the ticket (`analyst_id` set) |
| `penyeliaan` | All linked `sample_parameter` rows submitted — awaiting penyelia review |
| `selesai` | All linked `sample_parameter` rows accepted by penyelia — truly final |
