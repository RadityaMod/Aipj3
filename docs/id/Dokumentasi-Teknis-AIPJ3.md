# Dokumentasi Teknis dan Strategi — Situs Web AIPJ3

**RFP:** RFP/Website Development/018-08-2026
**Sifat dokumen:** materi pendukung penyusunan proposal — satu dokumen untuk seluruh sisi teknis.
**Bahasa:** Indonesia. Proposal resmi wajib berbahasa Inggris; dokumen ini sumbernya.

## Isi

1. Ringkasan — kenapa pendekatan ini
2. Strategi: di mana penawaran ini dimenangkan
3. Metodologi kerja
4. Rekomendasi struktur halaman
5. Desain sistem
6. Requirement fungsional
7. Requirement non-fungsional
8. Rencana pengujian dan penerimaan
9. Rencana pemeliharaan 12 bulan
10. Risiko dan hal yang perlu didiskusikan

---

## 1. Ringkasan — kenapa pendekatan ini

Dua kendala menentukan seluruh rancangan di bawah.

**Pagu tetap bertemu tahap penemuan.** Anggaran IDR 150.000.000 sudah dikunci, sementara Tahap 1
justru baru akan menghasilkan peta situs dan hierarki konten bersama pemangku kepentingan. Kalau
setiap hasil lokakarya berarti menulis kode baru, margin habis sebelum pembangunan selesai.

> **Jawabannya: bangun platform, bukan situs.** Dua belas blok konten siap pakai. Menambah jenis
> halaman berarti menyusun blok, bukan memprogram. Hasil Tahap 1 menjadi konfigurasi, bukan
> pekerjaan ulang.

**SLA berat bertemu tim kecil.** Kontrak menuntut ketersediaan 99,9%, tambalan keamanan kritis
dalam 48 jam, dan pemantauan selama 12 bulan.

> **Jawabannya: situs statis.** Halaman disajikan sebagai berkas mati dari CDN. Tidak ada server
> publik yang bisa jatuh atau diserang. **CMS mati tidak membuat situs ikut mati.** SLA 99,9%
> berubah dari janji aplikasi menjadi janji CDN — jauh lebih murah untuk ditepati.

Kedua jawaban itu bukan penghematan. Keduanya keputusan rekayasa yang membuat kontrak ini bisa
diselesaikan dengan baik pada anggaran yang tersedia.

---

## 2. Strategi: di mana penawaran ini dimenangkan

| Kriteria penilaian | Bobot |
|---|---:|
| **Pendekatan dan metodologi** | **50%** |
| Kualifikasi dan personel kunci | 30% |
| Pengalaman organisasi | 20% |

Blok metodologi berbobot lebih besar daripada pengalaman organisasi dan personel digabungkan.
Dan RFP membuka ruang pilihan teknologi sendiri: *"Provider could identify other than the list
with description of its advantages and disadvantages."*

Sebagian besar peserta akan menyalin ulang tabel teknologi RFP sebagai daftar centang. Itu hanya
bernilai *memenuhi syarat*. Lima hal berikut yang membuat penawaran ini berbeda.

**1. Menyelesaikan kontradiksi hosting secara terbuka.** RFP mensyaratkan penyedia lokal di bagian
pemeliharaan, tetapi menyebut AWS/Azure/Vercel/Cloudflare di tabel penilaian. Kita nyatakan
penafsiran kita, bukan mendiamkannya. Ini membuktikan dokumen dibaca utuh.

**2. Menghitung biaya CMS secara jujur.** Lisensi CMS berbayar adalah biaya berulang yang berlanjut
**setelah kontrak berakhir** — dan itu menjadi tanggungan AIPJ3, bukan kita. Kita sajikan
perbandingan biaya 12 dan 36 bulan.

**3. Menganggarkan pengujian nyata bersama penyandang disabilitas.** Ruang lingkup menulis
*"accessibility audit including with people with disability"* — bukan pemindaian otomatis. Ini
terhubung langsung dengan **EOPO 3: akses keadilan setara bagi perempuan, anak, dan penyandang
disabilitas.** Panel yang berasal dari program ini akan mengenali kerangka hasil mereka sendiri.
Pembeda terkuat yang tersedia, dan hampir pasti dilewatkan pesaing.

