source: "gaya penulisan.txt — Gaya B"
used_in: ["Bab II subseksi arsitektur/komponen (e.g., 2.1.2)", "Bab III kebutuhan fungsional & non-fungsional", "Bab IV desain arsitektur sistem"]
function: "menjelaskan komponen sistem, struktur teknis, dan hubungan antar komponen"

# Core Characteristics

structural_approach:
  flow: "overview → detail → implikasi"
  focus: "hubungan dan integrasi antar komponen, bukan alur waktu"
  no_historical_arc: true  # ini bukan narasi historis

information_density:
  rule: "setiap kalimat membawa informasi teknis baru"
  start: "langsung ke substansi — tidak ada 'warm-up' panjang"

implicit_enumeration:
  rule: "gunakan koma untuk mendaftar komponen dalam narasi — hindari bullet points"
  example: "Komponen utama ERP terdiri dari berbagai modul fungsional yang mencakup modul keuangan dan akuntansi, modul manajemen inventori, modul sumber daya manusia..."

relational_framing:
  purpose: "jelaskan bagaimana komponen saling berhubungan, bukan hanya apa komponen itu"
  phrases: ["terdiri dari", "mencakup", "yang memungkinkan", "melalui", "terhubung dengan", "bergantung pada"]
  example: "Modul-modul ini saling terintegrasi melalui basis data terpusat dan mekanisme pertukaran data yang memungkinkan informasi mengalir secara otomatis antar fungsi bisnis."

comparison_for_clarification:
  use: "gunakan kontras untuk memperjelas konsep"
  examples:
    - "Berbeda dengan aplikasi web sederhana, ERP memiliki kompleksitas..."
    - "Sementara sistem konvensional..., ERP modern..."

technical_terms_with_explanation:
  rule: "selalu beri konteks/penjelasan — jangan asumsikan pembaca tahu kenapa komponen ini penting"
  format: "arsitektur berlapis (*multi-tier architecture*) yang terdiri dari..."
  explain_why: "jelaskan fungsi dan tujuan, bukan hanya nama komponen"

# Paragraph & Sentence Guidelines

paragraph_length:
  target: "3-5 kalimat"
  rule: "padat tapi tidak fragmentasi — setiap paragraf satu komponen/konsep utama"

sentence_length:
  target: "20-35 kata (medium-panjang)"
  avoid: "kalimat terlalu pendek yang terkesan choppy"
  use_short_for: "emphasis atau definisi singkat sebelum elaborasi"

transitions:
  type: "relasional, bukan temporal"
  examples: ["terdiri dari", "mencakup", "yang memungkinkan", "sebagai komponen", "di atas lapisan ini"]

# Application to This Project

for_bab_III_tech_stack_justification:
  structure:
    - "gambaran umum stack (Laravel+Filament monolith + Go+Svelte microservice)"
    - "penjelasan tiap komponen: fungsi + kenapa dipilih"
    - "bagaimana komponen saling terhubung (REST/gRPC, Nginx sebagai reverse proxy)"
    - "implikasi untuk deployment di Orange Pi"
  note: "ini bukan Gaya C (komparatif) — fokus pada deskripsi arsitektur yang dipilih, bukan membandingkan opsi"

for_bab_IV_design:
  structure:
    - "overview arsitektur sistem (diagram description atau penjelasan layer)"
    - "tiap modul: tanggung jawab, entitas utama, alur data masuk/keluar"
    - "deployment architecture: Nginx → PHP-FPM → PostgreSQL/MariaDB + Redis + Go service"
  erd_description: "jelaskan relasi antar entitas utama dalam narasi sebelum/setelah diagram"

# Content Checklist

checklist:
  - "flow: overview → detail → implikasi (tiap subseksi)"
  - "setiap komponen dijelaskan fungsi DAN hubungannya dengan komponen lain"
  - "tidak ada bullet points dalam narasi utama"
  - "istilah teknis semua diberi penjelasan atau konteks"
  - "tidak ada kalimat choppy berturut-turut (variasikan panjang)"
  - "transisi relasional, bukan temporal"
