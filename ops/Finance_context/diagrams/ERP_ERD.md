# ERD

> Generated from migrations. Entities in the ERD design that are not yet implemented are listed at the bottom.

```mermaid
erDiagram
    %% ─── CUSTOMER ───────────────────────────────────────────
    customers {
        ulid id PK
        string nama
        string bidang_usaha
        string email_perusahaan
        string nomor_telpon_perusahaan
        string status_aktif
    }
    customer_contacts {
        ulid id PK
        ulid customer_id FK
        string nama
        string posisi
        string nomor_telp
        string email
    }
    customer_addresses {
        ulid id PK
        ulid customer_id FK
        string nama
        string alamat
        string provinsi
        string kota_kabupaten
        string kode_pos
    }

    %% ─── PRODUCT KNOWLEDGE ──────────────────────────────────
    produk_uji {
        ulid id PK
        string nama
        string kode
    }
    regulasi {
        ulid id PK
        ulid produk_uji_id FK
        string nama
        string kode
    }
    paket {
        ulid id PK
        ulid produk_uji_id FK
        ulid regulasi_id FK
        string nama
        string kode
    }
    paket_parameter {
        ulid id PK
        ulid paket_id FK
        ulid parameter_id FK
        string ambang_batas
        string satuan
    }
    paket_sentral {
        ulid id PK
        string nama
    }
    paket_sentral_regulasi {
        ulid id PK
        ulid paket_sentral_id FK
        ulid regulasi_id FK
    }
    parameter {
        ulid id PK
        string kode
        string parameter
        ulid reference_method_id FK
        ulid alat_id FK
        ulid wadah_id FK
        integer harga
        enum jenis_pengerjaan
        string status_akreditasi
    }
    reference_methods {
        ulid id PK
        string nama
    }
    alats {
        ulid id PK
        string nama
    }
    wadahs {
        ulid id PK
        string nama
    }
    metode_samplings {
        ulid id PK
        ulid produk_uji_id FK
        string nama
    }

    %% ─── SALES ──────────────────────────────────────────────
    quotations {
        ulid id PK
        string quotation_number
        ulid customer_id FK
        ulid customer_address_id FK
        bigint sales_id FK
        ulid customer_contact_id FK
        enum status_terima
        boolean status_approval
        double grand_total
        string no_po
        string file_po
        string term_of_payment
        boolean pakai_konsultan
    }
    quotation_details {
        ulid id PK
        ulid quotation_id FK
        string group_id
        ulid produk_uji_id FK
        ulid paket_id FK
        ulid paket_sentral_id FK
        ulid metode_sampling_id FK
        ulid lokasi_sampling FK
        string titik_sampling
        integer jumlah_titik
        integer frekuensi_sampling
        boolean is_composite_titik
        boolean is_composite_frekuensi
        string tipe_sampling
        boolean express
        double harga_parameter
        double sub_total
    }
    quotation_detail_parameters {
        ulid id PK
        ulid quotation_detail_id FK
        ulid parameter_id FK
        string ambang_batas
        string satuan
        double harga_asli
    }
    quotation_detail_regulations {
        ulid id PK
        ulid quotation_detail_id FK
        ulid regulasi_id FK
    }
    quotation_additional_costs {
        ulid id PK
        ulid quotation_id FK
        ulid additional_cost_id FK
        double kuantitas
        double harga
        double diskon
        double total
    }
    additional_costs {
        ulid id PK
        string nama
    }

    %% ─── OPERATIONS ─────────────────────────────────────────
    sales_orders {
        ulid id PK
        ulid quotation_id FK
        ulid customer_id FK
        string no_so
        integer qty
    }
    sales_order_details {
        ulid id PK
        ulid sales_order_id FK
        ulid quotation_detail_id FK
        ulid pengambilan_id FK
        string kode_sampling
        enum tipe_sampling
        integer titik_sampling
        string frekuensi
        boolean is_composite_titik
        boolean is_composite_frekuensi
        enum status
        boolean sudah_diambil
    }
    pengambilan {
        ulid id PK
        ulid sales_order_id FK
        bigint petugas_id FK
        ulid customer_contact_id FK
        integer pengambilan_nomor
        date tanggal_sampling
        text delevery_address
        text sampling_address
        text certificate_address
        text invoice_address
        enum tipe_sampling
        integer total_waktu
        string satuan_waktu
    }
    samples {
        ulid id PK
        ulid sales_order_details_id FK
        ulid quotation_detail_id FK
        enum status
        enum tipe_sampling
    }
    sample_parameter {
        ulid id PK
        ulid sales_order_details_id FK
        ulid quotation_detail_id FK
        ulid sample_id FK
        ulid parameter_id FK
        string ambang_batas
        string satuan
        boolean is_insitu
    }
    users {
        bigint id PK
        string name
        string email
    }

    %% ─── RELATIONSHIPS ───────────────────────────────────────
    customers ||--o{ customer_contacts : "has"
    customers ||--o{ customer_addresses : "has"
    customers ||--o{ quotations : "has"

    produk_uji ||--o{ regulasi : "has"
    produk_uji ||--o{ paket : "has"
    produk_uji ||--o{ metode_samplings : "has"
    regulasi ||--o{ paket : "has"
    paket ||--o{ paket_parameter : "has"
    paket_sentral ||--o{ paket_sentral_regulasi : "has"
    parameter ||--o{ paket_parameter : "in"
    parameter }o--|| reference_methods : "uses"
    parameter }o--|| alats : "uses"
    parameter }o--|| wadahs : "uses"

    quotations }o--|| customers : ""
    quotations }o--|| customer_addresses : ""
    quotations }o--|| customer_contacts : ""
    quotations }o--|| users : "sales"
    quotations ||--o{ quotation_details : "has"
    quotations ||--o{ quotation_additional_costs : "has"
    quotation_details }o--|| produk_uji : ""
    quotation_details }o--|| paket : ""
    quotation_details }o--|| paket_sentral : ""
    quotation_details }o--|| metode_samplings : ""
    quotation_details }o--|| customer_addresses : "lokasi"
    quotation_details ||--o{ quotation_detail_parameters : "has"
    quotation_details ||--o{ quotation_detail_regulations : "has"
    quotation_detail_parameters }o--|| parameter : ""
    quotation_detail_regulations }o--|| regulasi : ""
    quotation_additional_costs }o--|| additional_costs : ""

    sales_orders }o--|| quotations : ""
    sales_orders }o--|| customers : ""
    sales_orders ||--o{ sales_order_details : "has"
    sales_orders ||--o{ pengambilan : "has"
    sales_order_details }o--|| quotation_details : ""
    sales_order_details }o--o| pengambilan : ""
    sales_order_details ||--o{ samples : "has"
    sales_order_details ||--o{ sample_parameter : "has"
    pengambilan }o--|| users : "petugas"
    pengambilan }o--|| customer_contacts : ""
    samples }o--|| parameter : ""
    sample_parameter }o--|| parameter : ""
    sample_parameter }o--|| samples : ""
```

