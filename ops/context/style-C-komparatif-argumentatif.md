source: "gaya penulisan.txt — Gaya C"
used_in: ["Bab II subseksi perbandingan/pilihan (e.g., 2.1.3)", "Bab III justifikasi tech stack", "bagian manapun yang membandingkan opsi dan membangun justifikasi"]
function: "membandingkan opsi dan membangun justifikasi pemilihan"

# Core Characteristics

dichotomous_parallel_structure:
  pattern:
    para_1: "Opsi A → deskripsi → kelebihan → kelemahan"
    para_2: "Opsi B (alternatif) → deskripsi → kelebihan → keuntungan dibanding A"
    para_3: "contoh spesifik atau implementasi konkret → relevansi ke penelitian ini"
  rule: "struktur tiap paragraf harus paralel (mirroring) — opsi A dan B dijelaskan dengan kedalaman yang setara"

balanced_evaluation:
  rule: "setiap opsi dijelaskan secara balanced — kelebihan DAN kelemahan"
  avoid: "bias yang terlalu obvious"
  principle: "biarkan data/fakta membentuk kesimpulan, bukan sebaliknya"

explicit_justification:
  rule: "akhiri bagian dengan menghubungkan ke konteks penelitian secara eksplisit"
  example: >
    "Odoo dan ERPNext relevan untuk penelitian ini karena kombinasi antara maturitas, dokumentasi yang baik,
    arsitektur modular, dan kemampuan *deployment* pada infrastruktur beragam—menjadikan keduanya kandidat
    ideal untuk eksplorasi pada perangkat hemat daya..."
  for_this_project: >
    "Laravel + Filament dipilih karena... [alasan]. Go + Svelte untuk microservice finance karena...
    [alasan]. Kombinasi ini memungkinkan [outcome] yang sesuai dengan constraint deployment di Orange Pi."

trade_off_explanation:
  rule: "jelaskan trade-off secara eksplisit — pembaca harus memahami mengapa opsi lain tidak dipilih"
  not_just_listing: "bukan sekadar mendaftar fitur, tapi menjelaskan implikasinya untuk konteks ini"

# Transition Phrases

contrastive_transitions:
  - "Namun, keuntungan tersebut datang dengan..."
  - "Sebagai alternatif yang lebih terjangkau..."
  - "Di sisi lain..."
  - "Sebaliknya..."
  - "Berbeda dengan..."
  - "Meskipun demikian..."

listing_in_sentence:
  rule: "daftar kelebihan/kelemahan dalam satu kalimat dengan koma — bukan bullet"
  example: "Tidak ada biaya lisensi, *source code* tersedia untuk modifikasi, komunitas pengguna yang aktif menyediakan dukungan, dan arsitektur yang modular..."

# Paragraph & Sentence Guidelines

paragraph_length:
  target: "4-6 kalimat per paragraf"
  rule: "tiap paragraf = satu opsi atau satu dimensi perbandingan"

structure_rule:
  mirror: "jika Opsi A dijelaskan dalam 4 kalimat dengan urutan [definisi, kelebihan, kelemahan, contoh], Opsi B harus mengikuti urutan yang sama"

sentences:
  use_contrastive: "aktif gunakan transisi kontrastif di awal paragraf kedua"
  use_enumerative: "daftarkan keunggulan dalam satu kalimat panjang dengan koma untuk efisiensi"

ending_rule:
  must: "setiap bagian komparatif harus diakhiri dengan kalimat yang menghubungkan ke relevansi penelitian/proyek"
  avoid: "jangan biarkan perbandingan menggantung tanpa kesimpulan arah"

# Distinction from Style B

vs_style_B:
  style_B: "deskripsi arsitektur yang SUDAH dipilih — fokus pada 'bagaimana ini bekerja'"
  style_C: "justifikasi mengapa opsi ini dipilih — fokus pada 'mengapa ini, bukan yang lain'"
  note_for_bab_III: >
    Justifikasi tech stack di Bab III = Gaya C (membandingkan Laravel+Filament vs alternatif,
    Go vs alternatif untuk microservice). Deskripsi arsitektur di Bab IV = Gaya B.

# Application to This Project

for_bab_II_new_sections:
  laravel_filament:
    compare_against: "Odoo, ERPNext, atau framework PHP lain (CodeIgniter, Symfony)"
    justify: "dipilih karena [alasan spesifik] yang sesuai dengan kebutuhan custom ERP dari nol"
  microservice_go_svelte:
    compare_against: "opsi lain (Python FastAPI, Node.js) untuk microservice"
    justify: "Go dipilih karena [performa/concurrency], Svelte karena [bundle size/performa di SBC]"

for_bab_III_tech_stack:
  structure:
    - "kondisi saat ini (proses manual/spreadsheet) vs kebutuhan ERP terintegrasi — ini Gaya C"
    - "Laravel+Filament vs alternatif — Gaya C"
    - "pemilihan hardware: Orange Pi vs x86 on-premise — Gaya C (bukan vs VPS)"
  note: "perbandingan hardware hanya on-premise vs on-premise — tidak ada VPS comparison"

# Content Checklist

checklist:
  - "struktur paralel: tiap opsi dijelaskan dengan kedalaman setara"
  - "balanced — setiap opsi punya kelebihan dan kelemahan yang disebutkan"
  - "transisi kontrastif eksplisit di awal paragraf pembanding"
  - "daftar keunggulan dalam satu kalimat dengan koma (bukan bullet)"
  - "ending: selalu hubungkan ke relevansi penelitian/proyek"
  - "trade-off dijelaskan, bukan hanya fitur yang didaftarkan"
  - "tidak ada bias obvious — kesimpulan muncul dari data"
