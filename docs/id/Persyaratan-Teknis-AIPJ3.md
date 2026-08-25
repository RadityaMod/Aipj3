# Persyaratan Teknis AIPJ3 — Daftar Lengkap dan Jawaban Kita

**RFP:** RFP/Website Development/018-08-2026
**Isi dokumen:** seluruh persyaratan teknis dalam RFP, masing-masing dengan jawaban kita.

Dokumen pendamping: rancangan arsitektur di
`../superpowers/specs/2026-08-24-aipj3-website-design.md`, posisi komersial di
`Strategi-Penawaran-AIPJ3.md`.

---

## Ringkasan

**59 persyaratan teknis. Semuanya bisa kita penuhi.**

| Status | Jumlah | Artinya |
|---|---:|---|
| **Sesuai** | 43 | Kita penuhi persis seperti diminta |
| **Lebih** | 10 | Kita berikan melebihi yang diminta |
| **Alternatif** | 5 | Kita usulkan cara lain, dengan alasan |
| **Asumsi** | 1 | Perlu dikonfirmasi di rapat awal |

**Sepuluh dari dua belas teknologi yang disyaratkan cocok persis** dengan yang kita pakai.
Hanya CMS dan hosting yang berbeda, dan RFP sendiri membuka ruang untuk itu.

**Yang perlu diperhatikan:** kendala penawaran ini bukan di sisi teknis. Kendalanya ada di
Bagian 9 — **lima personel kunci belum ada CV-nya sama sekali**, padahal bobotnya 30%.

---

## Cara membaca

| Label | Arti |
|---|---|
| **Sesuai** | Memenuhi persis seperti diminta |
| **Lebih** | Melebihi yang diminta |
| **Alternatif** | Kita usulkan cara lain — alasannya di Bagian 10 |
| **Asumsi** | Bergantung pada hal yang perlu dikonfirmasi — daftarnya di Bagian 11 |

Setiap butir bertanda **Alternatif** dan **Asumsi** juga membawa label
**[PERLU DIDISKUSIKAN]**, lengkap dengan dengan siapa dibahas, kapan, dan apa rencana
cadangannya bila tidak disetujui. Rekapnya ada di Bagian 13.

---

## 1. Tujuan situs (8 butir)

| Yang diminta | Jawaban kita | Status |
|---|---|---|
| Situs modern, responsif, dwibahasa | Next.js 15 + TypeScript. Bahasa Inggris dan Indonesia sebagai dua kolom terpisah di database, bukan plugin terjemahan | Sesuai |
| Patuh penuh WCAG 2.2 Level AA | Diperiksa otomatis setiap kali kode dibangun. Build gagal kalau ada pelanggaran | Lebih |
| Skor Core Web Vitals bagus | Halaman disajikan sebagai berkas statis dari CDN. Ambang batas kecepatan diperiksa otomatis | Lebih |
| Konten bisa diperbarui mingguan | Staf komunikasi menerbitkan sendiri lewat CMS. Situs terbarui dalam 3–6 menit | Sesuai |
| Analitik, manajemen consent, pelacakan patuh privasi | GA4 lewat GTM dengan Consent Mode v2. Tidak ada tag berjalan sebelum pengunjung menyetujui | Sesuai |
| Hosting aman dan terukur, dengan prosedur terdokumentasi | Infrastruktur di Indonesia, dilindungi CDN dan WAF. Panduan operasional tersimpan di repositori | Sesuai |
| Unggah konten berkala | Layanan unggah rutin, masuk dalam jatah jam bulanan | Sesuai |
| Semua tahap selesai sesuai waktu dan anggaran | Rencana per tahap, terhubung ke tujuh keluaran, di dalam pagu 150 juta | Sesuai |

---

## 2. Tahap 1 — Konsep Desain (15 Sep – 15 Okt 2026, 6 butir)

