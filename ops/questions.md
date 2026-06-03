# Pertanyaan Klarifikasi — Sesi 2026-04-16

Jawab langsung di bawah setiap pertanyaan.
Target: setelah semua terjawab, `active.md` bisa diisi dan penulisan revisi dimulai.

---

## A. Latar Belakang Perusahaan

**A1. Nama lab**
Boleh disebut langsung di proposal, atau dianonimkan (misal "sebuah lab pengujian lingkungan komersil di Indonesia")?

> Jawab: Sentral Sistem Laboratory

**A2. Pain point konkret lab saat ini**
Apa yang sekarang bermasalah di proses operasional lab? Contoh: pencatatan sampel di Excel, tidak ada tracking status pengujian, CoA dibuat manual di Word, tidak ada sistem invoice terintegrasi, dll. Semakin spesifik semakin kuat motivasi RM.

> Jawab: dari penawaran, operasional, sertifikat, jurnal semuanya masih manual menggunakan di google sheets. tidak ada integrasi.

**A3. Program lama yang "baru sampai penawaran"**
Ini maksudnya sudah ada software/sistem yang cover alur sampai tahap penawaran ke klien, tapi belum ada modul selanjutnya? Atau ini alur bisnis manual yang sudah berjalan (pakai spreadsheet/Word)? Kalau ada software, dibuat pakai apa?

> Jawab: aplikasi lama tidak ada desain sistem apa apa (ERD, use case, dll) selain mockup, UX juga tidak jelas. aplikasi lama yang masih tahap dev juga menggunakan versi php 5 dengan code igniter 3 sehingga tidak layak.

---

## B. Scope Modul (Blocker Bab III & IV)

**B1. Modul yang pasti masuk scope TA**
Tandai mana yang IN, OUT, atau MAYBE:

| Modul | Status (IN / OUT / MAYBE) |
|-------|--------------------------|
| Registrasi sampel | |
| Penjadwalan pengujian | |
| Manajemen hasil uji | |
| Pelaporan CoA (Certificate of Analysis) | |
| Inventori reagen & alat | |
| Manajemen klien | |
| Finance microservice (invoice, AR/AP) | |

semuanya, end to end, finance microservice sebenarnya tambahan tapi masukan juga tidak masalah, kemudian ada juga kartu stok inventori juga

**B2. UAT dengan pengguna nyata**
Apakah pengujian dengan staf lab nyata masuk scope TA, atau cukup evaluasi teknis (fungsionalitas + hardware)?

> Jawab: belum sampai UAT karena data asli seperti parameter belum ada atau belum siap diupload sehingga tidak dapat digunakan

**B3. Database**
PostgreSQL atau MariaDB? Ini perlu dikunci sebelum ERD bisa digambar.

> Jawab: Postgres

---

## C. Struktur Bab III & IV

Konfirmasi pemahaman saya — jawab benar/salah/koreksi:

**C1. Bab III berisi:**
- BPMN *as-is* (proses lab saat ini, sebelum sistem dibangun)
- Analisis kondisi saat ini (manual, tidak terintegrasi, dll)
- Kebutuhan fungsional & non-fungsional
- Justifikasi tech stack (Laravel + Filament, Go + Svelte)
- Pemilihan hardware (Orange Pi 5 Pro, tetap relevan)

> Benar / Koreksi: ini agak bingung karena ada as is yang digunakan dan as is sedang di develop, kalau yang kemarin dibuat php 5 ci3 dan hardware ram 8gb dengan processor intel core duo quad yang cenderung overheat. satu lagi tidak ada project management yang jelas.

**C2. Bab IV berisi:**
- BPMN *to-be* (alur setelah sistem diterapkan)
- Use case diagram
- ERD (versi awal/konseptual, belum final)
- Gambaran arsitektur sistem (monolith + microservice, deployment di Orange Pi)

> Benar / Koreksi: benar

---

## D. AI-Assisted Development

**D1.**
Sudah ada rencana tanya ke dosen pembimbing soal angle ini? Kalau sudah disetujui, masuk di bagian mana menurut Anda — metodologi, catatan teknis di Bab IV, atau appendix?

> Jawab: skip dulu untuk sekarang

---

## E. Prioritas Hari Ini

**E1.**
Dari semua revisi yang ada, bagian mana yang paling ingin diselesaikan hari ini?
(Contoh: tulis ulang RM + Tujuan dulu, atau mulai dari paragraf latar belakang perusahaan, atau bersihkan subtitle dulu)

> Jawab: sebenarnya bisa semua karena artefak sudah ada, bab 2 tinggal tambah lims dan pengujian lingkungan secara singkat
