---
# Senling — Engineering Conventions (Full Spec)
# Authoritative reference. Summary → RULES.md
---

stack:
  backend:     Laravel 12 / PHP 8.4
  admin:       Filament 5 / Livewire 4
  db:          PostgreSQL
  styling:     Tailwind CSS 4
  rbac:        Spatie Permission + Filament Shield
  mcp:         Laravel Boost (search-docs, database-schema, database-query, tinker, browser-logs)
  autonumber:  Quotation::toRoman() — shared Roman numeral helper

---

db:
  primary_key:   $table->ulid('id')->primary()   # never auto-increment
  soft_deletes:  required on all domain models
  status_cols:   string/varchar — never enum (enum blocks new values without ALTER TYPE)
  field_language: Indonesian (nama, harga, tanggal, titik_sampling, frekuensi, pengambilan...)
  users_pk:      bigint — exception to ULID rule; FK to users uses foreignId()
  modify_column: include ALL previously defined attributes (type, nullable, default) + ->change()
  forbidden:
    - DB::  →  Model::query() always
    - DB::table()
    - auto-increment primary keys
    - enum columns

model:
  required_traits: [HasUlids, SoftDeletes, HasFactory]
  auto_numbering:
    hook:    booted() → static::creating()
    pattern: "{seq}/SSL/{TYPE}/{ROMAN_MONTH}/{2y}"
    example: "00001/SSL/QUO/III/26"
    helper:  Quotation::toRoman($month)
    new_pattern_so: "SSL-SO-YYMM-NNN"       # SalesOrder (FIX-03)
    new_pattern_coc: "SSL-SO-YYMM-NNN-nn"   # Pengambilan COC (FIX-03)
  auto_assign:   sales_id = auth()->id() on Quotation creating
  eager_loading: always use with() — never allow N+1
  forbidden:
    - skipping SoftDeletes
    - skipping HasUlids
    - bypassing *Revision writes for Quotation/QuotationDetail changes

filament:
  namespaces:
    form_fields:     Filament\Forms\Components\
    infolist_entries: Filament\Infolists\Components\
    layout:          Filament\Schemas\Components\   # Grid, Section, Fieldset, Tabs, Tab
    utilities:       Filament\Schemas\Components\Utilities\  # Get, Set
    actions:         Filament\Actions\
    icons:           Filament\Support\Icons\Heroicon  # enum
    notifications:   Filament\Notifications\Notification
    table_columns:   Filament\Tables\Columns\
    table_filters:   Filament\Tables\Filters\
    table_actions:   Filament\Tables\Actions\

  method_signatures:
    form:     "public static function form(Schema $schema): Schema"
    infolist: "public static function infolist(Schema $schema): Schema"
    table:    "public static function table(Table $table): Table"
    schema_top_level: "->components([...])"  # not ->schema([...])

  resource_structure: |
    app/Filament/Resources/{Name}/
    ├── {Name}Resource.php          # nav, model binding, getPages() — INSIDE folder, not root
    ├── Pages/
    │   ├── List{Name}s.php
    │   ├── Create{Name}.php
    │   ├── Edit{Name}.php
    │   └── View{Name}.php
    ├── Schemas/
    │   ├── {Name}Form.php          # form schema — NEVER inline in pages
    │   └── {Name}Infolist.php
    ├── Tables/
    │   └── {Name}sTable.php        # table def — NEVER inline in resource class
    └── RelationManagers/

  mobile_first: custom pages (TerimaSampel, lab tools) must be optimised for mobile browsers

  badge_colors:
    success: Done / Selesai / Terverifikasi
    warning: Menunggu / Abnormal / Pending
    danger:  Tolak / Batal / Error
    info:    Open / Draft

  forbidden:
    - inline form schemas in pages
    - inline table definitions in resource class
    - {Name}Resource.php at app/Filament/Resources/ root (must be inside subfolder)
    - Filament 3/4 namespaces

---

business_logic:
  so_generation:   QuotationService::generateSalesOrders() — only place; never duplicate
  qty_formula:     titik_sampling × frekuensi
  revision_trail:  any Quotation or QuotationDetail change MUST write *Revision record
  rbac_post_create: php artisan shield:generate after adding new resources
  finance_scope:   customer_credit / company_transactions = separate microservice — OUT OF SCOPE

---

code_quality:
  type_hints:    PHP 8.4 — mandatory property, parameter, return types
  validation:    Form Request classes — no inline validation in controllers/Livewire
  service_layer: cross-model logic in Services/, not duplicated inline
  constructor:   use PHP 8 constructor property promotion

---

verification:
  run:
    - php artisan test --compact
    - vendor/bin/pint --dirty --format agent

close:
  - plan.md status → done
  - tracker.md row → ✅ Done
  - requirements.csv implemented → TRUE
  - log.md → append [STATUS][ID] ✅ Done — timestamp + summary
  - active.json → next issue

---
# Last Updated: 2026-04-06