| Yang diminta | Jawaban kita | Status |
|---|---|---|
| Rapat dengan klien dan pemangku kepentingan | Dua lokakarya terfasilitasi, hasilnya daftar kebutuhan tertulis yang ditandatangani | Sesuai |
| Riset UX: persona dan peta perjalanan pengguna | Tiga persona: pejabat lembaga hukum, pemangku kepentingan DFAT, dan masyarakat sipil Indonesia | Sesuai |
| Arsitektur informasi: peta situs, hierarki konten, navigasi | Peta situs dengan taksonomi EOPO sebagai tulang punggung navigasi | Sesuai |
| Wireframe kasar untuk template halaman utama | Empat template: beranda, halaman dalam, kontak, halaman kampanye | Sesuai |
| Arah merek dan visual: tipografi, warna, bahasa desain | Dibuat sebagai design token. Dokumentasi dan kodenya jadi satu berkas yang sama | Lebih |
| Persetujuan formal sebelum masuk pengembangan | Keluaran 1, disetujui Strategic Communications Manager | Sesuai |

**Catatan.** Di tahap ini ada satu pemeriksaan teknis milik kita sendiri: memastikan penyedia
hosting mendukung header HTTP kustom dan API pembersihan cache. Ini harus tuntas sebelum
pekerjaan infrastruktur dimulai. Lihat Asumsi A3.

---

## 3. Tahap 2 — Pengembangan (16 Okt 2026 – 22 Jan 2027, 21 butir)

### 3a. Desain UI/UX

| Yang diminta | Jawaban kita | Status |
|---|---|---|
| Mockup detail di Figma untuk desktop, tablet, ponsel | Figma, tiga ukuran layar, memakai design token dari Tahap 1 | Sesuai |
| Prototipe interaktif untuk ditinjau pemangku kepentingan | Prototipe Figma, dengan dua putaran umpan balik terjadwal | Sesuai |

### 3b. Pengembangan front-end

| Yang diminta | Jawaban kita | Status |
|---|---|---|
| HTML5 semantik dengan ARIA landmark | Struktur landmark ditetapkan per template dan diperiksa otomatis | Sesuai |
| CSS3 dengan design token dan Tailwind CSS 4 | Tailwind 4, token sebagai CSS custom properties | Sesuai |
| Kerangka kerja: React 19 / Next.js 15 atau Vue 3 / Nuxt 3 | Next.js 15 + React 19 + TypeScript — dari daftar yang disebut RFP | Sesuai |
| Responsif, diuji di Chrome, Firefox, Safari, Edge | Pengujian otomatis di keempat peramban | Sesuai |
| Prinsip progressive enhancement | Konten dan navigasi tetap berfungsi tanpa JavaScript | Sesuai |

### 3c. Integrasi CMS

| Yang diminta | Jawaban kita | Status |
|---|---|---|
| CMS yang disetujui klien | Payload v3, dipasang sendiri. Lihat Alternatif 2 | Alternatif |
| Template halaman, komponen blok, model konten terstruktur | Dua belas blok siap pakai. Menambah jenis halaman cukup menyusun blok, tanpa menulis kode baru | Lebih |
| Kontrol akses berbasis peran (RBAC) | Empat peran, ditambah alur draf → tinjau → setujui → terbit yang menjalankan mekanisme persetujuan DFAT | Lebih |

### 3d. Back-end dan integrasi

| Yang diminta | Jawaban kita | Status |
|---|---|---|
| Usulkan pengembangan API bila diperlukan | Data diambil saat pembangunan situs, bukan lewat API publik. Endpoint yang tidak dibuat tidak bisa diserang | Alternatif |
| Kinerja dan SEO optimal | Penyajian statis, peta situs per bahasa, tag `hreflang`, data terstruktur | Sesuai |

### 3e. Keamanan

| Yang diminta | Jawaban kita | Status |
|---|---|---|
| Pemaksaan HTTPS | TLS 1.3 di CDN, HSTS, pengalihan otomatis dari HTTP | Sesuai |
| Header keamanan HTTP | CSP, HSTS, dan lainnya dipasang di CDN — hosting statis tidak bisa memasangnya dari kode aplikasi | Sesuai |
| Mitigasi OWASP Top 10 | Ditinjau tiap rilis. Situs publik berupa berkas mati, jadi hampir tidak ada permukaan serangan | Sesuai |
| Konfigurasi lain sesuai kebutuhan | Aturan WAF, pembatasan laju akses admin, pemindaian dependensi otomatis | Sesuai |

