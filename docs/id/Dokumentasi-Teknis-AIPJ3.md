# Dokumentasi Teknis dan Strategi — Situs Web AIPJ3

**RFP:** RFP/Website Development/018-08-2026
**Sifat dokumen:** materi pendukung penyusunan proposal — satu dokumen untuk seluruh sisi teknis.
**Bahasa:** Indonesia. Proposal resmi wajib berbahasa Inggris; dokumen ini sumbernya.

## Isi

1. Ringkasan — kenapa pendekatan ini
2. Strategi requirement gathering
3. Strategi: di mana penawaran ini dimenangkan
4. Metodologi kerja
5. Rekomendasi struktur halaman
6. Desain sistem
7. Requirement fungsional
8. Requirement non-fungsional
9. Rencana pengujian dan penerimaan
10. Rencana pemeliharaan 12 bulan
11. Risiko dan hal yang perlu didiskusikan

---

## 1. Ringkasan — kenapa pendekatan ini

Semua keputusan teknis di dokumen ini berangkat dari dua kendala yang sama.

Yang pertama, anggaran sudah dikunci di angka 150 juta, tapi peta situs dan hierarki kontennya
justru baru akan disusun di Tahap 1 bersama pemangku kepentingan. Artinya kita berkomitmen pada
harga sebelum tahu persis apa yang dibangun. Kalau setiap hasil lokakarya berarti menulis kode
baru, margin akan habis jauh sebelum pembangunan selesai.

Karena itu yang kami bangun bukan situs, melainkan platform. Ada dua belas blok konten siap pakai.
Menambah jenis halaman berarti menyusun blok, bukan memprogram ulang. Apa pun yang keluar dari
lokakarya Tahap 1 menjadi konfigurasi — bukan pekerjaan tambahan.

Kendala kedua soal beban operasional. Kontrak menuntut ketersediaan 99,9%, tambalan keamanan
kritis dalam 48 jam, dan pemantauan penuh selama 12 bulan. Untuk tim kecil, memikul itu di atas
aplikasi yang hidup terus-menerus adalah risiko yang tidak sebanding dengan nilainya.

Jawaban kami: situs statis. Halaman disajikan sebagai berkas mati dari CDN, tanpa server publik
yang bisa jatuh atau diserang. Kalau CMS-nya mati, situsnya tetap tayang. Janji 99,9% berubah dari
komitmen aplikasi menjadi komitmen CDN, dan itu jauh lebih realistis untuk ditepati selama setahun
penuh.

Dua-duanya bukan penghematan. Keduanya keputusan rekayasa supaya kontrak ini bisa diselesaikan
dengan benar pada anggaran yang memang segitu.

---

## 2. Strategi requirement gathering

### Kenapa bagian ini ada di depan

Daftar requirement di Bagian 7 dan 8 adalah hipotesis kami, bukan temuan. Secara kontrak,
kebutuhan baru ditetapkan bersama pemangku kepentingan di Tahap 1 dan ditandatangani sebagai
Keluaran 1.

Perbedaan itu penting karena pagunya tetap. Menggali kebutuhan tanpa batas pada anggaran yang tidak
bisa naik hanya berujung satu hal. Jadi kami perlakukan tahap ini sebagai proses berbatas waktu
dengan aturan main yang jelas, bukan rangkaian rapat terbuka.

### Lima prinsip

**Datang dengan hipotesis, bukan halaman kosong.** Peta situs dan daftar requirement di dokumen ini
kami bawa ke lokakarya untuk disetujui atau ditolak. Orang jauh lebih cepat menanggapi sesuatu yang
sudah ada wujudnya daripada mengarang dari nol, dan hasilnya biasanya lebih tajam.

**Pisahkan yang mengikat dari yang diusulkan.** Kebutuhan yang datang dari RFP sifatnya kontraktual
dan tidak bisa ditawar turun. Kebutuhan yang muncul di lokakarya sifatnya tambahan, dan harus
dihitung terhadap pagu. Kalau keduanya dicampur dalam satu daftar tanpa penanda, yang membengkak
tidak akan ketahuan sampai terlambat.

**Setiap kebutuhan punya pemilik dan cara mengujinya.** "Situsnya harus mudah dipakai" bukan
kebutuhan — tidak ada cara membuktikannya. "Penyunting bisa menerbitkan berita tanpa bantuan
developer" baru kebutuhan, karena bisa dicoba.

