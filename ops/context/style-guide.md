source: "gaya penulisan.txt (full file in repo root)"

# Style Files Index

general:    "style-general.md    — universal rules: bilingual terms, citations, sentence/paragraph length, anti-AI-stiffness"
style_A:    "style-A-naratif-historis.md    — Latar Belakang, Bab II intro sections; chronological, gap-analysis"
style_B:    "style-B-teknis-deskriptif.md   — Bab II arsitektur, Bab III kebutuhan, Bab IV desain; structural, relational"
style_C:    "style-C-komparatif-argumentatif.md — Bab II/III justifikasi, perbandingan opsi; parallel structure, trade-offs"

# Which Style Per Section

section_style_map:
  "Bab I - Latar Belakang":         A
  "Bab I - Rumusan Masalah/Tujuan": general  # formal enumerate format
  "Bab II - 2.1.1 sejarah ERP":     A
  "Bab II - arsitektur/komponen":   B
  "Bab II - Laravel+Filament":      C
  "Bab II - microservice Go+Svelte": C
  "Bab II - ISO 17025 / LIMS":      B
  "Bab III - kondisi saat ini":     A + C  # narasi kondisi → justifikasi kebutuhan ERP
  "Bab III - kebutuhan fungsional": B
  "Bab III - justifikasi tech stack": C
  "Bab III - justifikasi hardware": C
  "Bab IV - arsitektur sistem":     B
  "Bab IV - desain modul":          B
  "Bab V - rencana pengembangan":   B + general