### 3f. Pengujian dan jaminan mutu

| Yang diminta | Jawaban kita | Status |
|---|---|---|
| Uji lintas peramban dan perangkat | Otomatis di tiga mesin peramban, plus profil iOS dan Android | Sesuai |
| Uji otomatis, manual, dan integrasi | Termasuk pengujian menyeluruh atas seluruh kombinasi peran × koleksi × operasi | Lebih |
| Audit aksesibilitas **termasuk bersama penyandang disabilitas** | Pemeriksaan otomatis **ditambah** sesi pengujian berbayar bersama penyandang disabilitas melalui organisasi mitra | Lebih |
| Audit kinerja Lighthouse dan WebPageTest, target ≥ 90 | Ambang batas diperiksa tiap build. Lihat Catatan 1 soal ketegangan dengan GTM | Sesuai |
| UAT bersama perwakilan klien | Skenario uji disusun dari daftar kebutuhan Tahap 1 | Sesuai |

---

## 4. Tahap 3 — Peluncuran (23–29 Jan 2027, 5 butir)

| Yang diminta | Jawaban kita | Status |
|---|---|---|
| Uji coba pra-peluncuran | Gladi bersih penuh di infrastruktur setara produksi | Sesuai |
| Migrasi DNS, konfigurasi SSL/TLS, koordinasi transisi | Panduan langkah demi langkah, termasuk cara membatalkan bila gagal | Sesuai |
| Penerapan ke produksi | Versi lama tetap tayang sampai versi baru terverifikasi | Lebih |
| Pengujian pascapeluncuran, pemantauan pengguna nyata | Pemantauan kecepatan dari pengguna asli dan pelacakan galat dengan notifikasi | Sesuai |
| Laporan dasar GA4 dan Search Console dalam 5 hari kerja | Keduanya diverifikasi sebelum peluncuran, jadi hitungan 5 hari dipakai untuk laporan, bukan untuk pemasangan | Sesuai |

---

## 5. Tahap 4 — Pemeliharaan (29 Jan 2027 – 28 Jan 2028, 7 butir)

| Yang diminta | Jawaban kita | Status |
|---|---|---|
| Pembaruan CMS; tambalan keamanan kritis dalam 48 jam | Pembaruan dependensi otomatis mingguan, dengan jalur khusus 48 jam untuk celah kritis | Sesuai |
| Verifikasi cadangan bulanan dan cadangan luar lokasi | Cadangan harian ke penyedia berbeda, plus **uji pemulihan tiap bulan**. Verifikasi berarti benar-benar memulihkan, bukan sekadar memastikan berkasnya ada | Lebih |
| Pemantauan uptime, SLA ≥ 99,9% | Pemantauan dari luar dengan notifikasi. Karena situs statis, ini komitmen CDN, bukan aplikasi. Lihat Catatan 2 | Sesuai |
| Laporan kinerja bulanan dan enam bulanan | Bulanan: uptime, kecepatan, trafik, konten terbit, insiden. Enam bulanan: audit lebih dalam | Sesuai |
| Unggah konten dan perbaikan bug dalam jatah jam bulanan | AIPJ3 mengirim materi, kami unggah, penyetuju menerbitkan. Jam kerja dicatat dan dilaporkan | Sesuai |
| Dokumen protokol keamanan, audit tahunan, rekomendasi uji penetrasi | Protokol dan audit kami kerjakan. **Uji penetrasinya sendiri bersifat rekomendasi** — lihat Catatan 4 | Asumsi |
| Penyedia hosting lokal | Infrastruktur di Indonesia. Lihat Alternatif 3 | Alternatif |

---

## 6. Tujuh keluaran dan syarat penerimaannya