**Berbatas waktu.** Tahap 1 cuma 30 hari kalender, dan itu sudah termasuk menyusun wireframe serta
arah visual. Penggalian kebutuhan dapat jatah dua minggu pertama, tidak lebih.

**Bekukan di akhir Tahap 1.** Begitu Keluaran 1 ditandatangani, perubahan mengikuti prosedur di
bawah. Tanpa titik beku, tidak ada tanggal peluncuran yang bisa dipertahankan.

### Siapa yang harus ditemui

| Pemangku kepentingan | Yang digali dari mereka | Prioritas |
|---|---|---|
| Strategic Communications Manager | Definisi sukses, prioritas, wewenang persetujuan | Wajib — pemilik Keluaran 1 |
| Tim Komunikasi AIPJ3 | Alur kerja penerbitan sekarang, hambatannya, ritme mingguan | Wajib — pengguna harian CMS |
| Perwakilan DFAT | Mekanisme persetujuan konten, kebutuhan akuntabilitas | Wajib — memengaruhi desain peran |
| Perwakilan lembaga hukum GOI | Kebutuhan konten resmi, format dokumen | Penting |
| Organisasi disabilitas | Kebutuhan aksesibilitas nyata; sekaligus calon peserta uji Tahap 2 | Penting — hubungi sejak minggu 1 |
| Tim IT DT Global / AIPJ3 | Domain, DNS, kendala infrastruktur, kebijakan keamanan | Wajib — bisa mengubah arsitektur |

Baris DFAT yang paling sering terlewat. RFP menyebut *"following DFAT's approval mechanism"* tanpa
pernah menjelaskan mekanismenya seperti apa. Padahal itulah yang menentukan berapa lapis
persetujuan harus dibangun ke dalam sistem peran. Kami gali eksplisit di minggu pertama, bukan
diasumsikan sendiri.

### Teknik yang dipakai

| Teknik | Untuk menggali | Peserta | Durasi |
|---|---|---|---|
| Lokakarya penemuan | Tujuan, prioritas, definisi sukses | SCM + tim komunikasi | 3 jam |
| Wawancara mendalam | Alur kerja dan hambatan sebenarnya | 3–5 orang | 45 menit/orang |
| Audit konten | Materi yang sudah ada: volume, format, kondisinya | Mandiri + tim komunikasi | 2 hari |
| Analisis pembanding | Situs program donor sejenis | Mandiri | 1 hari |
| Kartu sortir | Struktur navigasi yang masuk akal bagi pengguna | 5–8 peserta | 1 jam |
| Sesi aksesibilitas | Kebutuhan nyata penyandang disabilitas | Organisasi mitra | 2 jam |
| Peninjauan teknis | Domain, DNS, hosting, kebijakan keamanan | Tim IT | 1 jam |

Dari semuanya, audit konten yang paling sering diremehkan. Situs terlambat tayang biasanya bukan
karena kodenya belum jadi, tapi karena kontennya belum siap. Mengauditnya di minggu pertama memberi
peringatan berbulan-bulan sebelum tenggat.

### Jadwal 30 hari Tahap 1

| Minggu | Kegiatan | Hasil |
|---|---|---|
| 1 (15–21 Sep) | Rapat awal, lokakarya penemuan, audit konten, peninjauan teknis | Daftar kebutuhan awal, gerbang hosting diperiksa |
| 2 (22–28 Sep) | Wawancara, kartu sortir, analisis pembanding, sesi aksesibilitas | Masukan pengguna, struktur navigasi teruji |
| 3 (29 Sep–5 Okt) | Sintesis | Persona, peta perjalanan, peta situs, requirement final |
| 4 (6–15 Okt) | Wireframe, arah visual, tinjauan klien, revisi | Keluaran 1 ditandatangani |

Perhatikan gerbang hosting ada di minggu 1, bukan menjelang pembangunan. Kalau penyedia lokal
ternyata tidak mendukung header HTTP kustom atau API pembersihan cache, yang berubah arsitekturnya
— dan kami perlu tahu itu selagi masih ada waktu memutar haluan.

### Cara mencatat: register kebutuhan

Satu tabel saja, dipakai sebagai rujukan sepanjang proyek.

| Kolom | Isi |
|---|---|
| ID | FR-01, NFR-01, dan seterusnya |
| Deskripsi | Satu kalimat yang bisa diuji |
| Sumber | Pasal RFP, atau nama orang yang memintanya |
| Sifat | Mengikat (dari RFP) atau Diusulkan (dari lokakarya) |
| Prioritas | Harus / Sebaiknya / Boleh / Tidak sekarang |
| Kriteria diterima | Cara membuktikannya terpenuhi |
| Status | Diusulkan → Disepakati → Dibangun → Diterima |

