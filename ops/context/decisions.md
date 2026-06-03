title: "Penerapan Enterprise Resource Planning pada Single Board Computer"
subtitle_removed: true  # "Dengan Analisis Kinerja dan Total Cost of Ownership" dihapus per arahan pembimbing
lab_in_title: false     # lab hanya jadi konteks/studi kasus di dalam teks

rumusan_masalah:
  - "Bagaimana merancang sistem ERP custom yang sesuai dengan proses bisnis end-to-end lab pengujian lingkungan komersil?"
  - "Bagaimana metodologi pengembangan yang efektif untuk membangun sistem ERP custom pada domain lab pengujian lingkungan?"
  rm1_focus: "hasil — rancangan sistem ERP (arsitektur, modul, desain domain)"
  rm2_focus: "proses — metodologi pengembangan; mencakup PM, dev methodology, SBC sebagai dev+UAT server, AI-assisted development (jika disetujui pembimbing)"

topic_shift: "studi kelayakan/evaluasi -> implementasi sistem"
no_vps_comparison: true   # kebutuhan adalah on-premise; tidak ada benchmarking vs VPS
on_premise_reason: "keinginan SSLab untuk self-hosting penuh — ingin mengelola sendiri tanpa bergantung pada infrastruktur pihak ketiga"

tech_stack:
  approach: "modular monolith — dibangun dari nol (custom), bukan kustomisasi Odoo/ERPNext"
  system_name: Senling
  framework: "Laravel 12 + Filament 5 (PHP 8.4)"
  database: PostgreSQL
  cache: Redis
  web_server: Nginx
  rbac: "Spatie Permission + Filament Shield"
  finance_in_proposal: "bagian dari monolith — modul finance masuk dalam Laravel, bukan microservice terpisah"

  justification_laravel_filament:
    alternatives_discussed: ["Odoo", "SAP"]
    why_not_off_the_shelf: >
      Odoo dan SAP tetap dibahas sebagai alternatif off-the-shelf yang umum dipertimbangkan.
      Keduanya tidak dipilih karena: domain lab pengujian lingkungan terlalu spesifik untuk
      dipetakan ke modul generik, biaya lisensi/implementasi tidak sebanding dengan skala SSLab,
      dan kustomisasi mendalam justru lebih mahal dari membangun sendiri.
    why_laravel: >
      Tim pengembang sudah terbiasa dengan PHP — familiaritas ini mengurangi waktu onboarding
      dan risiko teknis. Laravel dipilih atas framework PHP lain karena ekosistem yang mature,
      ORM yang ekspresif, dan komunitas yang aktif.
    why_filament: >
      Keterbatasan waktu pengembangan — Filament mempercepat pembuatan panel admin secara
      signifikan (tabel, form, CRUD, RBAC) tanpa menulis ulang dari nol, sehingga waktu
      dapat difokuskan pada logika domain bisnis lab yang spesifik.
    note_for_bab_III: "Justifikasi ini masuk di section Justifikasi Tech Stack Bab III (Gaya C)"
  note_microservice: >
    Finance microservice Go+Svelte ada di realita tapi TIDAK disebutkan dalam proposal.
    Proposal mempresentasikan sistem sebagai full modular monolith.

hardware:
  chosen: "Orange Pi 5 Pro"
  soc: RK3588S
  cores: octa-core
  max_ram: 16GB
  tdp: "10-15W"
  deployment: on-premise only
  justification_comparison:
    - device: "Orange Pi 5 Pro"
      price_approx: "~Rp 2 juta"
      verdict: DIPILIH
    - device: "Raspberry Pi 5"
      verdict: "pembanding — spesifikasi comparable"
    - device: "Intel N100 mini PC"
      verdict: "pembanding — terlalu mahal untuk opsi ini"
  price_actual: "~Rp 2 juta termasuk casing dan adapter"
  note: "Perbandingan ini untuk justifikasi pemilihan hardware di Bab III, bukan benchmarking kinerja"