| # | Keluaran | Syarat diterima | Tenggat |
|---|---|---|---|
| 1 | Konsep Desain | Disetujui Strategic Communications Manager | 15 Okt 2026 |
| 2 | Mockup Desain UI | Persetujuan tertulis | 30 Nov 2026 |
| 3 | Situs Web Jadi | Hasil UAT | 22 Jan 2027 *(RFP tertulis 2026 — lihat Asumsi A4)* |
| 4 | Pelatihan CMS dan Admin | Dokumentasi kehadiran | 22 Feb 2027 |
| 5 | Audit Aksesibilitas dan Kinerja | Laporan audit diserahkan | 1 Mar 2027 |
| 6 | Laporan Pascapeluncuran | Laporan diterima tertulis | 1 Mar 2027 |
| 7 | Perjanjian Pemeliharaan | Protokol keamanan, laporan kinerja, dukungan konten, hosting | 29 Jan 2027 – 28 Jan 2028 |

---

## 7. Teknologi yang disyaratkan (bobot 50%)

| Lapisan | Diminta RFP | Kita pakai | Status |
|---|---|---|---|
| Front-End | HTML5, CSS3, ES2024, TypeScript | Sama persis | Sesuai |
| Kerangka kerja | React 19 / Next.js 15 atau Vue 3 / Nuxt 3 | Next.js 15 + React 19 | Sesuai |
| Penataan gaya | Tailwind CSS 4, CSS custom properties | Sama persis | Sesuai |
| CMS | CMS headless (Contentful, Sanity) | **Payload v3** — Alternatif 2 | Alternatif |
| Back-End | Node.js 22 LTS, REST atau GraphQL | Node 22 LTS, keduanya tersedia | Sesuai |
| Basis data | PostgreSQL / MySQL | PostgreSQL | Sesuai |
| Hosting | AWS / Azure / Vercel / Cloudflare | **Infrastruktur Indonesia + CDN** — Alternatif 3 | Alternatif |
| Kendali versi | Git, pipeline CI/CD | GitHub + GitHub Actions | Sesuai |
| Keamanan | TLS 1.3, CSP, WAF, OWASP Top 10 | Sama persis, di sisi CDN | Sesuai |
| Aksesibilitas | WCAG 2.2 AA, ARIA landmark | Sama, tapi diperiksa otomatis tiap build | Lebih |
| Analitik | GA4 + Consent Mode v2, GTM | Sama persis | Sesuai |
| Target kinerja | LCP < 2,5s, INP < 200ms, CLS < 0,1 | Sama, tapi jadi ambang batas wajib di CI | Lebih |

---

## 8. Personel kunci yang disyaratkan (bobot 30%)

| Peran | Pengalaman minimum | Keahlian yang diminta |
|---|---|---|
| Manajer Proyek | 8 tahun | Memimpin proyek situs web, diutamakan sektor pembangunan atau publik |
| Front-end developer | 5 tahun | HTML, CSS, JavaScript, React/Vue, integrasi API, optimasi kinerja dan aksesibilitas |
| Back-end developer | 5 tahun | Bahasa server, manajemen basis data, desain API, layanan cloud |
| DevOps engineer | 5 tahun | Manajemen konfigurasi, kendali versi, keamanan, pengujian otomatis terukur |
| QA engineer | 5 tahun | Alat otomasi, pengujian API |

## 9. Kesenjangan terbesar

**Blok ini masih kosong.** Belum ada satu CV pun, belum ada pernyataan bertanda tangan, belum
ada pemberi referensi yang dikonfirmasi.

Setiap CV membutuhkan **dua pemberi referensi** yang mampu memberi keterangan dalam bahasa
Inggris, tersedia selama seleksi, dan bukan karyawan, pengurus, rekan bisnis, konsultan yang
diusulkan, maupun pegawai DT Global atau DFAT.

Berbeda dari seluruh isi dokumen ini, **bagian ini tidak bisa diselesaikan dengan menulis.**
Ini pekerjaan menghubungi lima orang beserta sepuluh pemberi referensi.