Kuncinya di kolom prioritas: jatah "Harus" tidak boleh melebihi kapasitas anggaran. Kalau lokakarya
menghasilkan lebih banyak "Harus" daripada yang muat, percakapan itu harus terjadi di bulan
pertama — bukan di bulan keempat waktu sudah tidak bisa apa-apa.

Seluruh requirement di Bagian 7 dan 8 masuk register ini dengan status Diusulkan. Yang datang
langsung dari RFP masuk sebagai Mengikat dan tidak dinegosiasikan.

### Prosedur perubahan setelah Tahap 1

Disepakati tertulis sebagai bagian dari Keluaran 1.

| Jenis perubahan | Penanganan |
|---|---|
| Tidak menambah usaha | Langsung dikerjakan, dicatat di register |
| Menambah usaha, masih ada ruang | Ditukar dengan butir lain berprioritas sama |
| Menambah usaha, tidak ada ruang | Jadi adendum terpisah, di luar kontrak ini |

Mekanisme tukar-lingkup inilah yang menjaga pagu tanpa membuat kami terkesan menolak masukan
klien. Jawabannya bukan "tidak bisa", tapi "bisa — butir mana yang kita geser?"

### Risiko penggalian kebutuhan

| Risiko | Penanganan |
|---|---|
| Pemangku kepentingan kunci tidak hadir | Jadwalkan sejak rapat awal; tetapkan pengganti yang berwenang |
| Kebutuhan membengkak melewati kapasitas | Empat tingkat prioritas + prosedur tukar-lingkup |
| Mekanisme persetujuan DFAT tidak jelas | Digali eksplisit di minggu 1 — memengaruhi desain peran |
| Konten belum siap saat pembangunan selesai | Audit konten minggu 1 memberi peringatan dini |
| Lokakarya menghasilkan struktur berbeda dari usulan | Sistem blok membuatnya jadi konfigurasi, bukan pekerjaan ulang |

---

## 3. Strategi: di mana penawaran ini dimenangkan

| Kriteria penilaian | Bobot |
|---|---:|
| Pendekatan dan metodologi | **50%** |
| Kualifikasi dan personel kunci | 30% |
| Pengalaman organisasi | 20% |

Blok metodologi bobotnya lebih besar daripada pengalaman organisasi dan personel digabungkan. Dan
RFP sendiri membuka pintu soal pilihan teknologi: *"Provider could identify other than the list with
description of its advantages and disadvantages."*

Kebanyakan peserta akan menyalin ulang tabel teknologi RFP sebagai daftar centang. Itu cuma bernilai
"memenuhi syarat". Lima hal berikut yang membuat penawaran kami berbeda.

**Menyelesaikan kontradiksi hosting secara terbuka.** RFP minta penyedia lokal di bagian
pemeliharaan, tapi menyebut AWS, Azure, Vercel, dan Cloudflare di tabel penilaian. Dua-duanya tidak
bisa benar sekaligus. Kami nyatakan penafsiran kami, bukan mendiamkannya — dan itu menunjukkan
dokumennya benar-benar dibaca sampai habis.

**Menghitung biaya CMS dengan jujur.** Lisensi CMS berbayar adalah biaya berulang yang jalan terus
setelah kontrak berakhir, dan yang menanggung AIPJ3, bukan kami. Karena itu kami sajikan
perbandingan biaya 12 dan 36 bulan, bukan cuma harga proyeknya.

**Menganggarkan pengujian nyata bersama penyandang disabilitas.** Ruang lingkupnya menulis
*"accessibility audit including with people with disability"* — itu pengujian dengan orangnya, bukan
pemindaian otomatis. Dan ini tersambung langsung ke EOPO 3, soal akses keadilan setara bagi
perempuan, anak, dan penyandang disabilitas. Panel yang berasal dari program ini akan mengenali
kerangka hasil mereka sendiri di proposal kami. Pembeda paling kuat yang tersedia, dan hampir pasti
dilewatkan pesaing.

**Membuka dengan pengalaman penyunting, bukan nama kerangka kerja.** Yang jadi masalah klien
sehari-hari bukan React atau Vue, tapi apakah staf komunikasi bisa menerbitkan konten mingguan
tanpa menelepon developer.

