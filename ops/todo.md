# Todo — Writing Tasks

Step-by-step tracker untuk penulisan proposal.
Dikerjakan satu per satu. Pick → active.md → selesai → log.md → kembali ke sini.

---

## Status Key
- [ ] PENDING
- [~] IN PROGRESS (lihat active.md)
- [x] DONE

---

## T-00 — ProposalTA.tex
- [x] Hapus subtitle "DENGAN ANALISIS KINERJA DAN TOTAL COST OF OWNERSHIP" dari halaman judul (baris ~237)
- [x] Hapus subtitle yang sama dari lembar pengesahan (baris ~284)

---

## T-01 — Bab I: Latar Belakang
- [x] Paragraf 1–3: pertahankan (sejarah ERP, cloud vs on-premise, ARM/SBC) — cek relevansi, trim jika perlu
- [x] Tambah paragraf SSL: profil lab, proses manual saat ini, pain points, motivasi ERP custom
- [x] Revisi paragraf gap: dari "belum ada data empiris SBC vs VPS" → "belum ada ERP custom untuk domain lab pengujian lingkungan di SBC"

## T-02 — Bab I: Rumusan Masalah
- [x] Tulis ulang dengan RM final:
      RM 1: rancangan sistem ERP custom untuk proses bisnis lab
      RM 2: metodologi pengembangan ERP custom untuk domain lab

## T-03 — Bab I: Tujuan
- [x] Selaraskan dengan RM baru:
      Tujuan 1: menghasilkan rancangan sistem ERP custom end-to-end untuk SSL
      Tujuan 2: mendokumentasikan metodologi pengembangan ERP custom domain lab

## T-04 — Bab I: Batasan Masalah
- [x] Tulis ulang:
      - deployment on-premise only
      - modul yang masuk scope (7 modul)
      - Orange Pi 5 Pro sebagai hardware
      - UAT tidak masuk scope (data parameter belum siap)
      - proposal scope sampai desain

## T-05 — Bab I: Metodologi
- [x] Ganti metodologi benchmarking/TCO → metodologi pengembangan sistem
      Fase: analisis kebutuhan → desain → implementasi → pengujian → evaluasi hardware

---

## T-06 — Bab II: Tambah section baru
- [x] Section: Proses bisnis lab pengujian lingkungan (referensi ISO 17025 sebagai standar target)
- [x] Section: LIMS — definisi singkat, hubungannya dengan ERP, mengapa Senling bukan LIMS murni
- [x] Section: Laravel + Filament sebagai platform ERP custom (Gaya C — bandingkan dengan alternatif)
- [x] Section: Justifikasi arsitektur modular monolith vs microservice (Gaya C)

## T-07 — Bab II: Hapus/kurangi section lama
- [x] Hapus atau slim section Metode Evaluasi (TCO, load testing, break-even)
- [x] Hapus atau slim section Kriteria Kelayakan
- [x] Slim section cloud comparison — pertahankan hanya yang relevan untuk on-premise justification

---

## T-08 — Bab III: Analisis Kondisi Saat Ini
- [x] Layer 1: proses operasional manual (Google Sheets, tidak terintegrasi) — narasi + BPMN as-is (ops/context/old bpmn/)
- [x] Layer 2: aplikasi lama PHP5/CI3 — upaya digitalisasi sebelumnya yang tidak layak

## T-09 — Bab III: Kebutuhan Fungsional & Non-Fungsional
- [x] Tulis ulang KF: modul-modul ERP untuk lab (7 modul, bukan kebutuhan penelitian)
- [x] Tulis ulang KNF: performa, keamanan, deployable di Orange Pi, maintainability

## T-10 — Bab III: Justifikasi Tech Stack
- [x] Ganti section "Pemilihan Platform Software" (ERPNext vs Odoo) →
      "Justifikasi Tech Stack": Laravel+Filament vs alternatif (Gaya C)