---

## 10. Lima alternatif yang kita usulkan

RFP membuka ruang ini sendiri: *"Provider could identify other than the list with description
of its advantages and disadvantages."* Karena itu setiap alternatif di bawah disertai
kekurangannya yang sebenarnya. Daftar yang hanya memuat kelebihan tidak akan dipercaya panel.

### Alternatif 1 — Situs statis, bukan aplikasi server

> **[PERLU DIDISKUSIKAN]**
> **Dibahas dengan:** AIPJ3 (Strategic Communications Manager)
> **Kapan:** Rapat awal, Tahap 1
> **Kenapa perlu dibahas:** Konsekuensinya konten terbit dalam 3–6 menit, bukan seketika. Ekspektasi ini harus disepakati di depan, bukan ditemukan saat ada koreksi mendesak.
> **Bila tidak disetujui:** Beralih ke mode server dengan ISR. Biaya hosting dan beban operasional naik, dan SLA 99,9% jadi komitmen aplikasi — bukan lagi CDN.


**Kelebihan.** Nyaris tidak ada permukaan serangan. SLA 99,9% jadi komitmen CDN, bukan
aplikasi. **CMS mati tidak membuat situs ikut mati** — versi terakhir tetap tayang. Kecepatan
terbaik. Biaya hosting cukup murah untuk masuk pagu bersama 12 bulan pemeliharaan.

**Kekurangan.** Konten yang diterbitkan muncul dalam 3–6 menit, bukan seketika. Tidak bisa
personalisasi per pengunjung atau fitur waktu nyata — keduanya memang tidak ada dalam lingkup.
Waktu bangun situs bertambah seiring jumlah konten.

### Alternatif 2 — Payload v3 dipasang sendiri, bukan Contentful atau Sanity

> **[PERLU DIDISKUSIKAN]**
> **Dibahas dengan:** AIPJ3 — RFP mensyaratkan *client-approved CMS*
> **Kapan:** Rapat awal, Tahap 1
> **Kenapa perlu dibahas:** Ini alternatif yang paling mungkin dipertanyakan panel, karena RFP menyebut dua nama secara eksplisit.
> **Bila tidak disetujui:** Pakai Sanity. Biaya lisensi tahun kedua dan seterusnya menjadi tanggungan AIPJ3, dan data draf tersimpan di luar Indonesia.


**Kelebihan.** Tidak ada biaya lisensi selamanya — penting, karena setelah kontrak berakhir
biaya itu jadi tanggungan AIPJ3, bukan kita. Data sepenuhnya di Indonesia. RBAC dan alur
persetujuan sudah bawaan, tanpa perlu paket berbayar. Berbasis Node 22, TypeScript, dan
PostgreSQL — tiga lapisan yang memang disyaratkan RFP. Lisensi MIT, jadi AIPJ3 bebas pindah
vendor kapan pun.

**Kekurangan.** Kita yang mengoperasikannya, sedangkan pada layanan berlangganan vendor yang
mengurus. Ekosistemnya lebih kecil dari Contentful. Server admin harus kita tambal dan pantau
sendiri. **Tidak ada SLA vendor pihak ketiga untuk dijadikan sandaran — komitmen ketersediaan
itu milik kita.** Ini alternatif yang paling mungkin ditanya panel, dan jawabannya: bebannya
terbatas karena server admin tidak berada di jalur kritis situs publik.

### Alternatif 3 — Hosting di Indonesia, bukan platform yang disebut RFP

> **[PERLU DIDISKUSIKAN]**
> **Dibahas dengan:** AIPJ3 **dan** calon penyedia hosting
> **Kapan:** **Sebelum pekerjaan infrastruktur dimulai** — ini gerbang Tahap 1
> **Kenapa perlu dibahas:** Satu-satunya alternatif yang bisa gugur karena alasan teknis, bukan karena keputusan. Penyedia harus terbukti mendukung header HTTP kustom dan API pembersihan cache.
> **Bila tidak disetujui:** Pasang CDN di depan server lokal. Kedaulatan data tetap terjaga, kerumitannya bertambah.


