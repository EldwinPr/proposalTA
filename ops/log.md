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
[DONE] T-19 — Bab V: Analisis Risiko — ganti 3 risiko (hardware/internet lama) dengan 5 risiko implementasi (go-live delay, scope creep, data loss, parameter availability, hardware failure); update caption dan intro text dari "penelitian" → "implementasi sistem" — 2026-06-03
[DONE] T-17 — Bab V: Metodologi Pengembangan — tulis section baru: PM approach evolution (GitHub → .md → agents), development process (7 phases), tools (Laravel+Filament+PostgreSQL), SBC role, AI-assisted development placeholder — 2026-06-03
[DONE] T-16 — Bab V: Rencana Pengembangan — tulis section baru: 8 phases (17 weeks total), phase breakdown per modul, UC coverage per fase, notes on schedule flexibility — 2026-06-03
[DONE] T-18 — Bab V: Gantt Chart — update Gantt reference: 17-week timeline (8 phases), updated caption to "Jadwal pengembangan sistem Senling" — 2026-06-03
[DONE] T-16/T-17/T-18 restructure — align Bab V Rencana Pengembangan dengan 5 BPMN to-be Bab IV (Sales to Order, Order to Acquisition, Acquisition to Storing, Storing to Testing, Schedule Management) + Penyeliaan; Gantt chart pindah ke atas, detail fase di bawah; total 14 minggu (2 doc + 6 impl); fix 39 UC → 31 UC, references ke Bab IV Subbab — 2026-06-03
[DONE] T-12 — Bab IV: Gambaran Umum Arsitektur — tulis ulang total section 4.1, 5 paragraf: overview modular monolith, stack teknis (Nginx→PHP-FPM→Laravel+Filament→PostgreSQL+Redis+RBAC), deployment Orange Pi on-premise, justifikasi monolith vs distribusi, domain isolation 5 klaster — 2026-04-18
[DONE] T-13 — Bab IV: Desain per Modul — narasi 6 subseksi BPMN to-be ditambahkan (lv0, sales→order, order→acquisition, acquisition→storing, storing→testing, schedule mgmt), masing-masing 2-4 kalimat deskripsi alur, aktor, dan UC terkait — 2026-04-18
[DONE] T-14 — Bab IV: ERD — narasi per-domain ditambahkan (5 domain: Customer, Product Knowledge, Sales, Operations, Finance), deskripsi entitas dan relasi antar domain — 2026-04-18
[DONE] T-15 — Bab IV: Use Case Overview — tulis ulang total section 4.4, tabel 31 UC dikelompokkan per domain (Sales, Planning, Sampling, Lab, Penyeliaan), kolom kode/nama/aktor/status, paragraf pembuka dan penutup — 2026-04-18
[DONE] Hotfix Bab I Latar Belakang — perbaiki bridge paragraph: fokus ERP+lab, hapus klaim SBC yang tidak berdasar, 1 kalimat transisi dari on-premise→lab pengujian — 2026-04-18
[DONE] T-21 — Funnel broad→spesifik: hapus semua penyebutan SSLab/Sentral Sistem Laboratory dari Bab I (latar belakang di-broad-kan, tujuan/batasan/metodologi → "lab pengujian lingkungan komersil", hapus \cite{ssl_website}) dan Bab II (6 mention SSLab → generik, baris 66 sekaligus hapus overclaim akreditasi); Bab III & IV-V tetap pakai SSLab. Bab III.1 background = milik user — 2026-06-09
[DONE] Fix akurasi akreditasi — Bab III baris 18 "SSLab telah terakreditasi KAN (ISO/IEC 17025)" → "...untuk sebagian parameter pengujiannya" (akreditasi per-parameter, SSLab unit baru 2025). decisions.md:68 + company-profile.md dikoreksi — 2026-06-09
[DONE] Bab III.1 — tulis \section{Profil Perusahaan}: paraphrase profil Sentral Sistem Group (PT Sentral Tehnologi Managemen 1999, Consulting → Calibration 2014 terakreditasi KAN → SSLab 2025 pengujian mekanik+lingkungan), voice marketing "kami" → deskriptif orang ketiga, \cite{ssl_website}; trim re-introduksi redundan di awal "Analisis Kondisi Saat Ini" — 2026-06-09
[DONE] Consistency check + humanizer — verifikasi funnel (Bab I/II bersih SSLab, III+ pakai SSLab), microservice hanya sebagai alternatif yang ditolak (OK), akreditasi konsisten (Calibration=KAN, SSLab sebagian parameter), ref Bab V→Bab IV Subbab 2.x valid. Humanize Profil Perusahaan (Gaya A: variasi ritme, buang brochure-speak, variasi opener temporal, closer jadi bridge ke Analisis Kondisi). Fix repetisi "manual"→"informal/inkonsistensi" di Bab I. FLAG: table/tabelkriteriakeberhasilan.tex orphan (TCO/VPS/benchmark, tidak di-\input) — 2026-06-09
[DONE] Hapus table/tabelkriteriakeberhasilan.tex (orphan, isi TCO/VPS/benchmark) via git rm — 2026-06-09
[DONE] Fix pemenggalan kata (hyphenation) — root cause: babel memecah kata sebelum sufiks "-an" (keuang-an, pembeli-an, pencatat-an, ditunjukk-an, lingkung-an) + kata Inggris (se-rver, ERPNe-xt, da-ta). Solusi global \addto\extrasindonesian{\righthyphenmin=3} di ProposalTA.tex (larang break menyisakan <=2 huruf) + \hyphenation{ser-ver} + \emergencystretch=2em. Verifikasi via baca ProposalTA.pdf hal 2-20 — 2026-06-09
[DONE] Consistency audit 3 subagent (Bab I+II, Bab III, cross-chapter) — 0 blocker; semua rule lolos (funnel, modular monolith, akreditasi sebagian parameter, 31 UC, 7 modul, tech stack). Minor: italik tidak konsisten Bab II, \cite nempel, Senling tanpa gloss, 4 entri .bib uncited — 2026-06-09
[DONE] Apply polish 1-3 + tighten klaim sitasi vague — Bab II: italik konsisten (load balancing, traffic, cluster, node, reliability, usability, business logic, user, dll), \cite{} dikasih spasi + triple cite digabung jadi \cite{a,b,c}, gloss Senling. Tighten "menunjukkan potensi yang lebih besar" → konkret (Bab I + Bab II beberapa kalimat). Hapus 4 entri .bib uncited (buijsse2024reference, neomind2024tco TCO-themed, qu2020experimental, newman2015building) — 2026-06-09
[DONE] Fix hyphenation (mekanisme yang benar) + orphan page — \addto\extrasindonesian gagal (babel timpa), ganti \righthyphenmin=3 SETELAH \begin{document} + \hyphenation eksplisit (ke-uangan, pem-be-lian, ling-kungan, pen-ca-tatan, di-tun-jukkan, data, ser-ver). Padatkan paragraf gap Latar Belakang Bab I (~2 baris) untuk hapus orphan hal 5. Verifikasi recompile: ke-uangan/pembe-lian benar, orphan hilang, dokumen -1 halaman — 2026-06-09