**4. Membuka dengan pengalaman penyunting, bukan nama kerangka kerja.** Kebutuhan riil klien adalah
staf komunikasi non-teknis bisa menerbitkan konten mingguan tanpa memanggil developer.

**5. Menyerahkan rencana kerja yang tanggalnya konsisten.** RFP memuat beberapa ketidakcocokan
tanggal. Kita tidak mengoreksi klien — kita cukup menyerahkan jadwal yang masuk akal.

---

## 3. Metodologi kerja

Empat tahap kontrak sudah selaras dengan alur design thinking. Kita gunakan itu apa adanya.

| Tahap kontrak | Fase design thinking | Pertanyaan yang dijawab |
|---|---|---|
| 1. Konsep Desain | Empathize + Define | Siapa penggunanya, apa yang mereka cari, bagaimana isinya ditata |
| 2. Pengembangan | Ideate + Prototype | Seperti apa wujudnya, dan apakah benar-benar bekerja |
| 3. Peluncuran | Test | Apakah bertahan di dunia nyata |
| 4. Pemeliharaan | Iterate | Apa yang perlu diperbaiki setelah dipakai |

### Tahap 1 — Konsep Desain (15 Sep – 15 Okt 2026)

**Tiga persona** yang kita bawa ke lokakarya sebagai bahan diskusi:

| Persona | Yang dicari | Sinyal kepercayaan yang dibutuhkan |
|---|---|---|
| Pejabat lembaga hukum Indonesia | Dokumen kebijakan, bukti kerja sama, rujukan resmi | Kejelasan kelembagaan, bahasa Indonesia, dapat diunduh |
| Pemangku kepentingan DFAT dan Australia | Kemajuan program, akuntabilitas, hasil terukur | Data, pelaporan berkala, penelusuran ke EOPO |
| Masyarakat sipil dan publik Indonesia | Cerita dampak, cara terlibat, akses informasi | Bahasa sederhana, aksesibel, mudah dibagikan |

Ketiganya punya tingkat literasi dan kebutuhan aksesibilitas berbeda. Itu satu masalah desain, bukan
tiga audiens yang berebut beranda.

**Keluaran tahap ini:** daftar kebutuhan tertulis, tiga persona, peta perjalanan, peta situs,
wireframe empat template, dan arah visual — semua ditandatangani sebagai Keluaran 1.

**Pemeriksaan teknis wajib di tahap ini:** memastikan penyedia hosting mendukung header HTTP kustom
dan API pembersihan cache. Bila gagal, arsitekturnya yang berubah — jadi ini harus tuntas sebelum
pekerjaan infrastruktur dimulai.

### Tahap 2 — Pengembangan (16 Okt 2026 – 22 Jan 2027)

Urutan kerjanya:

1. Infrastruktur dan pipeline CI
2. Design system dan dua belas blok konten
3. Model konten dan kontrol akses
4. Template halaman
5. Pencarian dan analitik
6. Pengerasan keamanan dan audit

**Kontrol akses dikerjakan lebih awal** karena bentuk semua pekerjaan sesudahnya bergantung padanya.

### Tahap 3 — Peluncuran (23–29 Jan 2027)

Gladi bersih di infrastruktur setara produksi, penurunan TTL DNS sebelum pemindahan, konfigurasi
SSL, penerapan, lalu pemantauan pengguna nyata. Versi lama tetap tayang sampai versi baru
terverifikasi.

### Tahap 4 — Pemeliharaan (29 Jan 2027 – 28 Jan 2028)

Rinciannya di Bagian 9.

---

## 4. Rekomendasi struktur halaman

> **[PERLU DIDISKUSIKAN]**
> **Dibahas dengan:** AIPJ3, pada lokakarya Tahap 1
> **Sifat:** usulan awal untuk ditanggapi, bukan keputusan. Peta situs final adalah Keluaran 1 dan
> ditandatangani klien.
> **Kenapa tetap diusulkan sekarang:** lokakarya berjalan jauh lebih cepat bila ada bahan konkret
> untuk disetujui atau ditolak, dibanding memulai dari halaman kosong.