**Kelebihan.** Memenuhi klausul "penyedia lokal" secara harfiah, bukan lewat argumen. Kedaulatan
data memang relevan untuk program kemitraan Pemerintah Indonesia–DFAT. Latensi lebih rendah bagi
audiens Indonesia.

**Kekurangan.** Kematangan peralatan penyedia lokal bervariasi — dukungan header kustom dan API
pembersihan cache tidak selalu ada. Justru karena itu hal ini jadi pemeriksaan wajib di Tahap 1.
Ekosistem otomasi infrastrukturnya belum sematang AWS. Bila pemeriksaan gagal, cadangannya
adalah memasang CDN di depan server lokal.

### Alternatif 4 — Pencarian statis, bukan layanan pencarian berbayar

> **[PERLU DIDISKUSIKAN]**
> **Dibahas dengan:** AIPJ3
> **Kapan:** Rapat awal, Tahap 1
> **Kenapa perlu dibahas:** Ringan — cukup konfirmasi bahwa analitik kata kunci pencarian tidak termasuk kebutuhan wajib.
> **Bila tidak disetujui:** Pasang layanan pencarian berlangganan. Menambah biaya berulang yang berlanjut setelah kontrak berakhir.


**Kelebihan.** Tanpa server, tanpa langganan, mendukung dua bahasa, indeksnya dibangun bersama
situs.

**Kekurangan.** Indeks ikut diunduh pengunjung, jadi ukurannya tumbuh seiring jumlah konten —
tidak masalah pada skala ini. Analitik kata kunci perlu dipasang terpisah.

### Alternatif 5 — Tanpa API publik

> **[PERLU DIDISKUSIKAN]**
> **Dibahas dengan:** AIPJ3
> **Kapan:** Rapat awal, Tahap 1
> **Kenapa perlu dibahas:** Perlu dipastikan tidak ada pihak ketiga yang berencana mengambil data dari situs ini selama masa kontrak.
> **Bila tidak disetujui:** Bangun API publik beserta autentikasi, pembatasan laju, dan pemeliharaannya. Menambah permukaan serangan dan pekerjaan.


**Kelebihan.** Endpoint yang tidak dibuat tidak bisa diserang atau lupa ditambal. Tidak ada
kebutuhan dalam lingkup yang memerlukannya.

**Kekurangan.** Bila kelak ada pihak ketiga yang perlu mengambil data, komponennya harus dibuat
baru. Dicatat sekarang agar menjadi pilihan sadar, bukan keterbatasan yang ditemukan belakangan.

---

## 11. Enam asumsi yang harus dinyatakan di proposal

Jendela pertanyaan sudah tutup 20 Agustus, jadi hal-hal ini tidak bisa lagi ditanyakan resmi.
**Keenamnya berlabel [PERLU DIDISKUSIKAN]** dan harus masuk agenda rapat awal bersama AIPJ3.

| # | Asumsi |
|---|---|
| **A1** | "Penyedia hosting lokal" kami baca sebagai infrastruktur yang berlokasi di Indonesia. Varian memakai platform global tersedia bila maksudnya sekadar penyedia berbadan hukum lokal. |
| **A2** | "CMS yang disetujui klien" memperbolehkan CMS headless di luar dua contoh yang disebut. |
| **A3** | Penyedia hosting terpilih mendukung header HTTP kustom dan API pembersihan cache. **Diperiksa di Tahap 1 sebelum pekerjaan infrastruktur dimulai.** |
| **A4** | Tanggal Keluaran 3 "22 Januari 2026" kami baca sebagai 2027. Keluaran 4–6 diperlakukan sebagai penyelesaian pascapeluncuran di bulan pertama pemeliharaan. |
| **A5** | "Pengujian bersama penyandang disabilitas" berarti sesi berbayar dengan peserta penyandang disabilitas, dan biayanya sudah masuk anggaran Tahap 2. |
| **A6** | Fasilitas pembebasan PPN berdasarkan PMK 59/2024 berlaku, sehingga harga diajukan neto. |