## Planned Schema Changes

Column additions planned in issue plans — not yet migrated.

### `samples` table — UC-18/19, UC-24
| Column | Type | Plan | Purpose |
|---|---|---|---|
| `kode_sampling` | varchar nullable | UC-18/19 | scan lookup key; copy from SOD at creation |
| `received_at` | timestamp nullable | UC-18/19 | set on QR scan; drives queue readiness |
| `catatan_abnormalitas` | text nullable | UC-18/19 | abnormality notes recorded on intake |

### `sales_order_details` table — UC-24
| Column | Type | Plan | Purpose |
|---|---|---|---|
| `express` | boolean default false | UC-24 | denormalized from `quotation_details.express` for queue sorting |

### `sample_parameter` table — UC-24
| Column | Type | Plan | Purpose |
|---|---|---|---|
| `status` | varchar(20) default 'antrian' | UC-24 | `antrian → pengujian → selesai` |
| `analyst_id` | ulid nullable FK→users | UC-24 | analyst who took the ticket |
| `hasil` | text nullable | UC-24 | test result |
| `tested_at` | timestamp nullable | UC-24 | when result was entered |

### `parameter` table — UC-24
| Column | Type | Plan | Purpose |
|---|---|---|---|
| `durasi_hari` | integer nullable | UC-24 | wait days after receipt before sample enters queue |

---

## Not Yet Implemented

New tables with no migration yet.

| Entity | Needed for Use Case | Plan |
|---|---|---|
| `jadwal_pengujian` | UC-20-22 | [uc-20-22-planning-pengujian/plan.md](../issues/uc-20-22-planning-pengujian/plan.md) |
| `keahlian` | UC-10 Pilih Teknisi | — |
| `jadwal` / `jadwal_pengambilan` | UC-11, UC-12 | — |
| `worksheet_pengujian` | UC-16, UC-17, UC-25 | Blocked by SYS-01 |
| `bahan` / `bahan_pengujian` | UC-24 Ambil tiket | — |
| `alat_so` | UC-20 Pilih alat pengujian | — |
| `customer_credit` / `company_transactions` | Finance — **out of scope, separate microservice** | — |
| `job_history` | Internal resource tracking | — |