### Peta situs usulan

```
/                             Beranda
/tentang
    /tentang/program          Apa itu AIPJ3, tujuan, jangka waktu
    /tentang/tata-kelola      Peran DFAT, Pemerintah Indonesia, DT Global
/hasil-program                Ikhtisar empat EOPO
    /hasil-program/eopo-1     Supremasi hukum dan pembangunan ekonomi
    /hasil-program/eopo-2     Pencegahan ekstremisme dan kejahatan transnasional
    /hasil-program/eopo-3     Akses keadilan setara
    /hasil-program/eopo-4     Kemitraan
/publikasi                    Indeks, dengan filter
    /publikasi/[slug]         Detail dan unduhan
/berita                       Indeks
    /berita/[slug]            Detail
/agenda                       Indeks kegiatan
    /agenda/[slug]            Detail
/mitra                        Lembaga mitra
/kontak                       Formulir dan informasi kontak
/pencarian                    Hasil pencarian
/aksesibilitas                Pernyataan aksesibilitas
/kebijakan-privasi            Privasi dan cookie
```

Semua tersedia dalam dua bahasa: `/en/...` dan `/id/...`.

### Kenapa EOPO jadi tulang punggung

Setiap publikasi, berita, dan kegiatan ditandai ke satu atau lebih EOPO. Akibatnya seluruh situs
bisa ditelusuri berdasarkan hasil program — persis cara DFAT dan Pemerintah Indonesia menalar
program ini.

Ini yang mengubah *"mendokumentasikan kemajuan, pembelajaran, dan dampak"* dari sekadar blog
kronologis menjadi arsitektur informasi yang benar-benar punya struktur.

### Rincian halaman utama

| Halaman | Tujuan | Audiens utama | Isi kunci |
|---|---|---|---|
| **Beranda** | Menjelaskan apa itu AIPJ3 dalam 10 detik, lalu mengarahkan | Ketiganya | Pernyataan program, empat pintu EOPO, sorotan terbaru, publikasi terbaru |
| **Hub EOPO** | Menjawab "apa hasilnya di bidang ini" | DFAT, lembaga hukum | Narasi hasil, publikasi terkait, berita terkait, mitra terlibat |
| **Indeks publikasi** | Menemukan dan mengunduh dokumen | Lembaga hukum, DFAT | Filter EOPO, jenis, tahun, bahasa; hasil dengan sampul dan ringkasan |
| **Detail publikasi** | Memberi konteks sebelum mengunduh | Semua | Abstrak, metadata, tombol unduh, ukuran berkas, publikasi terkait |
| **Indeks berita** | Menunjukkan program ini hidup | Publik, media | Daftar kronologis, filter EOPO |
| **Detail berita** | Menyampaikan cerita dampak | Publik | Isi kaya, kutipan, gambar dengan alt text, tombol berbagi |
| **Mitra** | Menunjukkan legitimasi dan jejaring | Semua | Logo dan profil singkat, dikelompokkan per kategori |
| **Aksesibilitas** | Menyatakan tingkat kepatuhan dan jalur pengaduan | Penyandang disabilitas | Status WCAG 2.2 AA, keterbatasan yang diketahui, kontak umpan balik |

**Catatan soal halaman aksesibilitas.** Halaman ini praktik baik WCAG dan lazim diwajibkan untuk
lembaga publik, tetapi hampir selalu dilupakan peserta tender. Mencantumkannya — beserta
keterbatasan yang jujur dan jalur pengaduan — memperkuat posisi pada EOPO 3.

### Template yang perlu dibangun

Tiga belas template, bukan puluhan halaman:

1. Beranda · 2. Halaman statis · 3. Hub EOPO · 4. Indeks publikasi · 5. Detail publikasi ·
6. Indeks berita · 7. Detail berita · 8. Indeks agenda · 9. Detail agenda · 10. Mitra ·
11. Kontak · 12. Hasil pencarian · 13. Halaman galat 404/500