**Menyerahkan rencana kerja yang tanggalnya konsisten.** RFP memuat beberapa tanggal yang tidak
cocok satu sama lain. Kami tidak mengoreksi klien — cukup menyerahkan jadwal yang masuk akal,
dengan satu baris catatan asumsi.

---

## 4. Metodologi kerja

Empat tahap kontraknya sebenarnya sudah sejalan dengan alur design thinking. Kami pakai apa adanya,
tidak perlu memaksakan kerangka lain di atasnya.

| Tahap kontrak | Fase design thinking | Pertanyaan yang dijawab |
|---|---|---|
| 1. Konsep Desain | Empathize + Define | Siapa penggunanya, apa yang mereka cari, bagaimana isinya ditata |
| 2. Pengembangan | Ideate + Prototype | Seperti apa wujudnya, dan apakah benar-benar bekerja |
| 3. Peluncuran | Test | Apakah bertahan di dunia nyata |
| 4. Pemeliharaan | Iterate | Apa yang perlu diperbaiki setelah dipakai |

### Tahap 1 — Konsep Desain (15 Sep – 15 Okt 2026)

Kami bawa tiga persona ke lokakarya sebagai bahan diskusi:

| Persona | Yang dicari | Sinyal kepercayaan yang dibutuhkan |
|---|---|---|
| Pejabat lembaga hukum Indonesia | Dokumen kebijakan, bukti kerja sama, rujukan resmi | Kejelasan kelembagaan, bahasa Indonesia, bisa diunduh |
| Pemangku kepentingan DFAT dan Australia | Kemajuan program, akuntabilitas, hasil terukur | Data, pelaporan berkala, penelusuran ke EOPO |
| Masyarakat sipil dan publik Indonesia | Cerita dampak, cara terlibat, akses informasi | Bahasa sederhana, aksesibel, mudah dibagikan |

Ketiganya punya tingkat literasi dan kebutuhan aksesibilitas yang berbeda. Tapi itu satu masalah
desain, bukan tiga audiens yang berebut ruang di beranda.

Keluaran tahap ini: daftar kebutuhan tertulis, tiga persona, peta perjalanan, peta situs, wireframe
empat template, dan arah visual — semuanya ditandatangani sebagai Keluaran 1.

Satu lagi yang wajib tuntas di tahap ini, meski bukan permintaan klien: memastikan penyedia hosting
mendukung header HTTP kustom dan API pembersihan cache. Kalau tidak, arsitekturnya yang berubah.

### Tahap 2 — Pengembangan (16 Okt 2026 – 22 Jan 2027)

Urutan kerjanya:

1. Infrastruktur dan pipeline CI
2. Design system dan dua belas blok konten
3. Model konten dan kontrol akses
4. Template halaman
5. Pencarian dan analitik
6. Pengerasan keamanan dan audit

Kontrol akses sengaja dikerjakan lebih awal, karena bentuk hampir semua pekerjaan sesudahnya
bergantung padanya.

### Tahap 3 — Peluncuran (23–29 Jan 2027)

Gladi bersih di infrastruktur setara produksi, TTL DNS diturunkan sebelum pemindahan, konfigurasi
SSL, penerapan, lalu pemantauan pengguna nyata. Versi lama tetap tayang sampai versi baru
terverifikasi — jadi tidak ada jendela waktu di mana situsnya kosong.

### Tahap 4 — Pemeliharaan (29 Jan 2027 – 28 Jan 2028)

Rinciannya di Bagian 10.

---
## 5. Rekomendasi struktur halaman

> **[PERLU DIDISKUSIKAN]**
> **Dibahas dengan:** AIPJ3, pada lokakarya Tahap 1
> **Sifatnya:** usulan untuk ditanggapi, bukan keputusan. Peta situs final adalah Keluaran 1 dan
> ditandatangani klien.
> **Kenapa tetap diusulkan sekarang:** lokakarya berjalan jauh lebih cepat kalau ada bahan konkret
> untuk disetujui atau dibantah, dibanding memulai dari papan kosong.

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

Semuanya tersedia dalam dua bahasa, lewat `/en/...` dan `/id/...`.

### Kenapa EOPO jadi tulang punggung

Setiap publikasi, berita, dan kegiatan ditandai ke satu atau lebih EOPO. Akibatnya seluruh situs
bisa ditelusuri berdasarkan hasil program — persis cara DFAT dan Pemerintah Indonesia menalar
program ini sehari-hari.