---

## 12. Lima catatan jujur

**Catatan 1 — GTM versus Lighthouse ≥ 90.** RFP mewajibkan Google Tag Manager *dan* skor
Lighthouse minimal 90 di semua kategori. Padahal kontainer GTM standar terbukti menurunkan skor
kecepatan. Solusi kami: GTM hanya dimuat setelah pengunjung menyetujui, dijalankan saat peramban
menganggur, dan kontainernya dibuat seminimal mungkin. Kami berkomitmen pada skor ≥ 90 yang
diukur pada kondisi yang benar-benar dialami pengunjung pertama, dan melaporkan angka
pasca-persetujuan secara terpisah. Menyatakan ketegangan ini lebih meyakinkan daripada
menjanjikan keduanya tanpa syarat.

**Catatan 2 — Definisi uptime 99,9%.** Angka itu memberi jatah henti sekitar 43 menit per bulan.
Cara pengukuran dan definisi "gangguan" perlu disepakati di rapat awal. Definisi yang tidak
tertulis adalah penyebab sengketa SLA yang paling umum.

**Catatan 3 — WCAG 2.2 AA sebagian bergantung pada isi konten.** Pemeriksaan otomatis tidak bisa
mencegah penyunting menulis teks tautan yang tidak informatif atau urutan judul yang keliru.
Karena itu kepatuhan jangka panjang adalah **tanggung jawab bersama**, dan sebaiknya dijelaskan
demikian, dengan dukungan panduan penyuntingan pada pelatihan Keluaran 4.

**Catatan 4 — Uji penetrasi sifatnya rekomendasi.** TOR meminta *"penetration testing
recommendation"*, bukan pengujiannya. Kami menyusun rekomendasi dan lingkupnya; pelaksanaan uji
ada di pihak AIPJ3 dan tidak masuk dalam harga. Perlu ditegaskan di rapat awal karena mudah
disalahpahami ke dua arah.

**Catatan 5 — Blok personel belum terisi.** Bobot 30%, dan tidak bisa diselesaikan dengan
menulis. Lihat Bagian 9.

---

## 13. Rekap: yang perlu didiskusikan

Sebelas butir, terbagi menurut siapa lawan bicaranya.

### Dibahas internal — sebelum proposal dikirim

| Butir | Batas waktu |
|---|---|
| Status akta, SK Kemenkumham, NPWP, surat domisili | **Malam ini** — menentukan ikut atau tidak |
| Lima personel kunci dan sepuluh pemberi referensi (Bagian 9) | Sebelum 26 Agustus |
| Pilihan Opsi A / B / C — lihat `Strategi-Penawaran-AIPJ3.md` | **Malam ini** |

### Dibahas dengan AIPJ3 — dinyatakan di proposal, disepakati di rapat awal

| Butir | Sifat |
|---|---|
| Alternatif 1 — situs statis | Ekspektasi waktu terbit konten |
| Alternatif 2 — Payload v3 | Butuh persetujuan formal *client-approved CMS* |
| Alternatif 3 — hosting Indonesia | **Bisa gugur karena alasan teknis** — gerbang Tahap 1 |
| Alternatif 4 — pencarian statis | Konfirmasi ringan |
| Alternatif 5 — tanpa API publik | Konfirmasi ringan |
| Asumsi A1–A6 | Enam asumsi yang tidak bisa lagi ditanyakan resmi |
| Catatan 1 — GTM versus Lighthouse ≥ 90 | Kontradiksi di dalam RFP, perlu kesepakatan cara ukur |
| Catatan 2 — definisi uptime 99,9% | Definisi tak tertulis adalah sumber sengketa SLA |
| Catatan 4 — uji penetrasi hanya rekomendasi | Mudah disalahpahami ke dua arah |

**Yang paling mendesak:** tiga butir internal. Semua butir AIPJ3 baru relevan setelah penawaran
kita benar-benar dievaluasi.