---

## 5. Desain sistem

### Dua bagian dengan tuntutan ketersediaan berbeda

```
┌─────────────────────────────┐        ┌──────────────────────────────┐
│  SITUS PUBLIK               │        │  PLATFORM REDAKSI            │
│                             │        │                              │
│  Next.js 15 → berkas statis │        │  Payload v3 + PostgreSQL     │
│  Object storage Indonesia   │        │  Server admin privat         │
│  CDN + WAF                  │        │  Akses terbatas, trafik kecil│
│                             │        │                              │
│  Ketersediaan: 99,9%        │        │  Ketersediaan: tidak kritis  │
│  Tanpa server, tanpa basis  │        │                              │
│  data, tanpa rahasia        │        │                              │
└─────────────────────────────┘        └──────────────────────────────┘
              ▲                                       │
              │      pipeline CI membangun ulang      │
              └───────────────────────────────────────┘
```

**Sifat terpenting rancangan ini:** kedua bagian tidak saling menjatuhkan. CMS mati, situs tetap
tayang. Pembangunan gagal, versi sebelumnya tetap tayang. Server admin diserang, situs publik tidak
terpengaruh karena ia hanya berkas mati.

### Alur penerbitan

```
Penyunting menerbitkan di Payload
  → hook mengirim sinyal ke pipeline
  → GitHub Actions mengambil konten lewat API
  → Next.js membangun berkas statis
  → disalin ke object storage
  → cache CDN dibersihkan
  → tayang dalam 3–6 menit
```

Kecepatan ini memadai karena kontrak menuntut pembaruan **mingguan**. Untuk koreksi mendesak
tersedia jalur cepat: pemicu manual pada pipeline yang sama, terdokumentasi dan dilatihkan.

### Pratinjau draf

Penyetuju harus bisa melihat draf sebelum menerbitkan. Satu basis kode dengan dua mode, dipilih
lewat variabel `BUILD_TARGET`: mode statis untuk produksi, mode server untuk pratinjau. Pratinjau
berjalan terkunci di server admin. Tidak perlu aplikasi ketiga.

### Model konten

**Koleksi:** `pages`, `news`, `publications`, `events`, `partners`, `people`, `eopos`, `media`
**Global:** `navigation`, `siteSettings`, `footer`, `homepage`

**Dua belas blok:** `richText`, `mediaWithCaption`, `quote`, `statistic`, `accordion`, `cardGrid`,
`callToAction`, `embed`, `publicationList`, `newsList`, `partnerLogos`, `timeline`

### Dwibahasa

Bahasa Inggris dan Indonesia sebagai kolom terpisah pada setiap ruas terjemahkan — bukan plugin
terjemahan yang ditempel belakangan. Berkas publikasi juga bersifat per bahasa, sehingga laporan
yang hanya terbit dalam bahasa Indonesia tetap terwakili dengan wajar.

**Bila terjemahan belum ada:** tampilkan versi Inggris disertai keterangan bahwa versi Indonesia
belum tersedia, dan tandai bagian itu dengan `lang="en"`. Jangan pernah mencampur dua bahasa dalam
satu halaman tanpa penanda — itu menyesatkan pembaca dan membuat pembaca layar salah melafalkan.

### Peran dan alur persetujuan

| Peran | Kewenangan |
|---|---|
| `contributor` | Membuat dan menyunting draf saja |
| `editor` | Menyunting dan mengajukan untuk persetujuan — tim komunikasi |
| `approver` | Menerbitkan — Strategic Communications Manager |
| `admin` | Administrasi teknis dan pengelolaan pengguna |

Status dokumen: **draf → ditinjau → disetujui → terbit**, dengan riwayat versi sebagai jejak audit.

Penerbitan dikunci pada peran `approver`. **Inilah mekanisme persetujuan DFAT yang dijadikan
mekanis** — tidak bisa dilewati oleh siapa pun yang sedang terburu-buru.

---

## 6. Requirement fungsional