Ini yang mengubah "mendokumentasikan kemajuan, pembelajaran, dan dampak" dari blog kronologis
menjadi sesuatu yang punya struktur sungguhan.

### Rincian halaman utama

| Halaman | Tujuan | Audiens utama | Isi kunci |
|---|---|---|---|
| Beranda | Menjelaskan apa itu AIPJ3 dalam 10 detik, lalu mengarahkan | Ketiganya | Pernyataan program, empat pintu EOPO, sorotan terbaru, publikasi terbaru |
| Hub EOPO | Menjawab "apa hasilnya di bidang ini" | DFAT, lembaga hukum | Narasi hasil, publikasi terkait, berita terkait, mitra terlibat |
| Indeks publikasi | Menemukan dan mengunduh dokumen | Lembaga hukum, DFAT | Filter EOPO, jenis, tahun, bahasa; hasil dengan sampul dan ringkasan |
| Detail publikasi | Memberi konteks sebelum mengunduh | Semua | Abstrak, metadata, tombol unduh, ukuran berkas, publikasi terkait |
| Indeks berita | Menunjukkan program ini hidup | Publik, media | Daftar kronologis, filter EOPO |
| Detail berita | Menyampaikan cerita dampak | Publik | Isi kaya, kutipan, gambar ber-alt text, tombol berbagi |
| Mitra | Menunjukkan legitimasi dan jejaring | Semua | Logo dan profil singkat, dikelompokkan per kategori |
| Aksesibilitas | Menyatakan tingkat kepatuhan dan jalur pengaduan | Penyandang disabilitas | Status WCAG 2.2 AA, keterbatasan yang diketahui, kontak umpan balik |

Soal halaman aksesibilitas — ini praktik baik WCAG dan lazim diharapkan dari lembaga publik, tapi
hampir selalu dilupakan peserta tender. Mencantumkannya, lengkap dengan keterbatasan yang diakui
jujur dan jalur pengaduan, memperkuat posisi kami di EOPO 3.

### Template yang perlu dibangun

Tiga belas template, bukan puluhan halaman:

1. Beranda · 2. Halaman statis · 3. Hub EOPO · 4. Indeks publikasi · 5. Detail publikasi ·
6. Indeks berita · 7. Detail berita · 8. Indeks agenda · 9. Detail agenda · 10. Mitra ·
11. Kontak · 12. Hasil pencarian · 13. Halaman galat 404/500

---

## 6. Desain sistem

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

Yang penting dari pemisahan ini: kalau satu tumbang, yang lain tetap jalan. CMS mati, situs tetap
tayang. Pembangunan gagal, versi sebelumnya tetap tayang. Server admin diserang, situs publik tidak
terpengaruh — karena isinya cuma berkas mati.

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

Kecepatan segitu memadai, karena yang diminta kontrak adalah pembaruan mingguan. Untuk koreksi
mendesak tetap ada jalur cepat: pemicu manual di pipeline yang sama, terdokumentasi dan dilatihkan
sejak pelatihan.

### Pratinjau draf

Penyetuju perlu melihat draf sebelum menerbitkan. Kami pakai satu basis kode dengan dua mode,
dipilih lewat variabel `BUILD_TARGET` — mode statis untuk produksi, mode server untuk pratinjau.
Pratinjaunya jalan terkunci di server admin. Tidak perlu aplikasi ketiga.

### Model konten

Koleksi: `pages`, `news`, `publications`, `events`, `partners`, `people`, `eopos`, `media`
Global: `navigation`, `siteSettings`, `footer`, `homepage`

Dua belas blok: `richText`, `mediaWithCaption`, `quote`, `statistic`, `accordion`, `cardGrid`,
`callToAction`, `embed`, `publicationList`, `newsList`, `partnerLogos`, `timeline`

### Dwibahasa

Inggris dan Indonesia disimpan sebagai kolom terpisah di setiap ruas yang bisa diterjemahkan —
bukan plugin terjemahan yang ditempel belakangan. Berkas publikasinya juga per bahasa, jadi laporan
yang cuma terbit dalam bahasa Indonesia tetap terwakili dengan wajar tanpa jadi kasus khusus.

Kalau terjemahannya belum ada, kami tampilkan versi Inggris disertai keterangan bahwa versi
Indonesianya belum tersedia, dan bagian itu ditandai `lang="en"`. Yang tidak boleh dilakukan adalah
mencampur dua bahasa dalam satu halaman tanpa penanda — pembaca jadi bingung, dan pembaca layar
melafalkannya dengan aksen yang salah.