domain:
  lab_name: "Sentral Sistem Laboratory"
  lab_abbr: SSLab
  lab_type: "lab pengujian lingkungan komersil"
  company_name_in_proposal: "boleh disebut langsung"
  iso_17025: "sudah terakreditasi ISO/IEC 17025; referensikan sebagai standar yang sudah dipegang SSLab, bukan sekadar target"

pain_points:
  - "Seluruh proses (penawaran, operasional, sertifikat, jurnal) masih manual menggunakan Google Sheets — tidak ada integrasi"
  - "Aplikasi lama (PHP 5 + CodeIgniter 3) pernah dikembangkan tapi tidak layak dilanjutkan: tidak ada desain sistem (ERD, use case), hanya mockup, UX tidak jelas, hanya mencakup sampai penawaran"
  - "Hardware lama: Intel Core Duo Quad, RAM 8GB, cenderung overheat — tidak memadai untuk server ERP"
  - "Tidak ada project management yang jelas pada pengembangan sebelumnya"

as_is_framing: |
  Kondisi saat ini = Google Sheets sepenuhnya (manual, tidak terintegrasi).
  Aplikasi lama PHP5/CI3 = upaya digitalisasi sebelumnya yang tidak berhasil/tidak layak,
  bukan kondisi yang sedang berjalan. Framing di Bab III: dua layer masalah —
  (1) proses operasional manual, (2) upaya digitalisasi sebelumnya gagal.

modules:
  in_scope:
    - registrasi sampel
    - penjadwalan pengujian
    - manajemen hasil uji
    - pelaporan sertifikat hasil uji
    - inventori reagen & alat (termasuk kartu stok)
    - manajemen klien
    - modul finance (invoice, AR/AP) — bagian dari monolith
  out_of_scope:
    - HR/payroll
    - multi-branch
    - UAT dengan pengguna nyata (data parameter asli belum siap)

use_cases:
  total: 31  # UC-01 s/d UC-31
  implemented: "UC-01 s/d UC-15 (Implementation: TRUE)"
  pending: "UC-16 s/d UC-31 (target 10/4/2026)"
  source: "ops/ERP_Context/requirements.csv"

artifacts_available:
  bpmn:
    - "ops/ERP_Context/diagrams/BPMN lv 0.png"       # overview
    - "ops/ERP_Context/diagrams/Sales to Order.png"
    - "ops/ERP_Context/diagrams/Order to acquisition.png"
    - "ops/ERP_Context/diagrams/Acquisition to Storing.png"
    - "ops/ERP_Context/diagrams/Storing to Testing.png"
    - "ops/ERP_Context/diagrams/Schedule Management.png"
  erd:
    - "ops/ERP_Context/diagrams/ERD.png"
    - "ops/ERP_Context/diagrams/erd.md"  # mermaid source
  use_cases: "ops/ERP_Context/requirements.csv"
  statuses: "ops/ERP_Context/statuses.md"
  conventions: "ops/ERP_Context/conventions.md"