Apa yang harus **bisa dilakukan** sistem. Semuanya dapat diuji.

### Situs publik

| ID | Requirement | Kriteria diterima |
|---|---|---|
| FR-01 | Setiap halaman tersedia dalam Inggris dan Indonesia | Pemilih bahasa berpindah ke halaman yang sama, bukan ke beranda |
| FR-02 | Pencarian seluruh situs | Kata kunci menemukan isi halaman, berita, dan publikasi di kedua bahasa |
| FR-03 | Filter publikasi | Dapat disaring per EOPO, jenis, tahun, dan bahasa; filter dapat digabung |
| FR-04 | Unduh berkas publikasi | Berkas terunduh; ukuran dan format tampil sebelum diklik |
| FR-05 | Penandaan EOPO pada seluruh konten | Setiap publikasi, berita, dan kegiatan tertaut ke minimal satu EOPO |
| FR-06 | Konten terkait | Halaman detail menampilkan item lain dengan EOPO sama |
| FR-07 | Formulir kontak | Kiriman terkirim dan pengirim menerima konfirmasi; dilindungi anti-spam |
| FR-08 | Berbagi ke media sosial | Tautan berbagi menghasilkan pratinjau benar di tiap bahasa |
| FR-09 | Banner persetujuan cookie | Pengunjung dapat menerima atau menolak per kategori; pilihan tersimpan |
| FR-10 | Halaman galat dwibahasa | 404 dan 500 tampil dalam bahasa yang sedang dipakai, dengan jalur kembali |
| FR-11 | Peta situs XML otomatis | Terbentuk per bahasa dan mutakhir setiap kali situs dibangun |

### Sisi pengelolaan konten

| ID | Requirement | Kriteria diterima |
|---|---|---|
| FR-12 | Kelola seluruh jenis konten | Penyunting dapat membuat, menyunting, dan menghapus tanpa bantuan developer |
| FR-13 | Alur persetujuan | Draf tidak dapat terbit tanpa persetujuan peran `approver` |
| FR-14 | Kontrol akses empat peran | Setiap peran hanya dapat melakukan yang menjadi haknya — diuji menyeluruh |
| FR-15 | Pratinjau draf | Penyetuju melihat wujud akhir sebelum menerbitkan |
| FR-16 | Riwayat versi | Setiap perubahan tercatat pelaku dan waktunya; dapat dikembalikan |
| FR-17 | Unggah media | Gambar wajib punya alt text dalam **dua bahasa**; tanpa itu tidak bisa disimpan |
| FR-18 | Susun halaman dari blok | Halaman baru dibuat dengan menyusun blok, tanpa menulis kode |
| FR-19 | Kelola navigasi | Menu diubah dari CMS, tidak perlu penerapan ulang |
| FR-20 | Penerbitan terjadwal | Konten dapat dijadwalkan terbit pada tanggal tertentu |

---

## 7. Requirement non-fungsional

**Seberapa baik** sistem harus bekerja. Ini yang biasanya menjadi sumber sengketa bila tidak
dituliskan angkanya.