### Peran dan alur persetujuan

| Peran | Kewenangan |
|---|---|
| `contributor` | Membuat dan menyunting draf saja |
| `editor` | Menyunting dan mengajukan untuk persetujuan — tim komunikasi |
| `approver` | Menerbitkan — Strategic Communications Manager |
| `admin` | Administrasi teknis dan pengelolaan pengguna |

Status dokumen bergerak dari draf → ditinjau → disetujui → terbit, dengan riwayat versi sebagai
jejak audit.

Tombol terbit dikunci pada peran `approver`. Dengan begitu mekanisme persetujuan DFAT jadi mekanis,
bukan sekadar kesepakatan — tidak bisa dilewati siapa pun yang sedang buru-buru.

---

## 7. Requirement fungsional

Apa yang harus bisa dilakukan sistem. Semuanya ditulis supaya bisa diuji.

### Situs publik

| ID | Requirement | Kriteria diterima |
|---|---|---|
| FR-01 | Setiap halaman tersedia dalam Inggris dan Indonesia | Pemilih bahasa pindah ke halaman yang sama, bukan balik ke beranda |
| FR-02 | Pencarian seluruh situs | Kata kunci menemukan isi halaman, berita, dan publikasi di kedua bahasa |
| FR-03 | Filter publikasi | Bisa disaring per EOPO, jenis, tahun, bahasa; filter bisa digabung |
| FR-04 | Unduh berkas publikasi | Berkas terunduh; ukuran dan format tampil sebelum diklik |
| FR-05 | Penandaan EOPO pada seluruh konten | Setiap publikasi, berita, dan kegiatan tertaut ke minimal satu EOPO |
| FR-06 | Konten terkait | Halaman detail menampilkan item lain dengan EOPO sama |
| FR-07 | Formulir kontak | Kiriman masuk dan pengirim dapat konfirmasi; ada perlindungan spam |
| FR-08 | Berbagi ke media sosial | Tautan berbagi menghasilkan pratinjau benar di tiap bahasa |
| FR-09 | Banner persetujuan cookie | Pengunjung bisa menerima atau menolak per kategori; pilihan tersimpan |
| FR-10 | Halaman galat dwibahasa | 404 dan 500 tampil dalam bahasa yang sedang dipakai, dengan jalan kembali |
| FR-11 | Peta situs XML otomatis | Terbentuk per bahasa dan mutakhir tiap kali situs dibangun |

### Sisi pengelolaan konten

| ID | Requirement | Kriteria diterima |
|---|---|---|
| FR-12 | Kelola seluruh jenis konten | Penyunting bisa membuat, menyunting, menghapus tanpa bantuan developer |
| FR-13 | Alur persetujuan | Draf tidak bisa terbit tanpa persetujuan peran `approver` |
| FR-14 | Kontrol akses empat peran | Tiap peran hanya bisa melakukan yang jadi haknya — diuji menyeluruh |
| FR-15 | Pratinjau draf | Penyetuju melihat wujud akhir sebelum menerbitkan |
| FR-16 | Riwayat versi | Tiap perubahan tercatat pelaku dan waktunya; bisa dikembalikan |
| FR-17 | Unggah media | Gambar wajib punya alt text di dua bahasa; tanpa itu tidak bisa disimpan |
| FR-18 | Susun halaman dari blok | Halaman baru dibuat dengan menyusun blok, tanpa menulis kode |
| FR-19 | Kelola navigasi | Menu diubah dari CMS, tidak perlu penerapan ulang |
| FR-20 | Penerbitan terjadwal | Konten bisa dijadwalkan terbit pada tanggal tertentu |

---

## 8. Requirement non-fungsional

Seberapa baik sistemnya harus bekerja. Bagian inilah yang biasanya jadi sumber sengketa kalau
angkanya tidak pernah dituliskan.

