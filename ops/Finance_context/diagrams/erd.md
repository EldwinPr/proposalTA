# Entity Relationship Diagram

_Mermaid format. Updated when models change._

```mermaid
erDiagram

    User {
        string id PK "ULID"
        string name
        string email "UNIQUE"
        string password "hidden"
        int clearance "0=Staff 10=Manager 20=Dev"
        datetime created_at
        datetime updated_at
        datetime deleted_at "soft delete"
    }

    COA {
        string id PK "account code e.g. 1-1100"
        string name
        string normal "D or C"
        string category "Neraca / Profit and Loss"
        string sub_category "Harta Kewajiban Modal Pendapatan Biaya"
        datetime created_at
        datetime updated_at
        datetime deleted_at "soft delete"
    }

    CompanyBalance {
        string id PK "ULID"
        string coa_id FK
        string account_name
        string account_number "e.g. 882-001-992"
        float balance
        datetime updated_at
        datetime deleted_at "soft delete"
    }

    CompanyTransaction {
        string id PK "ULID"
        string number "UNIQUE TRANS-YYYYMMDDNNNN"
        string balance_id FK
        string journal_id FK "nullable"
        string created_by_id FK
        datetime date
        float amount
        string type "IN or OUT"
        string description
        string voucher_number
        string reference
        datetime created_at
        datetime updated_at
    }

    CustomerCredit {
        string id PK "ULID"
        string customer_name "UNIQUE"
        string npwp
        string nik
        string tax_name
        string tax_address
        datetime created_at
        datetime updated_at
        datetime deleted_at "soft delete"
    }

    Invoice {
        string id PK "ULID"
        string number "UNIQUE"
        string customer_id FK
        string created_by_id FK
        string approved_by_id FK "nullable"
        datetime invoice_date
        datetime due_date
        float dpp "Dasar Pengenaan Pajak"
        float ppn "VAT 11%"
        float pph23 "Withholding tax"
        float total_amount
        string po_number
        string project_number
        string tax_invoice_number "Nomor Faktur Pajak"
        string status "DRAFT PENDING APPROVED VOID"
        datetime created_at
        datetime updated_at
        datetime deleted_at "soft delete"
    }

    InvoiceDetail {
        string id PK "ULID"
        string invoice_id FK
        string description
        float qty
        float price
        float subtotal
    }

    Journal {
        string id PK "ULID"
        string number "UNIQUE e.g. JV-2024-0001"
        string created_by_id FK
        string approved_by_id FK "nullable"
        datetime date
        string description
        string source_type "INVOICE PAYMENT VOUCHER MANUAL ADJUSTMENT SUBCON"
        string source_id "ID of source document"
        string status "DRAFT POSTED VOID"
        datetime created_at
        datetime updated_at
        datetime deleted_at "soft delete"
    }

    JournalEntry {
        string id PK "ULID"
        string journal_id FK
        string coa_id FK
        float debit
        float credit
        string entity_name "Client or Supplier"
        string nomor_faktur "Tax invoice number"
        string voucher_number
        string reff_type "INVOICE VOUCHER TRANSACTION CPR"
        string reff_num "human-readable reference"
        string reff_id "nullable FK to referenced record"
        string nde "Nomor Dokumen External"
        string description "Uraian"
        datetime created_at
    }

    AdjustmentTicket {
        string id PK "ULID"
        string created_by_id FK
        string approved_by_id FK "nullable"
        string target_id "nullable FK to target record"
        string type "CREATE UPDATE VOID MANUAL_JOURNAL"
        string target_table "invoices manual_journals company_transactions"
        string payload "JSON of proposed change"
        string description "reason"
        string status "PENDING APPROVED REJECTED POSTED"
        datetime created_at
        datetime updated_at
        datetime deleted_at "soft delete"
    }

    Voucher {
        int id PK "external system BigInt — no ULID"
        string journal_id FK
        string voucher_num "UNIQUE from external app"
        string source_type "PENGAJUAN SUBCON etc."
        string description
        float amount
        string status "OPEN CLOSED"
        datetime created_at
        datetime updated_at
        datetime deleted_at "soft delete"
    }

    %% Relationships
    CustomerCredit ||--o{ Invoice : "has many"
    Invoice ||--o{ InvoiceDetail : "has many"
    Invoice }o--|| User : "created_by"
    Invoice }o--o| User : "approved_by"

    Journal ||--o{ JournalEntry : "has many"
    Journal }o--|| User : "created_by"
    Journal }o--o| User : "approved_by"

    JournalEntry }o--|| COA : "coa_id"

    CompanyBalance }o--|| COA : "coa_id"
    CompanyTransaction }o--|| CompanyBalance : "balance_id"
    CompanyTransaction }o--o| Journal : "journal_id"
    CompanyTransaction }o--|| User : "created_by"

    Voucher }o--|| Journal : "journal_id"

    AdjustmentTicket }o--|| User : "created_by"
    AdjustmentTicket }o--o| User : "approved_by"
```

---

## Key Relationships Summary

```
CustomerCredit  ──< Invoice ──< InvoiceDetail
Invoice         ────────────────────► Journal  (approval,  source_type=INVOICE)
Invoice+Payment ────────────────────► Journal  (payment,   source_type=PAYMENT)
Voucher         ────────────────────► Journal  (source_type=VOUCHER|SUBCON)
AdjustmentTicket ───────────────────► Journal  (approval,  source_type=ADJUSTMENT)
Journal         ──────────────────< JournalEntry
JournalEntry (bank COA) ────────────► CompanyTransaction  (auto-sync via syncBankFromEntries)
CompanyTransaction ──────────────────► CompanyBalance      (balance updated)
CompanyBalance  ────────────────────► COA
```