| ID | Aspek | Target | Cara diukur |
|---|---|---|---|
| NFR-01 | Kecepatan muat | LCP < 2,5 detik | Lighthouse CI tiap build; data pengguna nyata setelah tayang |
| NFR-02 | Responsivitas interaksi | INP < 200 ms | Sama |
| NFR-03 | Kestabilan tata letak | CLS < 0,1 | Sama |
| NFR-04 | Skor Lighthouse | ≥ 90 seluruh kategori | Ambang wajib di CI — build gagal bila di bawahnya |
| NFR-05 | Aksesibilitas | WCAG 2.2 Level AA | Pemeriksaan otomatis tiap build **plus** sesi uji bersama penyandang disabilitas |
| NFR-06 | Ketersediaan | ≥ 99,9% per bulan | Pemantauan dari luar; setara jatah henti ±43 menit/bulan |
| NFR-07 | Waktu konten tayang | ≤ 6 menit sejak diterbitkan | Diuji pada UAT |
| NFR-08 | Tambalan keamanan kritis | ≤ 48 jam sejak rilis | Dicatat dan dilaporkan bulanan |
| NFR-09 | Cadangan | Harian, luar lokasi, penyedia berbeda | **Uji pemulihan tiap bulan** ke basis data kosong |
| NFR-10 | Keamanan transport | TLS 1.3, HSTS, CSP, WAF | Pemindaian header dan konfigurasi tiap rilis |
| NFR-11 | Kerentanan | Tidak ada celah kritis terbuka | Pemindaian dependensi otomatis; tinjauan OWASP tiap rilis |
| NFR-12 | Kedaulatan data | Data berada di Indonesia | Konfigurasi infrastruktur, diperiksa di Tahap 1 |
| NFR-13 | Dukungan peramban | Chrome, Firefox, Safari, Edge — dua versi terakhir | Pengujian otomatis lintas peramban |
| NFR-14 | Rentang layar | 320 px hingga 2560 px | Pengujian pada tiga titik henti |
| NFR-15 | Privasi | Tidak ada pelacakan sebelum persetujuan | Diperiksa manual pada UAT |
| NFR-16 | Ketahanan lonjakan trafik | Tidak terpengaruh | Berkas statis di CDN — tidak ada server yang bisa jenuh |
| NFR-17 | Kebebasan berpindah | Tanpa kunci vendor | Seluruh komponen berlisensi MIT atau standar terbuka |
| NFR-18 | Kemudahan pemeliharaan | Dapat dilanjutkan pihak lain | Panduan operasional, catatan keputusan, dan infrastruktur sebagai kode |

**Catatan NFR-17.** Payload berlisensi MIT, basis datanya PostgreSQL, penyimpanannya standar. Saat
kontrak berakhir AIPJ3 bisa menender ulang atau mengelola sendiri **tanpa negosiasi lisensi dengan
siapa pun.** Ini argumen *value for money* yang layak dinyatakan terbuka.

---

## 8. Rencana pengujian dan penerimaan

| Lapisan | Alat | Cakupan |
|---|---|---|
| Unit | Vitest | Komponen blok, logika bahasa cadangan, format |
| Integrasi | Vitest + Payload | **Seluruh kombinasi peran × koleksi × operasi** |
| Ujung ke ujung | Playwright | Alur terbit→bangun→tayang, ganti bahasa, pencarian, unduhan |
| Aksesibilitas | axe-core | Setiap template, kedua bahasa |
| Kinerja | Lighthouse CI | Ambang NFR-01 sampai NFR-04 |

Kombinasi peran diuji **menyeluruh, bukan sampel**. Kesalahan di sini berarti konten yang belum
disetujui tayang di situs yang dilihat DFAT — kegagalan paling mahal yang mungkin terjadi pada
sistem ini.

### Enam pembuktian penerimaan

1. Seluruh uji otomatis lulus
2. Uji ujung ke ujung lulus, termasuk alur terbit sampai tayang
3. Nol pelanggaran aksesibilitas di semua template, dua bahasa
4. Seluruh ambang kinerja terpenuhi
5. **Uji peran manual:** masuk sebagai `editor`, buat publikasi dua bahasa, pastikan tombol
   terbit **ditolak**; masuk sebagai `approver`, terbitkan; pastikan tayang di kedua bahasa,
   ditemukan lewat pencarian, dan berkasnya terunduh
6. **Uji pemulihan:** ambil cadangan semalam, pulihkan ke basis data kosong, periksa keutuhan isi

Butir 5 dan 6 membuktikan kewajiban kontrak. Butir 1–4 membuktikan kodenya.

---

## 9. Rencana pemeliharaan 12 bulan

| Kegiatan | Frekuensi |
|---|---|
| Pemantauan uptime dan notifikasi | Terus-menerus |
| Cadangan basis data dan media ke luar lokasi | Harian |
| **Uji pemulihan cadangan** | Bulanan |
| Pembaruan dependensi | Mingguan, otomatis |
| Tambalan celah kritis | Dalam 48 jam sejak rilis |
| Unggah konten dari AIPJ3 | Sesuai kebutuhan, dalam jatah jam |
| Laporan kinerja | Bulanan |
| Audit mendalam kinerja dan aksesibilitas | Enam bulanan |
| Rekomendasi uji penetrasi | Tahunan |

