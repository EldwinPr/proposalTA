source: "gaya penulisan.txt — Gaya A"
used_in: ["Latar Belakang (Bab I)", "Bab II bagian pengantar/historis (e.g., 2.1.1)"]
function: "membangun konteks, motivasi, dan gap penelitian"

# Core Characteristics

storytelling:
  approach: "alur kronologis — bangun pemahaman dari konsep sederhana ke kompleks"
  technique: "sebutkan peristiwa historis, vendor, dan tokoh teknologi untuk konkretisasi"
  example: "Sejak pertama kali komputer dikenalkan pada tahun 1960, banyak kelompok yang membuat aplikasi untuk mencatat sumber daya..."

argument_structure:
  layers: "konteks historis umum → perkembangan relevan → detail teknis → gap penelitian"
  rule: "bangun argumen secara incremental, jangan langsung ke kesimpulan"
  ending: "pertanyaan penelitian yang eksplisit dan bold"

temporal_transitions:
  examples: ["Sejak pertama kali...", "Pada tahun...", "Kemudian...", "Hingga saat ini...", "Memasuki era..."]
  rule: "variasikan frasa temporal — hindari repetisi 'Pada tahun' terus-menerus"
  show: "perkembangan waktu dan evolusi konsep"

local_contextualization:
  rule: "hubungkan topik global ke konteks Indonesia atau domain spesifik"
  for_this_project: "hubungkan ke lab pengujian lingkungan komersil sebagai domain yang butuh ERP on-premise"

gap_analysis_structure:
  para_1: "review 2-3 penelitian terkait + keterbatasannya masing-masing"
  para_2: "identifikasi gap spesifik + pertanyaan penelitian (bold)"
  template: "Penelitian X menunjukkan A, namun terbatas pada B. Penelitian Y mengeksplorasi C, tetapi belum mencakup D. Gap yang teridentifikasi adalah E dan F..."
  gap_for_this_project: "dari 'belum ada data empiris SBC vs VPS' → 'belum ada implementasi ERP custom untuk domain lab pengujian lingkungan yang berjalan di SBC'"

# Paragraph & Sentence Guidelines

paragraph_length:
  target: "4-5 kalimat (boleh hingga 6 untuk narasi historis yang padat)"
  proportion: "50% konteks/sejarah, 50% gap dan relevansi — jangan lebih berat ke konteks"

sentence_length:
  mix: "kalimat pendek untuk emphasis, panjang untuk elaborasi historis"
  max_clauses: 2
  complex_sentence_use: "hanya untuk transisi atau menyatukan konsep erat"

  bad_example: >
    "Perkembangan teknologi ARM yang berkelanjutan telah meningkatkan kemampuan komputasional SBC secara signifikan,
    yang awalnya hanya digunakan sebagai *microcontroller* telah berubah menjadi komputer bahkan *server*,
    dan pada penelitian berjudul '...' peneliti berhasil menjalankan *web server* menggunakan Raspberry Pi 4,
    walaupun berhasil menjalankan *web server*, penelitian tersebut hanya menguji skenario yang relatif sederhana..."
  bad_reason: "1 kalimat 80+ kata, 4+ clauses — terlalu padat"

  good_example: >
    "Perkembangan teknologi ARM yang berkelanjutan telah meningkatkan kemampuan komputasional SBC secara signifikan.
    SBC yang awalnya hanya digunakan sebagai *microcontroller* kini telah berubah menjadi komputer bahkan *server*.

    Beberapa penelitian telah mengeksplorasi penggunaan SBC untuk aplikasi *server*. Pada penelitian
    'Implementasi *Cluster Server* Pada Raspberry Pi...', peneliti berhasil menjalankan *web server* menggunakan
    Raspberry Pi 4 \cite{Putra2019}. Namun, penelitian tersebut hanya menguji skenario yang relatif sederhana—
    spesifiknya *web server* dengan *traffic* HTTP. Skenario ini tidak representative terhadap kompleksitas
    aplikasi ERP yang melibatkan operasi *database* intensif, manajemen *state* kompleks, dan interaksi
    *multi-user concurrent* simultan."
  good_reason: "2 paragraf (2+4 kalimat), variasi panjang kalimat, transisi jelas"

# Trade-offs to Watch

long_paragraphs:
  original_style: "6-8 kalimat"
  recommendation: "4-5 kalimat — balance kepadatan dan readability"

complex_sentences:
  use_for: "kalimat transisi atau yang menyatukan konsep sangat erat"
  alternative: "pecah menjadi 2 kalimat jika melebihi 2 clauses"

implicit_topic_transitions:
  risk: "pembaca kehilangan thread"
  fix: "tambahkan frasa transisi halus — 'Ketertarikan UMKM ini didorong oleh...', 'Hal ini disebabkan oleh...'"

historical_detail_filter:
  question: "Apakah detail ini penting untuk memahami gap penelitian atau evolusi konsep?"
  if_no: "hapus — jangan sebutkan vendor/peristiwa yang tidak mendukung argumen"

assumed_knowledge:
  risk: "pembaca tidak familiar dengan 'dotcom bubble', 'Y2K', dll."
  fix: "beri konteks singkat dalam kurung atau dash — 'gelembung *dotcom* (2001)—krisis ekonomi yang...'"

# Signposting

optional_preview:
  good: "Bagian ini akan menjelaskan..." atau "Berikut akan dibahas..."
  rule: "opsional — jangan berlebihan; bisa langsung masuk narasi jika flow sudah jelas"

# Content Checklist for Latar Belakang

checklist:
  - "proporsi 50% konteks + 50% gap"
  - "gap research dalam 2 paragraf terstruktur (review penelitian + identifikasi gap)"
  - "pertanyaan penelitian bold dan standalone atau di akhir paragraf dengan emphasis"
  - "semua detail historis relevan untuk argumen"
  - "ada kontekstualisasi lokal (domain lab pengujian lingkungan)"
  - "temporal transitions bervariasi"
