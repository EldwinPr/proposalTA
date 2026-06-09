erDiagram
    customers {
        ulid id PK
        string nama
        string bidang_usaha
        string produk_jual
        string kredibilitas
        string referensi
        string nomor_telpon_perusahaan
        string nomor_fax_perusahaan
        string email_perusahaan
        string website
        string status_aktif
        string npwp
        string nik
        string tax_name
        ulid tax_address_id FK
    }
    customer_contacts {
        ulid id PK
        ulid customer_id FK
        string nama
        string posisi
        string nomor_telp
        string email
    }
    customer_addresses {
        ulid id PK
        ulid customer_id FK
        string nama
        string country_code
        string provinsi
        string kota_kabupaten
        string alamat
        string kode_pos
    }

    produk_uji {
        ulid id PK
        string nama
        string kode
    }
    regulasi {
        ulid id PK
        ulid produk_uji_id FK
        string nama
        string kode
        string elib_regulation_id
    }
    paket {
        ulid id PK
        ulid produk_uji_id FK
        ulid regulasi_id FK
        string nama
        ulid kode
    }
    paket_parameter {
        ulid id PK
        ulid paket_id FK
        ulid parameter_id FK
        string ambang_batas
        string satuan
    }
    paket_sentral {
        ulid id PK
        ulid produk_uji_id FK
        string nama
        text deskripsi
    }
    paket_sentral_items {
        ulid id PK
        ulid paket_sentral_id FK
        ulid paket_id FK
    }
    paket_sentral_regulasi {
        ulid id PK
        ulid paket_sentral_id FK
        ulid regulasi_id FK
    }
    parameter {
        ulid id PK
        string parameter
        ulid reference_method_id FK
        string duration
        string rumus_kimia
        string jenis_pengerjaan
        string pengawetan
        string batas_penyimpanan
        string status_akreditasi
        boolean status_aktif
        ulid alat_id FK
        ulid wadah_id FK
        integer harga
        string bidang_pengujian
        string sample_size
        ulid produk_uji_id FK
        string loq
    }
    reference_method {
        ulid id PK
        string nama
        string judul
    }
    alat {
        ulid id PK
        string nama
        string kode
        text deskripsi
    }
    unit_alat {
        ulid id PK
        ulid alat_id FK
        string kode
        string lokasi
        text keterangan
    }
    wadah {
        ulid id PK
        string nama
        text deskripsi
        boolean sekali_pakai
        integer jumlah_tersedia
        integer jumlah_dipakai
        integer jumlah_total
    }
    bahan {
        ulid id PK
        string kode
        string nama
        string rumus_kimia
        string nomor_katalog
        double qty
        string unit
        double min_qty
        string kegunaan_analisa
        text sds
        text coa
    }
    kartu_stok {
        ulid id PK
        ulid bahan_id FK
        date tanggal
        string nomor_batch
        date tgl_kadaluarsa
        string keterangan
        string tipe
        double jumlah
        double saldo_setelah
        ulid sample_id FK
        bigint user_id FK
        ulid pengajuan_id FK
        double harga
        string status
    }
    metode_sampling {
        ulid id PK
        ulid produk_uji_id FK
        string nama
        string file_instruksi
    }
    term_of_payments {
        ulid id PK
        string nama
        text deskripsi
    }

    quotations {
        ulid id PK
        string quotation_number
        ulid customer_id FK
        bigint sales_id FK
        ulid customer_contact_id FK
        ulid customer_address_id FK
        double biaya_pengujian
        double biaya_lain
        double sub_total
        double diskon
        double ppn
        double grand_total
        double dp
        string status_terima
        boolean status_approval
        bigint approve_by FK
        timestamp tanggal_approval
        string no_po
        timestamp tanggal_po
        string file_po
        string term_of_payment
        boolean pakai_konsultan
        ulid konsultan_id FK
        ulid konsultan_address_id FK
        ulid konsultan_contact_id FK
        string nama_konsultan
        string alamat_konsultan
        string telpon_konsultan
        timestamp cancel_date
        text cancel_reason
    }
    quotation_details {
        ulid id PK
        ulid quotation_id FK
        ulid produk_uji_id FK
        ulid paket_id FK
        ulid paket_sentral_id FK
        ulid lokasi_sampling FK
        string titik_sampling
        integer jumlah_titik
        string tipe_sampling
        string periode_frekuensi
        integer frekuensi_sampling
        string tujuan_sampling
        string catatan_sampling
        string permintaan_tanggal
        boolean express
        double harga_parameter
        double tambahan_express
        double diskon
        double sub_total
        string longitude
        string latitude
        boolean is_composite_titik
        boolean is_composite_frekuensi
        string group_id
        text metode_sampling_ids
        boolean is_resample
        string parent_sales_order_detail_id FK
    }
    quotation_detail_parameters {
        ulid id PK
        ulid quotation_detail_id FK
        ulid parameter_id FK
        string ambang_batas
        string satuan
        double harga_asli
        double penambahan_harga
        string parameter
    }
    quotation_detail_regulations {
        ulid id PK
        ulid quotation_detail_id FK
        ulid regulasi_id FK
    }
    quotation_additional_costs {
        ulid id PK
        ulid quotation_id FK
        ulid additional_cost_id FK
        double kuantitas
        double harga
        double diskon
        double total
    }
    additional_cost {
        ulid id PK
        string nama
        text deskripsi
        boolean flag_active
    }
    quotation_revisions {
        ulid id PK
        ulid quotation_id FK
        integer revisi_ke
        text alasan_revisi
        ulid customer_id FK
        bigint sales_id FK
        double grand_total
        string status_terima
    }

    sales_orders {
        ulid id PK
        ulid quotation_id FK
        string no_so
        ulid customer_id FK
        integer qty
        text catatan_sampling
        string status
    }
    sales_order_details {
        ulid id PK
        string kode_titik
        ulid sales_order_id FK
        ulid quotation_detail_id FK
        string pengambilan_id FK
        integer titik_sampling
        boolean is_composite_titik
        string frekuensi
        boolean is_composite_frekuensi
        string status
        string tipe_sampling
        boolean is_wadah_customer
        boolean sudah_diambil
        integer nomor_urut
        string certificate_file
    }
    certificates {
        ulid id PK
        ulid sales_order_detail_id FK
        string file
        string tipe
    }
    pengambilan {
        ulid id PK
        ulid sales_order_id FK
        string pengambilan_nomor
        bigint petugas_id FK
        text delevery_address
        text invoice_address
        text sampling_address
        text certificate_address
        date tanggal_sampling
        integer total_waktu
        string satuan_waktu
        string customer_contact_id FK
        string tipe_sampling
        string status
    }
    jadwal_pengambilan {
        ulid id PK
        ulid pengambilan_id FK
        date tanggal
        string waktu_mulai
        string waktu_selesai
    }
    samples {
        ulid id PK
        ulid sales_order_details_id FK
        ulid quotation_detail_id FK
        string status
        string tipe_sampling
        boolean wadah_disiapkan
        ulid wadah_id FK
        integer wadah_qty
        integer nomor_urut
        timestamp received_at
        text catatan_abnormalitas
        string parameter
        string pengambilan_id FK
        bigint penyiap_id FK
        bigint penerima_id FK
    }
    sample_parameter {
        ulid id PK
        ulid quotation_detail_id FK
        ulid sample_id FK
        ulid parameter_id FK
        string ambang_batas
        string satuan
        ulid sales_order_details_id FK
        string status
        string jenis
        ulid pengujian_id FK
        string alasan_tolak
        string parent_sample_parameter_id FK
        bigint analyst_id FK
        string worksheet_url
        string penyelia_id FK
        timestamp diselia_at
        string hasil_akhir
    }
    pengujian {
        ulid id PK
        ulid alat_id FK
        bigint analyst_id FK
        string status
        timestamp started_at
        timestamp selesai_at
        boolean express
        ulid unit_alat_id FK
        string jenis
        string worksheet_url
        text kondisi_awal_alat
        text kondisi_akhir_alat
    }
    resample_requests {
        ulid id PK
        string status
        string alasan_supervisor
        bigint requested_by FK
        bigint approved_by FK
        timestamp approved_at
        bigint sales_id FK
        timestamp draft_sent_at
        decimal harga_resample
        string pengujian_id FK
        string sales_order_detail_id FK
        decimal percepatan
        decimal disc
    }
    users {
        bigint id PK
        string name
        string email
        ulid division_id FK
        ulid lingkup_id FK
    }

    pengajuan {
        ulid id PK
        string no_pr
        ulid coa_pengajuan_id FK
        string barang
        string type
        string tujuan
        bigint harga
        date tanggal_dibutuhkan
        integer lama_pengerjaan
        text keterangan
        string status
        string file_brosur
        date tanggal_pengajuan
        bigint user_id FK
        ulid bahan_id FK
        double jumlah
        ulid rekening_id FK
    }
    bayar {
        ulid id PK
        ulid pengajuan_id FK
        bigint nominal
        string file_bukti_transfer
    }
    coa_pengajuan {
        ulid id PK
        string account_code
        string account_name
        text deskripsi
    }
    rekening_perusahaan {
        ulid id PK
        string nama_bank
        string no_rek
        string atas_nama
    }
    rekening_user {
        ulid id PK
        string code
        string nama_bank
    }

    customers ||--o{ customer_contacts : "has"
    customers ||--o{ customer_addresses : "has"
    customers ||--o{ quotations : "has"
    customers }o--|| customer_addresses : "tax address"

    produk_uji ||--o{ regulasi : "has"
    produk_uji ||--o{ paket : "has"
    produk_uji ||--o{ metode_sampling : "has"
    produk_uji ||--o{ parameter : "has"
    regulasi ||--o{ paket : "has"
    paket ||--o{ paket_parameter : "has"
    paket ||--o{ paket_sentral_items : "in"
    paket_sentral ||--o{ paket_sentral_items : "has"
    paket_sentral ||--o{ paket_sentral_regulasi : "has"
    regulasi ||--o{ paket_sentral_regulasi : "in"
    parameter ||--o{ paket_parameter : "in"
    parameter }o--|| reference_method : "uses"
    parameter }o--|| alat : "uses"
    parameter }o--|| wadah : "uses"
    alat ||--o{ unit_alat : "has"

    bahan ||--o{ kartu_stok : "has"
    samples ||--o{ kartu_stok : "uses"
    users ||--o{ kartu_stok : "by"
    pengajuan ||--o{ kartu_stok : "from"

    quotations }o--|| customers : ""
    quotations }o--|| customer_addresses : ""
    quotations }o--|| customer_contacts : ""
    quotations }o--|| users : "sales"
    quotations }o--|| users : "approve_by"
    quotations ||--o{ quotation_details : "has"
    quotations ||--o{ quotation_additional_costs : "has"
    quotations ||--o{ quotation_revisions : "has"
    quotation_details }o--|| produk_uji : ""
    quotation_details }o--|| paket : ""
    quotation_details }o--|| paket_sentral : ""
    quotation_details }o--|| customer_addresses : "lokasi"
    quotation_details ||--o{ quotation_detail_parameters : "has"
    quotation_details ||--o{ quotation_detail_regulations : "has"
    quotation_detail_parameters }o--|| parameter : ""
    quotation_detail_regulations }o--|| regulasi : ""
    quotation_additional_costs }o--|| additional_cost : ""

    sales_orders }o--|| quotations : ""
    sales_orders }o--|| customers : ""
    sales_orders ||--o{ sales_order_details : "has"
    sales_orders ||--o{ pengambilan : "has"
    sales_order_details }o--|| quotation_details : ""
    sales_order_details }o--o| pengambilan : ""
    sales_order_details ||--o{ samples : "has"
    sales_order_details ||--o{ sample_parameter : "has"
    sales_order_details ||--o{ certificates : "has"
    pengambilan }o--|| users : "petugas"
    pengambilan }o--|| customer_contacts : ""
    pengambilan ||--o| jadwal_pengambilan : "has"
    samples }o--|| wadah : ""
    samples }o--|| users : "penyiap"
    samples }o--|| users : "penerima"
    sample_parameter }o--|| parameter : ""
    sample_parameter }o--|| samples : ""
    sample_parameter }o--|| pengujian : ""
    sample_parameter }o--|| users : "analyst"
    pengujian }o--|| alat : ""
    pengujian }o--|| unit_alat : ""
    pengujian }o--|| users : "analyst"
    resample_requests }o--|| users : "requested_by"
    resample_requests }o--|| users : "approved_by"
    resample_requests }o--|| sales_order_details : ""
    resample_requests }o--|| pengujian : ""

    pengajuan }o--|| coa_pengajuan : ""
    pengajuan }o--|| users : ""
    pengajuan }o--|| bahan : ""
    pengajuan }o--|| rekening_perusahaan : ""
    bayar }o--|| pengajuan : ""