**Verifikasi cadangan berarti memulihkan.** Kontrak menulis *backup verification*. Memastikan
berkas cadangan ada bukan verifikasi — memulihkannya ke basis data kosong dan memeriksa isinya
barulah verifikasi. Kita lakukan tiap bulan.

**Uji penetrasi bersifat rekomendasi.** TOR meminta *"penetration testing recommendation"*, bukan
pengujiannya. Kita susun rekomendasi dan lingkupnya; pelaksanaannya di pihak AIPJ3 dan tidak masuk
harga.

### Serah terima

Panduan operasional, catatan keputusan arsitektur, dan infrastruktur sebagai kode tersimpan di
repositori. Pelatihan dua jam direkam, disertai panduan admin dwibahasa.

---

## 10. Risiko dan hal yang perlu didiskusikan

| Risiko | Penanganan |
|---|---|
| Hasil Tahap 1 mengubah struktur konten | Sistem blok menyerapnya sebagai konfigurasi |
| Pembangunan ulang terlalu lambat untuk koreksi mendesak | Jalur cepat manual, dilatihkan sejak awal |
| **Penyedia lokal tidak mendukung header kustom atau API cache** | **Gerbang Tahap 1** — diperiksa sebelum pekerjaan infrastruktur; cadangannya CDN di depan server lokal |
| Perekrutan peserta uji disabilitas butuh waktu | Dijadwalkan sejak Tahap 1, dilaksanakan di Tahap 2 |
| Ketergantungan pada satu orang | Catatan keputusan dan panduan operasional sejak hari pertama |

### Empat hal yang harus dibahas dengan AIPJ3 di rapat awal

**1. GTM versus Lighthouse ≥ 90.** RFP mewajibkan Google Tag Manager *dan* skor Lighthouse minimal
90. Padahal kontainer GTM standar terbukti menurunkan skor kecepatan. Solusi kita: GTM hanya dimuat
setelah pengunjung menyetujui, dijalankan saat peramban menganggur, kontainer seminimal mungkin.
Kita berkomitmen pada ≥ 90 diukur pada kondisi yang benar-benar dialami pengunjung pertama, dengan
angka pasca-persetujuan dilaporkan terpisah. **Menyatakan ketegangan ini lebih meyakinkan daripada
menjanjikan keduanya tanpa syarat.**

**2. Definisi uptime 99,9%.** Jatah henti ±43 menit per bulan. Cara pengukuran dan definisi
"gangguan" harus disepakati tertulis. Definisi yang tidak tertulis adalah penyebab sengketa SLA
paling umum.

**3. WCAG 2.2 AA sebagian bergantung isi konten.** Pemeriksaan otomatis tidak bisa mencegah
penyunting menulis teks tautan yang tidak informatif. Kepatuhan jangka panjang adalah **tanggung
jawab bersama**, didukung panduan penyuntingan pada pelatihan.

**4. Persetujuan CMS.** RFP menyebut Contentful dan Sanity; kita mengusulkan Payload. Butuh
persetujuan formal sebagai *client-approved CMS*. Bila ditolak, cadangannya Sanity — dengan
konsekuensi biaya lisensi tahun kedua menjadi tanggungan AIPJ3.

---

## Dokumen terkait

| Berkas | Isi |
|---|---|
| `Strategi-Penawaran-AIPJ3.md` | Opsi penawaran, rekomendasi, rencana eksekusi |
| `Analisis-RFP-AIPJ3.md` | Temuan atas dokumen RFP |
| `Persyaratan-Teknis-AIPJ3.md` | 59 persyaratan RFP dan jawabannya, satu per satu |
| `../superpowers/specs/2026-08-24-aipj3-website-design.md` | Rancangan arsitektur teknis |
| `../reference/RFP-extracted-text.md` | Teks RFP 15 halaman verbatim |
