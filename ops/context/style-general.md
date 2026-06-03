source: "gaya penulisan.txt"
applies_to: all styles

# Universal Rules

language:
  register: "bahasa Indonesia baku, akademik, tidak kaku"
  tone: "formal tapi accessible — seperti artikel ilmiah populer, bukan textbook kering"
  voice: "third-person; gunakan 'penelitian ini', 'studi ini', 'proposal ini' — hindari 'saya'/'kami'"
  passive_active: "variasikan — pasif OK untuk metodologi, aktif untuk narasi"

bilingual_terms:
  rule: "istilah asing ditulis *italic* saat pertama kali muncul per bab"
  format: "*Enterprise Resource Planning* (ERP)"
  exceptions:
    - "nama produk/tools TIDAK italic: Laravel, Filament, Go, Svelte, Redis, Nginx, PostgreSQL, MariaDB, Orange Pi"
    - "akronim yang sudah dijelaskan sebelumnya TIDAK perlu italic ulang"
  always_give_context: true  # jangan asumsikan pembaca tahu semua istilah teknis

citations:
  style: "\\cite{key} atau \\textcite{key} sesuai konteks"
  placement: "langsung setelah klaim/fakta yang dikutip"
  rule: "tidak over-cite — hanya pada klaim faktual dan konsep penting"
  must_not: "jangan tinggalkan referensi tanpa sitasi"

formatting:
  akronim: "(ERP), (MRP), (UMKM)"
  italic: "istilah asing"
  bold: "penekanan pertanyaan penelitian dan poin krusial — gunakan jarang"
  lists_in_narasi: "hindari bullet points — gunakan enumerasi implisit dengan koma"
  lists_formal_sections: "enumerate OK untuk Rumusan Masalah, Tujuan"

consistency_terms:
  - "sistem ERP custom" # bukan 'custom ERP system'
  - "lab pengujian lingkungan" # bukan 'environmental testing lab'
  - "on-premise" # dengan hyphen, konsisten seluruh dokumen

# Sentence & Paragraph Rules

sentence_length:
  short: "15-25 kata"
  medium: "25-35 kata"
  long: "35-45 kata"
  ideal_ratio: "40% pendek, 40% medium, 20% panjang"
  rule: "jangan 3 kalimat panjang berturut-turut"
  max_clauses_per_sentence: 2

paragraph_length:
  standard: "3-4 kalimat"
  complex: "maksimal 5 kalimat"
  transition: "2 kalimat OK"
  rule: "satu ide utama per paragraf"

rhythm:
  pattern: "pendek → panjang → medium → pendek → panjang"
  use_short_for: "emphasis setelah paragraf panjang, transisi"
  use_long_for: "elaborasi konsep kompleks"

# Anti-AI-Stiffness Rules

vary_sentence_opening:
  - "frasa keterangan: 'Pada tahun 1990-an, integrasi MRP...'"
  - "subordinate clause: 'Setelah meledaknya popularitas *cloud computing*, UMKM...'"
  - "participial phrase: 'Berkembang dari kontrol inventori sederhana, MRP kemudian...'"
  rule: "hindari semua kalimat dimulai dengan subjek-predikat"

vary_transitions:
  bad_example: "Pada tahun... (5 kali berturut-turut)"
  good_variants:
    - "Pada 1970-an..."
    - "Dekade 1980 menandai..."
    - "Memasuki tahun 1990..."
    - "Era 2000-an membawa..."
    - "Belakangan ini..."
  relational: ["terdiri dari", "mencakup", "yang memungkinkan", "melalui"]
  contrastive: ["Namun", "Di sisi lain", "Sebaliknya", "Berbeda dengan", "Sementara"]
  natural_not_robotic:
    bad: "Selanjutnya akan dibahas..."
    good: "Perkembangan ini membawa kita pada..."

use_concrete_not_abstract:
  bad: "Vendor besar mendominasi pasar."
  good: "Oracle, SAP, dan Infor menguasai lebih dari 60% pasar ERP global."

avoid_over_precision:
  bad: "terdapat sejumlah besar organisasi yang..."
  good: "banyak organisasi yang..."
  bad2: "mengalami peningkatan yang signifikan"
  good2: "meningkat pesat" atau "meningkat signifikan"

academic_personality_phrases:
  use_sparingly:
    - "Menariknya, perkembangan ini..."
    - "Perlu dicatat bahwa..."
    - "Yang patut diperhatikan adalah..."

rhetorical_devices:
  rhetorical_question: "jarang, hanya untuk transisi penting — 'Lalu, apa yang mendorong perubahan ini?'"
  parallelism: "untuk emphasis — 'ERP tidak hanya mengintegrasikan data, tetapi juga mengintegrasikan proses...'"

# Pre-Finalization Checklist

per_paragraph:
  - "maksimal 4-5 kalimat (3 ideal)"
  - "satu ide utama"
  - "transisi smooth dari paragraf sebelumnya"
  - "tidak ada kalimat dengan lebih dari 2 subordinate clauses"

per_section:
  - "variasi panjang kalimat (tidak semua panjang/pendek)"
  - "variasi struktur kalimat (tidak semua subjek-predikat)"
  - "frasa transisi yang bervariasi (tidak repetitif)"
  - "semua istilah teknis dijelaskan atau diberi konteks"
  - "tidak ada asumsi pengetahuan yang tidak reasonable"