| ID | Aspek | Target | Cara diukur |
|---|---|---|---|
| NFR-01 | Kecepatan muat | LCP < 2,5 detik | Lighthouse CI tiap build; data pengguna nyata setelah tayang |
| NFR-02 | Responsivitas interaksi | INP < 200 ms | Sama |
| NFR-03 | Kestabilan tata letak | CLS < 0,1 | Sama |
| NFR-04 | Skor Lighthouse | ≥ 90 seluruh kategori | Ambang wajib di CI — build gagal kalau di bawahnya |
| NFR-05 | Aksesibilitas | WCAG 2.2 Level AA | Pemeriksaan otomatis tiap build, plus sesi uji bersama penyandang disabilitas |
| NFR-06 | Ketersediaan | ≥ 99,9% per bulan | Pemantauan dari luar; setara jatah henti ±43 menit/bulan |
| NFR-07 | Waktu konten tayang | ≤ 6 menit sejak diterbitkan | Diuji saat UAT |
| NFR-08 | Tambalan keamanan kritis | ≤ 48 jam sejak rilis | Dicatat dan dilaporkan bulanan |
| NFR-09 | Cadangan | Harian, luar lokasi, penyedia berbeda | Uji pemulihan tiap bulan ke basis data kosong |
| NFR-10 | Keamanan transport | TLS 1.3, HSTS, CSP, WAF | Pemindaian header dan konfigurasi tiap rilis |
| NFR-11 | Kerentanan | Tidak ada celah kritis terbuka | Pemindaian dependensi otomatis; tinjauan OWASP tiap rilis |
| NFR-12 | Kedaulatan data | Data berada di Indonesia | Konfigurasi infrastruktur, diperiksa di Tahap 1 |
| NFR-13 | Dukungan peramban | Chrome, Firefox, Safari, Edge — dua versi terakhir | Pengujian otomatis lintas peramban |
| NFR-14 | Rentang layar | 320 px hingga 2560 px | Pengujian pada tiga titik henti |
| NFR-15 | Privasi | Tidak ada pelacakan sebelum persetujuan | Diperiksa manual saat UAT |
| NFR-16 | Ketahanan lonjakan trafik | Tidak terpengaruh | Berkas statis di CDN — tidak ada server yang bisa jenuh |
| NFR-17 | Kebebasan berpindah | Tanpa kunci vendor | Seluruh komponen berlisensi MIT atau standar terbuka |
| NFR-18 | Kemudahan pemeliharaan | Bisa dilanjutkan pihak lain | Panduan operasional, catatan keputusan, infrastruktur sebagai kode |

Soal NFR-17 — Payload berlisensi MIT, basis datanya PostgreSQL, penyimpanannya standar. Waktu
kontrak berakhir, AIPJ3 bisa menender ulang atau mengelola sendiri tanpa perlu bernegosiasi lisensi
dengan siapa pun. Ini argumen *value for money* yang layak dinyatakan terbuka di proposal.

---

## 9. Rencana pengujian dan penerimaan

| Lapisan | Alat | Cakupan |
|---|---|---|
| Unit | Vitest | Komponen blok, logika bahasa cadangan, format |
| Integrasi | Vitest + Payload | Seluruh kombinasi peran × koleksi × operasi |
| Ujung ke ujung | Playwright | Alur terbit→bangun→tayang, ganti bahasa, pencarian, unduhan |
| Aksesibilitas | axe-core | Setiap template, kedua bahasa |
| Kinerja | Lighthouse CI | Ambang NFR-01 sampai NFR-04 |

Kombinasi perannya diuji menyeluruh, bukan disampel. Kalau ada yang lolos di sini, artinya konten
yang belum disetujui bisa tayang di situs yang dilihat DFAT — dan itu kegagalan paling mahal yang
mungkin terjadi pada sistem ini.

### Enam pembuktian penerimaan

1. Seluruh uji otomatis lulus
2. Uji ujung ke ujung lulus, termasuk alur terbit sampai tayang
3. Nol pelanggaran aksesibilitas di semua template, dua bahasa
4. Seluruh ambang kinerja terpenuhi
5. Uji peran manual — masuk sebagai `editor`, buat publikasi dua bahasa, pastikan tombol terbit
   ditolak; masuk sebagai `approver`, terbitkan; pastikan tayang di kedua bahasa, ketemu lewat
   pencarian, dan berkasnya benar-benar terunduh
6. Uji pemulihan — ambil cadangan semalam, pulihkan ke basis data kosong, periksa keutuhan isinya

Butir 5 dan 6 yang membuktikan kewajiban kontraknya. Butir 1 sampai 4 membuktikan kodenya.

---

## 10. Rencana pemeliharaan 12 bulan