- [x] Tambah sub-section: justifikasi arsitektur modular monolith vs microservice

## T-11 — Bab III: Justifikasi Hardware
- [x] Pertahankan struktur tabel perbandingan, update konten:
      - Hapus VPS sebagai pembanding
      - Perbandingan: Orange Pi 5 Pro vs Raspberry Pi 5 vs Intel N100
      - Framing: justifikasi pemilihan dev+UAT server, bukan benchmarking

---

## T-20 — Bab II: Restrukturisasi urutan + konten ✓ DONE 2026-04-17

---

## T-12 — Bab IV: Gambaran Umum Arsitektur
- [x] Tulis ulang total: gambaran sistem Senling (modular monolith)
      Stack: Nginx → PHP-FPM → Laravel+Filament → PostgreSQL + Redis
      Deployment di Orange Pi 5 Pro

## T-13 — Bab IV: Desain per Modul
- [x] BPMN to-be per alur (gunakan ops/ERP_Context/diagrams/)
- [x] Deskripsi tanggung jawab tiap modul (dari requirements.csv)

## T-14 — Bab IV: ERD
- [x] Include ERD (ops/ERP_Context/diagrams/ERD.png)
- [x] Narasi domain separation: Customer, Product Knowledge, Sales, Operations, Finance

## T-15 — Bab IV: Use Case Overview
- [x] Ringkasan UC-01 s/d UC-31 (dari requirements.csv)
- [x] Kelompokkan per domain/aktor

---

## T-16 — Bab V: Rencana Pengembangan
- [x] Ganti "Rencana Evaluasi" → "Rencana Pengembangan"
- [x] Fase: 8 fase sekuensial (doc setup, migrasi, 7 modul) × 1–3 minggu each
- [x] Dokumentasi lengkap 39 UC tercakup dalam fase-fase implementasi

## T-17 — Bab V: Metodologi Pengembangan (RM 2)
- [x] Tulis section metodologi: PM approach (GitHub → .md → agents), development process, tools
- [x] SBC sebagai dev+UAT server — bagian dari setup metodologi
- [x] Placeholder untuk AI-assisted development (agents + context management)

## T-18 — Bab V: Gantt Chart
- [x] Gantt chart reference updated (timeline pengembangan, 17 minggu)
- [x] Sesuaikan dengan 8 fase di T-16

## T-19 — Bab V: Analisis Risiko
- [x] Revisi: ganti risiko penelitian → risiko implementasi
      (5 risiko implementasi: go-live delay, scope creep, data loss, parameter availability, hardware failure)

---

## T-21 — Narasi perusahaan: broad → specific funnel
Prinsip: Bab I & II bersifat broad (ERP, SBC, lab pengujian secara umum, tech stack).
Detail spesifik perusahaan baru masuk mulai Bab III → IV → V.

- [x] Bab I: hapus semua penyebutan perusahaan spesifik (SSLab / Sentral Sistem Laboratory) — broad-ified (2026-06-09)
- [x] Bab II: hapus semua penyebutan perusahaan spesifik — semua SSLab → generik (2026-06-09)
      (Bab II baris 66 di-broad-kan; sekaligus menghapus overclaim akreditasi)
- [x] Bab III.1: \section{Profil Perusahaan} ditulis — paraphrase profil Sentral Sistem Group (PT Sentral Tehnologi Managemen 1999 → Consulting → Calibration 2014 → SSLab 2025), \cite{ssl_website} (2026-06-09)

### Akurasi akreditasi ISO/IEC 17025
- [x] Bab III baris 18: overclaim diperbaiki → "terakreditasi KAN (ISO/IEC 17025) untuk sebagian parameter pengujiannya" (2026-06-09)
- [x] decisions.md sudah dikoreksi (2026-06-09) — jangan pakai frasa "terakreditasi penuh".

Catatan: Bab I, II, III sudah diberi treatment. Hanya III.1 (company background prose) yang tersisa — milik user.