architecture:
  old_system:
    type: "monolith (PHP 5 + CodeIgniter 3)"
    problems: "tidak ada desain (ERD, use case), hanya mockup, hanya cover sampai penawaran, hardware overheat"
  new_main_system:
    type: "modular monolith (Laravel 12 + Filament 5)"
    note: >
      Satu codebase, satu deployment, satu database PostgreSQL — tapi domain dipisahkan secara eksplisit.
      Domain separation terlihat di ERD: Customer, Product Knowledge, Sales, Operations masing-masing
      cluster entitas yang terisolasi. Berbeda dari PHP5/CI3 yang tidak punya pemisahan domain.
    domains:
      - Customer: customers, customer_contacts, customer_addresses
      - Product Knowledge: produk_uji, regulasi, paket, parameter, reference_methods, alats, wadahs
      - Sales: quotations, quotation_details, quotation_detail_parameters
      - Operations: sales_orders, sales_order_details, pengambilan, samples, sample_parameter
  finance_module:
    in_proposal: "modul finance adalah bagian dari modular monolith Laravel"
    not_mentioned: "Go + Svelte microservice tidak disebutkan di proposal"

  architecture_justification:
    chosen: "modular monolith"
    rejected: "microservice"
    reason: >
      Skala operasional SSLab masih kecil — jumlah pengguna terbatas, volume transaksi tidak tinggi,
      tim pengembang kecil. Overhead koordinasi microservice (network calls, service discovery,
      distributed tracing) tidak sebanding dengan manfaatnya pada skala ini.
      Modular monolith memberikan keuntungan pemisahan domain (maintainability) sekaligus
      kesederhanaan deployment dan operasional yang sesuai untuk on-premise di Orange Pi.
    note_for_bab_III: "Justifikasi ini masuk di section pemilihan arsitektur Bab III (Gaya C)"

bab_III_as_is:
  note: "Ada dua kondisi as-is yang perlu dibedakan"
  kondisi_1: "Proses manual via Google Sheets — tidak terintegrasi"
  kondisi_2: >
    Aplikasi lama PHP5/CI3 — tidak layak: tidak ada desain (ERD, use case),
    hanya mockup Excel, BPMN dibuat di Bizagi (tidak terintegrasi ke sistem),
    hanya mencakup sampai penawaran. Hardware lama (Intel Core Duo Quad, RAM 8GB)
    overheat terdeteksi via htop — tidak ada screenshot tapi ada file:
    ops/context/hasil test lama.png
  bpmn_as_is_available: "ops/context/old bpmn/ — 10 file PNG"
  bpmn_as_is_include: "level 0 + proses pembelian/penawaran + pilih yang paling representatif (tidak harus semua 10)"

bab_III_requirements:
  concurrent_users_target: 20  # edge case / target maksimal dalam 1 menit
  security: "tidak ada requirement khusus — on-premise karena ingin self-hosting"
  tech_stack_decision: "langsung custom dari awal — tidak pernah mempertimbangkan Odoo/ERPNext"

hardware:
  chosen: "Orange Pi 5 Pro"
  price_actual: "~Rp 2 juta termasuk casing dan adapter"

bab_IV_scope:
  - "BPMN to-be — ops/ERP_Context/diagrams/ (6 PNG: BPMN lv 0, Sales to Order, dll)"
  - "Use case — ops/ERP_Context/requirements.csv (31 UC)"
  - "ERD modular monolith — ops/ERP_Context/diagrams/ERD.png + erd.md"
  - "Arsitektur: Nginx → PHP-FPM → Laravel+Filament → PostgreSQL + Redis (semua dalam satu deployment)"
  note: "Semua versi awal/proposal — bukan implementasi final. Tidak ada referensi microservice."

sources_available:
  iso_17025: "sources/ISO_IEC_17025_2005_IN.pdf — versi Indonesia, perlu entry BibTeX sebelum digunakan"
  old_bpmn: "ops/context/old bpmn/ — 10 PNG as-is BPMN (proses sebelum sistem)"
  new_bpmn: "ops/ERP_Context/diagrams/ — 6 PNG + ERD.png to-be (sistem Senling)"
  ssl_website: "https://www.sentralsistemlaboratory.com/ — website resmi SSLab, gunakan untuk deskripsi lab di Latar Belakang"

citations_todo:
  - "ISO 17025 — tambahkan BibTeX entry saat mulai nulis Bab II/III"
  - "SSLab website — tambahkan BibTeX @online entry saat menulis paragraf latar belakang SSLab"
  - "LIMS — sebut singkat sebagai konsep, tidak perlu referensi formal"
  - "Tidak perlu sitasi dokumentasi framework"

bab_V_gantt: "perlu dibuat ulang — timeline pengembangan (bukan timeline penelitian)"
ai_development_angle: "skip — tanya dosen dulu"