| Kegiatan | Frekuensi |
|---|---|
| Pemantauan uptime dan notifikasi | Terus-menerus |
| Cadangan basis data dan media ke luar lokasi | Harian |
| Uji pemulihan cadangan | Bulanan |
| Pembaruan dependensi | Mingguan, otomatis |
| Tambalan celah kritis | Dalam 48 jam sejak rilis |
| Unggah konten dari AIPJ3 | Sesuai kebutuhan, dalam jatah jam |
| Laporan kinerja | Bulanan |
| Audit mendalam kinerja dan aksesibilitas | Enam bulanan |
| Rekomendasi uji penetrasi | Tahunan |

Satu hal yang perlu ditegaskan: verifikasi cadangan itu artinya memulihkan. Kontraknya menulis
*backup verification*. Memastikan berkas cadangannya ada bukan verifikasi — memulihkannya ke basis
data kosong dan memeriksa isinya barulah verifikasi. Kami lakukan tiap bulan.

Soal uji penetrasi, TOR-nya meminta *"penetration testing recommendation"* — rekomendasinya, bukan
pengujiannya. Kami susun rekomendasi beserta lingkupnya; pelaksanaan ujinya ada di pihak AIPJ3 dan
tidak masuk harga kami.

### Serah terima

Panduan operasional, catatan keputusan arsitektur, dan infrastruktur sebagai kode semuanya tersimpan
di repositori. Pelatihan dua jamnya direkam, disertai panduan admin dwibahasa.

---

## 11. Risiko dan hal yang perlu didiskusikan

| Risiko | Penanganan |
|---|---|
| Hasil Tahap 1 mengubah struktur konten | Sistem blok menyerapnya sebagai konfigurasi |
| Pembangunan ulang terlalu lambat untuk koreksi mendesak | Jalur cepat manual, dilatihkan sejak awal |
| Penyedia lokal tidak mendukung header kustom atau API cache | Gerbang Tahap 1 — diperiksa sebelum pekerjaan infrastruktur; cadangannya CDN di depan server lokal |
| Perekrutan peserta uji disabilitas butuh waktu | Dijadwalkan sejak Tahap 1, dilaksanakan di Tahap 2 |
| Ketergantungan pada satu orang | Catatan keputusan dan panduan operasional sejak hari pertama |

### Empat hal yang harus dibahas dengan AIPJ3 di rapat awal

**GTM versus Lighthouse ≥ 90.** RFP mewajibkan Google Tag Manager sekaligus skor Lighthouse minimal
90. Masalahnya, kontainer GTM standar memang terbukti menurunkan skor kecepatan. Jalan keluar kami:
GTM baru dimuat setelah pengunjung menyetujui, dijalankan waktu peramban menganggur, kontainernya
dibuat seminimal mungkin. Kami berkomitmen pada ≥ 90 yang diukur pada kondisi yang benar-benar
dialami pengunjung pertama, dan angka pasca-persetujuan dilaporkan terpisah. Menyatakan ketegangan
ini lebih meyakinkan daripada menjanjikan dua-duanya tanpa syarat lalu gagal di bulan ketiga.

**Definisi uptime 99,9%.** Angka itu memberi jatah henti sekitar 43 menit sebulan. Cara mengukurnya
dan apa yang dihitung sebagai gangguan harus disepakati tertulis. Definisi yang tidak pernah ditulis
adalah penyebab sengketa SLA yang paling sering terjadi.

**WCAG 2.2 AA sebagian bergantung isi konten.** Pemeriksaan otomatis tidak bisa mencegah penyunting
menulis teks tautan yang tidak informatif atau urutan judul yang kacau. Jadi kepatuhan jangka
panjang itu tanggung jawab bersama, dan sebaiknya dijelaskan begitu sejak awal — didukung panduan
penyuntingan di pelatihan.

**Persetujuan CMS.** RFP menyebut Contentful dan Sanity; kami mengusulkan Payload. Ini butuh
persetujuan formal sebagai *client-approved CMS*. Kalau ditolak, cadangannya Sanity — dengan
konsekuensi biaya lisensi tahun kedua dan seterusnya jadi tanggungan AIPJ3.

---

## Dokumen terkait

| Berkas | Isi |
|---|---|
| `Strategi-Penawaran-AIPJ3.md` | Opsi penawaran, rekomendasi, rencana eksekusi |
| `Analisis-RFP-AIPJ3.md` | Temuan atas dokumen RFP |
| `Persyaratan-Teknis-AIPJ3.md` | 59 persyaratan RFP dan jawabannya, satu per satu |
| `../superpowers/specs/2026-08-24-aipj3-website-design.md` | Rancangan arsitektur teknis |
| `../reference/RFP-extracted-text.md` | Teks RFP 15 halaman verbatim |
