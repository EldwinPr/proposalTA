# Log — Append-Only History

<!-- Format: [DONE] Short description — YYYY-MM-DD -->
<!-- Never edit past entries. Append only. -->

[DONE] T-00 — Hapus subtitle ProposalTA.tex — 2026-04-16
[DONE] T-01 — Revisi Latar Belakang Bab I — 2026-04-16
[DONE] T-02 — Tulis ulang Rumusan Masalah Bab I — 2026-04-16
[DONE] T-03 — Tulis ulang Tujuan Bab I — 2026-04-16
[DONE] T-04 — Tulis ulang Batasan Masalah Bab I — 2026-04-16
[DONE] T-05 — Tulis ulang Metodologi Bab I — 2026-04-16
[DONE] T-07 — Hapus/slim sections lama Bab II (Metode Evaluasi, Kriteria Kelayakan, cloud TCO) — 2026-04-16
[DONE] T-06 — Tambah 4 sections baru Bab II (proses bisnis lab, LIMS, Laravel+Filament, monolith vs microservice) — 2026-04-16
[DONE] T-11 — Tulis ulang Justifikasi Hardware Bab III (RPi5 vs OPi5Pro vs N100, hapus VPS, framing pemilihan server) — 2026-04-16
[DONE] T-10 — Tulis ulang Justifikasi Teknologi Bab III (custom vs Odoo/SAP, Laravel+Filament, monolith vs microservice) — 2026-04-16
[DONE] T-09 — Tulis ulang Analisis Kebutuhan Bab III (7 KF modul lab + 4 KNF) — 2026-04-16
[DONE] T-08 — Tulis ulang Analisis Kondisi Saat Ini Bab III (2 layer: Google Sheets manual + PHP5/CI3 gagal, 3 BPMN as-is + gambar overheat) — 2026-04-16
[DONE] Sesi klarifikasi & setup konteks — 2026-04-16
- Semua keputusan dikonfirmasi: lab SSL, stack modular monolith Laravel+Filament, PostgreSQL, Orange Pi 5 Pro
- Go/Svelte microservice tidak masuk proposal
- Proposal-writer skill dibuat (.claude/skills/proposal-writer/SKILL.md)
- BPMN as-is tersedia (ops/context/old bpmn/, 10 file)
- BPMN to-be tersedia (ops/ERP_Context/diagrams/, 6 file + ERD)
- ISO 17025 PDF tersedia di sources/
- decisions.md, active.md, style files semua tersinkron

[DONE] T-20 Bab II: Restrukturisasi urutan sections, hapus Framework Laravel+Filament, persingkat CISC/RISC, gabung Deployment+Arsitektur Sistem — 2026-04-17
[DONE] T-12 — Bab IV: Gambaran Umum Arsitektur — tulis ulang total section 4.1, 5 paragraf: overview modular monolith, stack teknis (Nginx→PHP-FPM→Laravel+Filament→PostgreSQL+Redis+RBAC), deployment Orange Pi on-premise, justifikasi monolith vs distribusi, domain isolation 5 klaster — 2026-04-18
[DONE] T-13 — Bab IV: Desain per Modul — narasi 6 subseksi BPMN to-be ditambahkan (lv0, sales→order, order→acquisition, acquisition→storing, storing→testing, schedule mgmt), masing-masing 2-4 kalimat deskripsi alur, aktor, dan UC terkait — 2026-04-18
[DONE] T-14 — Bab IV: ERD — narasi per-domain ditambahkan (5 domain: Customer, Product Knowledge, Sales, Operations, Finance), deskripsi entitas dan relasi antar domain — 2026-04-18
[DONE] T-15 — Bab IV: Use Case Overview — tulis ulang total section 4.4, tabel 31 UC dikelompokkan per domain (Sales, Planning, Sampling, Lab, Penyeliaan), kolom kode/nama/aktor/status, paragraf pembuka dan penutup — 2026-04-18
[DONE] Hotfix Bab I Latar Belakang — perbaiki bridge paragraph: fokus ERP+lab, hapus klaim SBC yang tidak berdasar, 1 kalimat transisi dari on-premise→lab pengujian — 2026-04-18
