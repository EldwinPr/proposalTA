# Catatan Revisi Proposal TA

**Judul:** Penerapan Enterprise Resource Planning pada Single Board Computer  
**Perubahan utama:** Topik bergeser dari studi kelayakan/evaluasi → implementasi sistem ERP custom untuk lab pengujian lingkungan komersil menggunakan Orange Pi sebagai server on-premise.

---

## ProposalTA.tex

- [ ] Hapus subtitle "Dengan Analisis Kinerja dan Total Cost of Ownership" dari judul di halaman judul
- [ ] Hapus subtitle yang sama dari lembar pengesahan

---

## Bab I — Pendahuluan

**Latar Belakang**
- [ ] Pertahankan paragraf 1–3 (sejarah ERP, cloud vs on-premise, ARM/SBC)
- [ ] Tambah paragraf baru: lab pengujian lingkungan komersil sebagai domain yang membutuhkan ERP on-premise (data sensitif, tidak bergantung internet, skala kecil-menengah cocok untuk SBC)
- [ ] Revisi paragraf gap: dari "belum ada data empiris SBC vs VPS" → "belum ada implementasi ERP custom untuk domain lab pengujian lingkungan yang berjalan di SBC"

**Rumusan Masalah** (tulis ulang)
- [ ] RM 1: Bagaimana merancang dan mengimplementasikan sistem ERP custom yang sesuai dengan proses bisnis end-to-end lab pengujian lingkungan komersil?
- [ ] RM 2: Apakah Single Board Computer (Orange Pi) layak digunakan sebagai platform server on-premise yang hemat biaya untuk sistem ERP skala lab pengujian lingkungan?

**Tujuan** (tulis ulang, selaraskan dengan RM baru)
- [ ] Tujuan 1: Merancang arsitektur dan mengimplementasikan ERP custom untuk lab pengujian lingkungan
- [ ] Tujuan 2: Mengevaluasi kelayakan Orange Pi sebagai server on-premise (vs x86 on-premise, bukan vs VPS)

**Batasan Masalah** (tulis ulang)
- [ ] Tentukan modul yang masuk scope (kandidat: registrasi sampel, penjadwalan pengujian, manajemen hasil uji, pelaporan CoA, inventori reagen, manajemen klien, finance)
- [ ] Tegaskan: deployment on-premise only, tidak ada perbandingan vs VPS
- [ ] Sebutkan Orange Pi 5 Pro sebagai hardware yang digunakan
- [ ] Tentukan apakah UAT dengan pengguna nyata masuk scope

**Metodologi** (tulis ulang)
- [ ] Ganti metodologi benchmarking + TCO → metodologi pengembangan sistem (SDLC/prototyping)
- [ ] Fase: analisis kebutuhan → desain → implementasi → pengujian → evaluasi hardware

---

## Bab II — Studi Literatur

**Tambah section baru:**
- [ ] Proses bisnis lab pengujian lingkungan (referensi ISO 17025 sebagai standar)
- [ ] LIMS (Laboratory Information Management System) dan hubungannya dengan ERP
- [ ] Laravel + Filament sebagai platform pengembangan ERP
- [ ] Justifikasi arsitektur modular monolith (vs microservice) untuk skala lab + deployment SBC

**Hapus atau kurangi:**
- [ ] Literatur TCO comparison cloud vs on-premise
- [ ] Literatur benchmark SBC vs VPS

---

## Bab III — Analisis Masalah

- [ ] Tulis ulang "Analisis Kondisi Saat Ini": proses lab saat ini (manual/spreadsheet yang tidak terintegrasi)
- [ ] Tulis ulang "Kebutuhan Fungsional": modul-modul ERP untuk lab (bukan kebutuhan penelitian)
- [ ] Tulis ulang "Kebutuhan Non-Fungsional": performa, keamanan, deployable di Orange Pi
- [ ] Ganti seluruh section "Pemilihan Platform Software" (ERPNext vs Odoo) → "Justifikasi Tech Stack" (Laravel + Filament, arsitektur modular monolith)
- [ ] Pertahankan dan sesuaikan "Pemilihan Platform Hardware" (justifikasi Orange Pi 5 Pro masih relevan)

---

## Bab IV — Desain Konsep Solusi

Tulis ulang total:
- [ ] Gambaran umum arsitektur sistem: Laravel + Filament sebagai modular monolith, dijalankan di Orange Pi dengan Nginx sebagai reverse proxy (Nginx → PHP-FPM → Laravel+Filament → PostgreSQL + Redis)
- [ ] Desain per modul (alur data, tanggung jawab tiap modul)
- [ ] ERD atau diagram relasi antar entitas utama
- [ ] Deployment architecture di Orange Pi (stack lengkap: Nginx, PHP-FPM, PostgreSQL/MariaDB, Redis, Go service)

---

## Bab V — Rencana Selanjutnya

- [ ] Ganti "Rencana Evaluasi" → "Rencana Pengembangan"
- [ ] Tulis fase-fase pembangunan: setup dev environment → implementasi modul inti → integrasi → testing → evaluasi hardware
- [ ] Revisi kriteria keberhasilan: dari throughput/response time benchmark → fungsionalitas modul + UAT + evaluasi Orange Pi untuk prod
- [ ] Buat Gantt chart baru sesuai timeline pengembangan
- [ ] Revisi analisis risiko: sesuaikan dengan risiko implementasi (bukan risiko penelitian)
