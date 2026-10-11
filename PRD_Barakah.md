# Product Requirements Document (PRD)

# Barakah: Jadwal Sholat, Kiblat & Donasi

| Atribut | Keterangan |
|---|---|
| Nama Produk | Barakah |
| Platform | Android (utama), iOS (opsional) |
| Jenis Dokumen | PRD, Tugas Akhir Pemrograman Aplikasi Mobile |
| Versi | 1.0 (Draf) |
| Tanggal | 11 Oktober 2026 |
| Penyusun | [Nama Mahasiswa / Kelompok] |
| Dosen Pengampu | [Nama Dosen] |

Tabel 1. Informasi dokumen

---

## 1. Ringkasan Eksekutif

Barakah adalah aplikasi mobile bagi umat Muslim yang menggabungkan ibadah harian dan kegiatan sosial dalam satu aplikasi. Fungsi utamanya adalah menampilkan jadwal sholat sesuai lokasi, menunjukkan arah kiblat dengan sensor, dan mengelola zakat serta donasi secara transparan. Aplikasi ini juga memuat tasbih digital, tanya jawab fikih dasar berbasis AI, kuis pengetahuan Islam, dan pengingat adzan.

Aplikasi ini sengaja memanfaatkan banyak kemampuan perangkat mobile, yaitu lokasi (LBS), sensor (magnetometer dan accelerometer), zona waktu, konversi mata uang, buku catatan berantai hash, AI, game, dan notifikasi terjadwal. Hasilnya, Barakah juga menjadi studi kasus yang utuh untuk mata kuliah Pemrograman Aplikasi Mobile.

## 2. Latar Belakang dan Masalah

1. Pengguna biasanya memakai beberapa aplikasi terpisah untuk jadwal sholat, kompas kiblat, tasbih, dan donasi, sehingga pengalamannya terpecah.
2. Pelancong dan pekerja yang sering berpindah zona waktu kesulitan membandingkan waktu sholat di kota asal dan kota tujuan.
3. Donatur sering tidak yakin apakah catatan donasi mereka tetap utuh dan tidak diubah pengelola.
4. Pengguna yang bertransaksi lintas negara (misalnya umrah atau donasi ke luar negeri) membutuhkan perhitungan zakat dan donasi dalam beberapa mata uang.
5. Pertanyaan fikih dasar sering muncul di tengah aktivitas dan butuh jawaban cepat yang tetap mengarahkan ke rujukan terpercaya.

## 3. Tujuan Produk dan Metrik Keberhasilan

### 3.1 Tujuan

1. Menyediakan jadwal sholat dan arah kiblat yang akurat berdasarkan lokasi pengguna.
2. Menyediakan pencatatan zakat dan donasi yang transparan dan dapat diverifikasi integritasnya.
3. Mendukung pengguna yang bepergian lewat konversi zona waktu dan mata uang.
4. Menyediakan fitur pendukung ibadah (tasbih, kuis, tanya jawab fikih) dalam satu aplikasi.
5. Menunjukkan penerapan teknologi mobile (LBS, sensor, notifikasi, kriptografi dasar, AI) dalam satu produk yang berjalan.

### 3.2 Metrik Keberhasilan

| No | Metrik | Target |
|---|---|---|
| 1 | Waktu tampil jadwal sholat setelah lokasi diperoleh | ≤ 2 detik |
| 2 | Deviasi arah kiblat setelah kalibrasi dibanding rujukan | ≤ 5 derajat |
| 3 | Ketepatan pengingat adzan terhadap waktu sholat | Selisih ≤ 1 menit |
| 4 | Deteksi perubahan data pada ledger donasi | 100% terdeteksi pada uji manipulasi |
| 5 | Jadwal sholat tetap tersedia saat offline | 7 hari ke depan dari cache terakhir |
| 6 | Tingkat selesai alur donasi pada uji pengguna | ≥ 80% |
| 7 | Skor kemudahan penggunaan (SUS) pada uji pengguna | ≥ 68 |

Tabel 2. Metrik keberhasilan

## 4. Target Pengguna dan Persona

### 4.1 Segmentasi

1. Muslim usia 17 sampai 45 tahun yang memakai smartphone Android setiap hari.
2. Pekerja, pelajar, dan musafir yang sering berpindah kota atau negara.
3. Donatur individu yang ingin catatan donasinya transparan.

### 4.2 Persona

| Persona | Profil | Kebutuhan | Titik Masalah |
|---|---|---|---|
| Rizky | Mahasiswa, 21 tahun, tinggal di Yogyakarta | Jadwal akurat, pengingat adzan, tasbih, kuis | Aplikasi penuh iklan dan terpisah-pisah |
| Bu Siti | Karyawan, 45 tahun, sering dinas Jakarta, Makassar, Jayapura | Jadwal di beberapa zona waktu sekaligus, arah kiblat di hotel | Salah menghitung selisih waktu sholat antar kota |
| Pak Ahmad | Jamaah umrah, 52 tahun, perjalanan ke Jeddah dan transit London | Zakat dan donasi dalam SAR, USD, IDR, jadwal di London | Sulit memantau kurs dan memastikan donasi tercatat |

Tabel 3. Persona pengguna

## 5. Ruang Lingkup

### 5.1 Termasuk (In Scope)

1. Jadwal sholat berbasis lokasi dan konversi ke WIB, WITA, WIT, dan London.
2. Pencarian masjid terdekat dan tampilan peta.
3. Kompas kiblat dengan magnetometer, serta kalibrasi dan indikator akurasi.
4. Tasbih digital dengan accelerometer (goyang = hitung) dan tombol manual.
5. Kalkulator zakat dan pencatatan donasi dalam IDR, USD, dan SAR.
6. Ledger donasi berantai hash (SHA-256) dengan verifikasi integritas.
7. Tanya jawab fikih dasar berbasis AI.
8. Kuis pengetahuan Islam.
9. Notifikasi pengingat adzan.

### 5.2 Tidak Termasuk (Out of Scope)

1. Pemrosesan pembayaran riil (payment gateway, transfer bank). Pada versi ini donasi dicatat dan disimulasikan.
2. Blockchain publik terdistribusi seperti Ethereum. Yang dibangun adalah hash chain (rantai hash) sederhana.
3. Fatwa resmi. Jawaban AI bersifat informasi dasar, bukan fatwa.
4. Konten Al-Qur'an lengkap dan audio murottal.
5. Fitur sosial (komentar, pertemanan).

## 6. Arsitektur dan Teknologi yang Direkomendasikan

| Lapisan | Rekomendasi | Alasan |
|---|---|---|
| Framework | Flutter (Dart) | Satu basis kode, dukungan sensor dan notifikasi matang |
| State management | Provider atau Riverpod | Sederhana dan mudah diuji |
| Lokasi | geolocator, geocoding | Akses GPS dan nama kota |
| Peta dan masjid | flutter_map (OpenStreetMap) dan Overpass API, atau Google Places API | Pencarian tempat ibadah terdekat |
| Sensor | sensors_plus (accelerometer, magnetometer), flutter_compass | Arah kiblat dan deteksi goyang |
| Jadwal sholat | Aladhan API atau perhitungan lokal | Jadwal berdasarkan koordinat dan metode hitung |
| Zona waktu | timezone dan intl | Konversi zona waktu IANA, termasuk DST London |
| Kurs | API kurs publik (misal exchangerate.host atau sejenisnya) | Konversi IDR, USD, SAR |
| Penyimpanan lokal | sqflite atau drift (SQLite) | Cache jadwal, ledger, skor kuis |
| Kriptografi | package crypto (SHA-256) | Hash blok ledger |
| Backend opsional | Firebase (Firestore, Auth) | Sinkronisasi dan jangkar hash ledger |
| AI | Anthropic Claude API atau LLM lain lewat layanan perantara | Tanya jawab fikih dasar |
| Notifikasi | flutter_local_notifications, workmanager | Pengingat adzan terjadwal |

Tabel 4. Rekomendasi teknologi

Catatan: pemilihan paket dan penyedia API final perlu diverifikasi ulang saat implementasi, karena ketersediaan, batas pemakaian, dan syarat layanan bisa berubah. Kunci API AI tidak boleh disimpan di dalam aplikasi, sebaiknya dipanggil lewat server perantara.

### 6.1 Gambaran Arsitektur

```
+---------------------------------------------------+
|                 PRESENTATION (UI)                 |
| Beranda | Kiblat | Tasbih | Masjid | Donasi | AI  |
+---------------------------------------------------+
|              STATE MANAGEMENT (Provider)          |
+---------------------------------------------------+
|                  DOMAIN / SERVICE                 |
| PrayerService  QiblaService  TasbihService        |
| TimezoneService CurrencyService LedgerService     |
| AiService  QuizService  NotificationService       |
+---------------------------------------------------+
|                      DATA                         |
| SQLite (cache, ledger) | REST API | Firestore*    |
+---------------------------------------------------+
| PERANGKAT: GPS | Magnetometer | Accelerometer     |
|            Alarm/Notifikasi lokal                 |
+---------------------------------------------------+
* opsional
```

Gambar 1. Arsitektur berlapis aplikasi Barakah

## 7. Kebutuhan Fungsional

Setiap modul memuat deskripsi, kebutuhan (FR) dan kriteria penerimaan (AC) dalam format Given, When, Then.

### 7.1 Modul 1: Onboarding dan Perizinan

Deskripsi: pengguna diminta izin lokasi, notifikasi, dan sensor sebelum fitur dipakai, dengan penjelasan alasan tiap izin.

Kebutuhan:

1. FR-01 Aplikasi menampilkan penjelasan singkat fitur pada peluncuran pertama.
2. FR-02 Aplikasi meminta izin lokasi, notifikasi, dan alarm tepat (Android 12 ke atas) lewat dialog yang menjelaskan manfaatnya.
3. FR-03 Pengguna dapat memilih lokasi manual jika menolak izin lokasi.
4. FR-04 Pengguna dapat memilih metode hitung sholat dan mazhab Ashar di Pengaturan.

Kriteria penerimaan:

1. AC-01 Given pengguna baru, When membuka aplikasi pertama kali, Then layar onboarding tampil sebelum beranda.
2. AC-02 Given izin lokasi ditolak, When pengguna masuk ke beranda, Then aplikasi menawarkan pencarian kota manual dan tidak menutup aplikasi.
3. AC-03 Given izin ditolak permanen, When pengguna menekan tombol aktifkan lokasi, Then aplikasi mengarahkan ke pengaturan sistem.

### 7.2 Modul 2: Jadwal Sholat Berbasis Lokasi (LBS)

Deskripsi: menampilkan waktu Subuh, Terbit, Dzuhur, Ashar, Maghrib, dan Isya berdasarkan koordinat pengguna.

Kebutuhan:

1. FR-05 Aplikasi mengambil koordinat GPS dan nama kota pengguna.
2. FR-06 Aplikasi menampilkan jadwal hari ini, penanda sholat berikutnya, dan hitung mundur.
3. FR-07 Aplikasi menyimpan cache jadwal minimal 7 hari ke depan untuk pemakaian offline.
4. FR-08 Aplikasi memperbarui jadwal otomatis ketika perpindahan lokasi melebihi 20 km.
5. FR-09 Pengguna dapat melihat jadwal hari lain lewat geser tanggal.

Kriteria penerimaan:

1. AC-04 Given GPS aktif dan izin diberikan, When beranda dibuka, Then jadwal enam waktu tampil dengan nama kota dalam 2 detik pada jaringan normal.
2. AC-05 Given sholat berikutnya adalah Ashar, When waktu mendekat, Then kartu Ashar disorot dan hitung mundur berkurang tiap detik.
3. AC-06 Given perangkat offline dan cache tersedia, When beranda dibuka, Then jadwal dari cache tampil dengan label "Data offline".
4. AC-07 Given pengguna berpindah lebih dari 20 km, When aplikasi dibuka, Then jadwal dihitung ulang untuk lokasi baru.

### 7.3 Modul 3: Masjid Terdekat

Deskripsi: mencari dan menampilkan masjid di sekitar pengguna pada daftar dan peta.

Kebutuhan:

1. FR-10 Aplikasi menampilkan masjid dalam radius default 2 km, dapat diubah sampai 10 km.
2. FR-11 Setiap item menampilkan nama, jarak, dan arah ke masjid.
3. FR-12 Pengguna dapat membuka rute lewat aplikasi peta bawaan.
4. FR-13 Hasil pencarian terakhir disimpan di cache.

Kriteria penerimaan:

1. AC-08 Given lokasi tersedia, When pengguna membuka tab Masjid, Then daftar terurut dari jarak terdekat tampil beserta penanda di peta.
2. AC-09 Given tidak ada masjid dalam radius, When pencarian selesai, Then aplikasi menyarankan memperbesar radius.
3. AC-10 Given pengguna menekan tombol rute, When aplikasi peta terpasang, Then rute ke masjid terpilih terbuka.

### 7.4 Modul 4: Arah Kiblat (Magnetometer)

Deskripsi: kompas yang menunjukkan arah Ka'bah dengan membaca magnetometer.

Rumus arah kiblat (bearing dari posisi pengguna ke Ka'bah di koordinat 21.4225 LU, 39.8262 BT):

```
dLon = lonKabah - lonUser            (dalam radian)
y    = sin(dLon) * cos(latKabah)
x    = cos(latUser) * sin(latKabah)
     - sin(latUser) * cos(latKabah) * cos(dLon)
kiblat = (atan2(y, x) dalam derajat + 360) mod 360
```

Kebutuhan:

1. FR-14 Aplikasi menghitung sudut kiblat dari koordinat pengguna.
2. FR-15 Aplikasi membaca heading perangkat dari magnetometer dan menampilkan jarum kompas.
3. FR-16 Aplikasi memberi umpan balik (getar dan perubahan warna) ketika perangkat menghadap kiblat dengan toleransi 3 derajat.
4. FR-17 Aplikasi menampilkan indikator akurasi sensor dan petunjuk kalibrasi gerakan angka 8.
5. FR-18 Aplikasi memberi peringatan jika terdeteksi gangguan medan magnet atau sensor tidak tersedia.

Kriteria penerimaan:

1. AC-11 Given lokasi tersedia, When layar Kiblat dibuka, Then sudut kiblat (derajat) dan jarak ke Ka'bah tampil.
2. AC-12 Given perangkat diputar, When heading berubah, Then jarum bergerak halus (pembaruan minimal 10 kali per detik).
3. AC-13 Given heading berada dalam ±3° dari kiblat, When kondisi tercapai, Then ikon Ka'bah berwarna hijau dan perangkat bergetar singkat.
4. AC-14 Given akurasi sensor rendah, When layar dibuka, Then banner kalibrasi tampil.
5. AC-15 Given perangkat tidak memiliki magnetometer, When layar dibuka, Then aplikasi menampilkan nilai derajat statis dan petunjuk memakai kompas lain.

### 7.5 Modul 5: Tasbih Digital (Accelerometer)

Deskripsi: penghitung dzikir yang bertambah ketika perangkat digoyang.

Kebutuhan:

1. FR-19 Aplikasi menghitung satu goyangan jika magnitudo percepatan melewati ambang (default 15 m/s²) dan jeda antar hitungan minimal 500 ms.
2. FR-20 Pengguna dapat memilih target hitungan (33, 99, 100, atau kustom) dan melakukan reset.
3. FR-21 Pengguna dapat mengatur sensitivitas goyang (rendah, sedang, tinggi) dan mengaktifkan atau menonaktifkan getar.
4. FR-22 Tersedia tombol layar sebagai alternatif hitung manual.
5. FR-23 Riwayat dzikir harian tersimpan di lokal.

Kriteria penerimaan:

1. AC-16 Given mode goyang aktif, When perangkat digoyang sekali, Then penghitung bertambah tepat satu.
2. AC-17 Given goyangan beruntun cepat di bawah 500 ms, When terjadi, Then hanya satu hitungan yang dicatat.
3. AC-18 Given target tercapai, When hitungan sama dengan target, Then perangkat bergetar dan muncul pesan selesai.
4. AC-19 Given layar mati atau aplikasi berpindah ke latar belakang, When perangkat bergoyang, Then penghitung tidak bertambah.

### 7.6 Modul 6: Konversi Zona Waktu (WIB, WITA, WIT, London)

Deskripsi: pengguna dapat melihat jadwal sholat sebuah lokasi dalam zona waktu lain.

Ketentuan zona waktu:

| Zona | Identitas IANA | Selisih UTC |
|---|---|---|
| WIB | Asia/Jakarta | UTC+7 |
| WITA | Asia/Makassar | UTC+8 |
| WIT | Asia/Jayapura | UTC+9 |
| London | Europe/London | UTC+0 (GMT), UTC+1 (BST saat musim panas) |

Tabel 5. Zona waktu yang didukung

Kebutuhan:

1. FR-24 Pengguna memilih zona tampilan (WIB, WITA, WIT, London) dari pemilih zona.
2. FR-25 Aplikasi menampilkan jadwal pada zona tampilan, dengan label zona dan selisih jam terhadap zona lokasi asli.
3. FR-26 Aplikasi menangani perubahan waktu musim panas London (DST) secara otomatis memakai basis data zona IANA.
4. FR-27 Mode bandingkan menampilkan dua zona berdampingan.
5. FR-28 Pengingat adzan selalu dijadwalkan berdasarkan waktu lokal lokasi pengguna saat ini, bukan zona tampilan.

Kriteria penerimaan:

1. AC-20 Given Dzuhur di Yogyakarta pukul 11.45 WIB, When zona tampilan diubah ke WIT, Then waktu tampil 13.45 WIT.
2. AC-21 Given tanggal berada dalam masa BST, When zona London dipilih, Then selisih terhadap WIB dihitung dengan UTC+1.
3. AC-22 Given mode bandingkan aktif, When dua zona dipilih, Then kedua jadwal tampil berdampingan dengan label zona jelas.
4. AC-23 Given zona tampilan bukan zona lokal, When layar dibuka, Then terdapat penanda bahwa waktu ditampilkan dalam zona lain.

### 7.7 Modul 7: Zakat dan Donasi Multi-Mata Uang (IDR, USD, SAR)

Deskripsi: kalkulator zakat dan form donasi yang mendukung tiga mata uang.

Kebutuhan:

1. FR-29 Aplikasi mengambil kurs IDR, USD, dan SAR dari API kurs dan menyimpan cache beserta waktu pembaruan.
2. FR-30 Kalkulator zakat maal menghitung 2,5% dari harta yang mencapai nisab. Nilai nisab (setara 85 gram emas) dan harga emas dapat dikonfigurasi pengguna agar tidak tertanam kaku.
3. FR-31 Aplikasi menyediakan kalkulator zakat fitrah berdasarkan jumlah jiwa dan nilai per jiwa yang dapat diatur.
4. FR-32 Pengguna memilih mata uang input, dan aplikasi menampilkan padanan di dua mata uang lain.
5. FR-33 Pengguna memilih kampanye donasi atau menulis kampanye bebas, memasukkan nominal, lalu mengonfirmasi.
6. FR-34 Setiap donasi terkonfirmasi diteruskan ke modul ledger (Modul 8).
7. FR-35 Jika kurs offline, aplikasi memakai kurs terakhir dan menampilkan waktu pembaruannya.

Kriteria penerimaan:

1. AC-24 Given pengguna memasukkan harta di atas nisab, When menekan hitung, Then zakat 2,5% tampil dalam mata uang input dan padanannya.
2. AC-25 Given harta di bawah nisab, When menekan hitung, Then aplikasi menampilkan keterangan belum wajib zakat.
3. AC-26 Given nominal 100 USD, When kurs tersedia, Then nilai IDR dan SAR tampil dengan pembulatan sesuai mata uang (IDR tanpa desimal, USD dan SAR dua desimal).
4. AC-27 Given kurs tidak dapat diambil, When pengguna menghitung, Then aplikasi memakai kurs cache dan menampilkan "Kurs per [tanggal dan jam]".
5. AC-28 Given nominal kosong, nol, atau negatif, When pengguna mengonfirmasi, Then aplikasi menolak dan menampilkan pesan kesalahan.

### 7.8 Modul 8: Ledger Donasi Berantai Hash

Deskripsi: setiap donasi disimpan sebagai blok yang memuat hash blok sebelumnya, sehingga perubahan pada data lama akan memutus rantai dan terdeteksi.

Struktur blok:

```
Block {
  index         : integer (0 untuk genesis)
  timestamp     : ISO-8601 UTC
  donor_alias   : string
  campaign      : string
  amount        : decimal
  currency      : IDR | USD | SAR
  amount_idr    : decimal (nilai setara saat transaksi)
  rate_used     : decimal
  prev_hash     : string (64 hex)
  hash          : string (64 hex)
}

hash = SHA256( index | timestamp | donor_alias | campaign |
               amount | currency | amount_idr | rate_used | prev_hash )
```

Skema tabel SQLite:

```sql
CREATE TABLE ledger (
  idx          INTEGER PRIMARY KEY,
  timestamp    TEXT    NOT NULL,
  donor_alias  TEXT    NOT NULL,
  campaign     TEXT    NOT NULL,
  amount       REAL    NOT NULL,
  currency     TEXT    NOT NULL CHECK (currency IN ('IDR','USD','SAR')),
  amount_idr   REAL    NOT NULL,
  rate_used    REAL    NOT NULL,
  prev_hash    TEXT    NOT NULL,
  hash         TEXT    NOT NULL UNIQUE
);
```

Kebutuhan:

1. FR-36 Aplikasi membuat blok genesis pada pemakaian pertama.
2. FR-37 Setiap donasi baru menjadi blok dengan prev_hash sama dengan hash blok terakhir.
3. FR-38 Aplikasi menyediakan tombol Verifikasi Rantai yang menghitung ulang semua hash dan mencocokkan prev_hash.
4. FR-39 Jika verifikasi gagal, aplikasi menampilkan indeks blok pertama yang tidak valid.
5. FR-40 Pengguna dapat melihat daftar blok beserta potongan hash (8 karakter awal) dan menyalin hash lengkap.
6. FR-41 Pengguna dapat mengekspor ledger sebagai berkas JSON.
7. FR-42 (Opsional) Hash blok terakhir dikirim ke Firestore sebagai jangkar sehingga penghapusan atau penulisan ulang seluruh rantai lokal tetap terdeteksi.
8. FR-43 Blok tidak dapat diedit atau dihapus dari antarmuka aplikasi.

Kriteria penerimaan:

1. AC-29 Given donasi terkonfirmasi, When disimpan, Then blok baru terbentuk dengan prev_hash sama dengan hash blok sebelumnya.
2. AC-30 Given ledger tidak diubah, When Verifikasi Rantai dijalankan, Then hasilnya "Rantai valid" beserta jumlah blok.
3. AC-31 Given satu nilai pada blok ke-N diubah langsung di basis data, When Verifikasi Rantai dijalankan, Then aplikasi melaporkan "Rantai tidak valid pada blok N".
4. AC-32 Given isi dua blok yang sama, When hash dihitung, Then hasilnya identik (deterministik).
5. AC-33 Given pengguna membuka ledger, When mencari opsi ubah atau hapus blok, Then opsi tersebut tidak tersedia.

Batasan yang perlu dipahami: hash chain lokal hanya membuktikan keutuhan terhadap perubahan sebagian. Pihak yang mengendalikan perangkat sepenuhnya dapat membangun ulang seluruh rantai. Karena itu jangkar hash eksternal (FR-42) direkomendasikan untuk klaim "tidak bisa diubah diam-diam".

### 7.9 Modul 9: Tanya Jawab Fikih Dasar (AI)

Deskripsi: asisten percakapan untuk pertanyaan fikih dasar seperti tata cara wudhu, sholat, dan puasa.

Kebutuhan:

1. FR-44 Pengguna mengetik pertanyaan dan menerima jawaban dalam bahasa Indonesia.
2. FR-45 Sistem prompt membatasi cakupan pada fikih dasar, meminta jawaban menyebut adanya perbedaan pendapat antar mazhab bila relevan, dan tidak mengeluarkan fatwa.
3. FR-46 Setiap jawaban disertai catatan: "Ini informasi umum, konsultasikan dengan ulama atau ustadz untuk kasus spesifik."
4. FR-47 Pertanyaan di luar cakupan (misalnya politik atau fatwa kasus pribadi yang kompleks) dijawab dengan penolakan sopan dan saran bertanya kepada ulama.
5. FR-48 Riwayat percakapan disimpan lokal dan dapat dihapus pengguna.
6. FR-49 Permintaan dibatasi (rate limit) dan menampilkan status memuat serta kesalahan jaringan.
7. FR-50 Pemanggilan AI dilakukan lewat server perantara agar kunci API tidak berada dalam aplikasi.

Kriteria penerimaan:

1. AC-34 Given pertanyaan "Apa saja rukun wudhu?", When dikirim, Then jawaban terstruktur tampil beserta catatan disclaimer.
2. AC-35 Given pertanyaan di luar cakupan, When dikirim, Then aplikasi menolak dengan sopan dan menyarankan bertanya kepada ulama.
3. AC-36 Given koneksi terputus, When pertanyaan dikirim, Then pesan kesalahan tampil dan pertanyaan dapat dikirim ulang.
4. AC-37 Given pengguna memilih hapus riwayat, When dikonfirmasi, Then seluruh percakapan lokal terhapus.

### 7.10 Modul 10: Kuis Pengetahuan Islam (Game)

Deskripsi: kuis pilihan ganda berkategori dengan skor dan papan skor lokal.

Kebutuhan:

1. FR-51 Kategori kuis: Rukun Islam dan Iman, Sejarah Nabi, Fikih Dasar, dan Umum.
2. FR-52 Satu sesi terdiri dari 10 soal acak dengan 4 pilihan jawaban dan batas waktu 20 detik per soal.
3. FR-53 Setelah menjawab, aplikasi menampilkan jawaban benar dan penjelasan singkat.
4. FR-54 Skor dihitung dari jawaban benar dan bonus kecepatan, lalu disimpan sebagai skor tertinggi per kategori.
5. FR-55 Bank soal tersimpan lokal (JSON atau SQLite) dan dapat diperbarui.

Kriteria penerimaan:

1. AC-38 Given kategori dipilih, When kuis dimulai, Then 10 soal acak tanpa duplikat tampil satu per satu.
2. AC-39 Given waktu 20 detik habis, When pengguna belum menjawab, Then soal dihitung salah dan lanjut ke soal berikutnya.
3. AC-40 Given kuis selesai, When ringkasan tampil, Then skor akhir, jumlah benar, dan skor tertinggi kategori ditampilkan.

### 7.11 Modul 11: Notifikasi Pengingat Adzan

Deskripsi: notifikasi terjadwal pada setiap waktu sholat.

Kebutuhan:

1. FR-56 Aplikasi menjadwalkan notifikasi lokal untuk lima waktu sholat (dan opsional Terbit) selama 7 hari ke depan.
2. FR-57 Pengguna dapat mengaktifkan atau menonaktifkan pengingat per waktu sholat dan memilih suara (adzan penuh, adzan pendek, nada standar).
3. FR-58 Pengguna dapat memilih pengingat sebelum waktu masuk (0, 5, 10, atau 15 menit).
4. FR-59 Jadwal notifikasi dihitung ulang saat lokasi berubah signifikan, zona waktu berubah, atau pengaturan diubah.
5. FR-60 Jadwal notifikasi dijadwalkan ulang setelah perangkat dinyalakan ulang.
6. FR-61 Aplikasi menampilkan petunjuk pengecualian optimasi baterai pada perangkat yang membatasi proses latar belakang.

Kriteria penerimaan:

1. AC-41 Given pengingat Maghrib aktif, When waktu Maghrib tiba, Then notifikasi muncul dengan selisih paling lama 1 menit.
2. AC-42 Given pengguna menonaktifkan pengingat Dzuhur, When waktu Dzuhur tiba, Then tidak ada notifikasi Dzuhur.
3. AC-43 Given perangkat dimulai ulang, When sistem aktif kembali, Then notifikasi tetap terjadwal.
4. AC-44 Given pengguna berpindah ke lokasi baru, When jadwal diperbarui, Then notifikasi lama dibatalkan dan diganti sesuai lokasi baru.

## 8. Kebutuhan Non-Fungsional

| Kode | Kategori | Kebutuhan |
|---|---|---|
| NFR-01 | Kinerja | Waktu mulai dingin aplikasi ≤ 3 detik pada perangkat kelas menengah |
| NFR-02 | Kinerja | Pembaruan sensor kompas ≥ 10 Hz tanpa gangguan tampilan (60 fps) |
| NFR-03 | Keandalan | Fitur jadwal, kiblat, tasbih, dan ledger berfungsi tanpa internet |
| NFR-04 | Keamanan | Seluruh komunikasi jaringan memakai HTTPS |
| NFR-05 | Keamanan | Kunci API tidak disimpan dalam kode aplikasi |
| NFR-06 | Privasi | Koordinat tidak dikirim ke server selain penyedia jadwal dan masjid yang diperlukan, dan tidak disimpan jangka panjang |
| NFR-07 | Privasi | Nama donatur memakai alias, tidak ada data pribadi sensitif pada ledger |
| NFR-08 | Kegunaan | Target sentuh minimal 48 dp, kontras teks sesuai WCAG AA |
| NFR-09 | Aksesibilitas | Mendukung ukuran huruf sistem dan pembaca layar dasar |
| NFR-10 | Kompatibilitas | Android 8.0 (API 26) ke atas |
| NFR-11 | Lokalisasi | Bahasa Indonesia sebagai bahasa utama, struktur siap untuk bahasa lain |
| NFR-12 | Konsumsi daya | Sensor dilepas (unsubscribe) saat layar sensor tidak aktif |
| NFR-13 | Kualitas | Cakupan uji unit minimal 60% untuk logika perhitungan (kiblat, zakat, hash, zona waktu) |

Tabel 6. Kebutuhan non-fungsional

## 9. Alur Pengguna (User Flow)

### 9.1 Alur Peluncuran dan Jadwal Sholat

```
[Mulai]
   |
   v
[Pertama kali?] --ya--> [Onboarding] --> [Minta izin lokasi/notifikasi]
   |tidak                                      |
   v                                           v
[Beranda] <-------------------------- [Izin diberikan?]
   |                                    |ya        |tidak
   |                                    |          v
   |                                    |   [Pilih kota manual]
   |                                    v          |
   +---------------------------> [Ambil lokasi] <--+
                                       |
                                       v
                          [Online?] --ya--> [Ambil jadwal dari API]
                              |tidak              |
                              v                    v
                      [Pakai cache]        [Simpan cache + jadwalkan adzan]
                              |                    |
                              +--------+-----------+
                                       v
                          [Tampilkan jadwal + hitung mundur]
```

Gambar 2. Alur peluncuran dan jadwal sholat

### 9.2 Alur Arah Kiblat

1. Pengguna membuka tab Kiblat.
2. Aplikasi mengecek ketersediaan lokasi. Jika tidak ada, aplikasi meminta izin atau lokasi manual.
3. Aplikasi menghitung sudut kiblat dan jarak ke Ka'bah.
4. Aplikasi mengaktifkan magnetometer. Jika tidak tersedia, tampilkan sudut statis dan keluar dari alur.
5. Aplikasi mengecek akurasi sensor. Jika rendah, tampilkan petunjuk kalibrasi gerakan angka 8.
6. Pengguna memutar perangkat sampai jarum menghadap penanda kiblat.
7. Ketika sudut berada dalam ±3°, aplikasi memberi getar dan warna hijau.
8. Pengguna meninggalkan layar, dan aplikasi melepas sensor.

### 9.3 Alur Zakat dan Donasi sampai Ledger

```
[Tab Donasi]
     |
     v
[Pilih: Zakat / Donasi]
     |                      |
 (Zakat)                (Donasi)
     v                      v
[Input harta+mata uang] [Pilih kampanye]
     v                      v
[Hitung vs nisab]       [Input nominal+mata uang]
     v                      |
[Hasil zakat] --lanjut--> [Ringkasan: nominal, kurs, setara IDR]
                            |
                            v
                      [Konfirmasi donasi?] --tidak--> [Kembali]
                            |ya
                            v
                  [Buat blok: prev_hash + hash baru]
                            |
                            v
                  [Simpan ke SQLite (+ jangkar hash opsional)]
                            |
                            v
                  [Bukti donasi + hash blok]
                            |
                            v
                  [Buka Ledger] --> [Verifikasi Rantai] --> [Valid / Tidak valid di blok N]
```

Gambar 3. Alur zakat, donasi, dan ledger

### 9.4 Alur Tasbih Digital

1. Pengguna membuka tab Tasbih dan memilih target hitungan.
2. Pengguna memilih mode goyang atau tombol manual.
3. Pada mode goyang, aplikasi berlangganan accelerometer dan menghitung magnitudo percepatan.
4. Jika magnitudo melebihi ambang dan jeda lebih dari 500 ms, hitungan bertambah satu.
5. Saat hitungan mencapai target, aplikasi bergetar dan menampilkan penanda selesai.
6. Pengguna dapat mereset atau memulai putaran baru.

### 9.5 Alur Tanya Jawab AI dan Kuis

1. Tanya AI: pengguna mengetik pertanyaan, aplikasi mengirim ke server perantara, server memanggil model dengan sistem prompt fikih dasar, jawaban ditampilkan beserta disclaimer, riwayat disimpan lokal.
2. Kuis: pengguna memilih kategori, 10 soal tampil berurutan dengan penghitung waktu, tiap jawaban diikuti penjelasan, ringkasan skor tampil di akhir dan skor tertinggi diperbarui.

## 10. Wireframe

Wireframe berikut berupa sketsa kasar (low-fidelity). Tampilan akhir mengikuti panduan desain Material 3.

### 10.1 Beranda dan Jadwal Sholat

```
+--------------------------------+
| Barakah               [Gear]   |
| Yogyakarta, DI Yogyakarta      |
| Zona: [WIB v]    [Bandingkan]  |
+--------------------------------+
|  Sholat berikutnya: ASHAR      |
|        15:08 WIB               |
|     dalam 02:14:35             |
+--------------------------------+
| Subuh      04:25        [Bell] |
| Terbit     05:41                |
| Dzuhur     11:46        [Bell] |
| Ashar      15:08  <---- next   |
| Maghrib    17:52        [Bell] |
| Isya       19:03        [Bell] |
+--------------------------------+
| < 10 Okt   Hari ini   12 Okt > |
+--------------------------------+
| [Jadwal][Kiblat][Tasbih][Masjid]|
| [Donasi][Tanya AI][Kuis]       |
+--------------------------------+
```

Gambar 4. Wireframe beranda (angka waktu hanya contoh ilustrasi)

### 10.2 Kiblat

```
+--------------------------------+
| < Arah Kiblat                  |
+--------------------------------+
|        Kiblat: 295 derajat     |
|        Jarak ke Ka'bah: 8.xxx km|
|                                |
|              N                 |
|          .---^---.             |
|         /    |    \            |
|        W  ---+--->  E          |
|         \    Ka'bah   /        |
|          '---v---'             |
|              S                 |
|   Heading: 290 derajat         |
|   [ Hampir tepat: selisih 5 ]  |
+--------------------------------+
| Akurasi sensor: Sedang         |
| [Cara kalibrasi (angka 8)]     |
+--------------------------------+
```

Gambar 5. Wireframe layar kiblat

### 10.3 Tasbih Digital

```
+--------------------------------+
| < Tasbih Digital               |
+--------------------------------+
|  Target: [33][99][100][Kustom] |
|                                |
|           .-----------.        |
|          |     27      |       |
|          |   dari 33   |       |
|           '-----------'        |
|                                |
|  Mode: (o) Goyang  ( ) Manual  |
|  Sensitivitas: [----o----]     |
|  Getar: [ON]                   |
|                                |
|     [   TAP UNTUK HITUNG   ]   |
|            [ Reset ]           |
+--------------------------------+
```

Gambar 6. Wireframe tasbih digital

### 10.4 Masjid Terdekat

```
+--------------------------------+
| < Masjid Terdekat   Radius: 2km|
+--------------------------------+
| [        PETA OSM        ]     |
| [   o  masjid   o   (Anda)  ]  |
+--------------------------------+
| 1. Masjid Al-Contoh     350 m  |
|    arah: Timur Laut     [Rute] |
| 2. Masjid An-Contoh     720 m  |
|    arah: Barat          [Rute] |
| 3. Musholla Contoh      1,1 km |
|    arah: Selatan        [Rute] |
+--------------------------------+
```

Gambar 7. Wireframe masjid terdekat (nama hanya contoh)

### 10.5 Zakat dan Donasi

```
+--------------------------------+
| < Zakat & Donasi               |
+--------------------------------+
| [ Zakat ]  [ Donasi ]          |
+--------------------------------+
| Mata uang: [IDR] [USD] [SAR]   |
| Nominal:   [ 1.000.000      ]  |
| Kampanye:  [ Pilih kampanye v ]|
|                                |
| Setara:  USD 63,xx | SAR 237,xx|
| Kurs per: 11 Okt 2026 08:00    |
|                                |
| Alias donatur: [ Hamba Allah ] |
|                                |
|      [   KONFIRMASI DONASI  ]  |
+--------------------------------+
```

Gambar 8. Wireframe form donasi (nilai hanya ilustrasi)

### 10.6 Ledger Donasi

```
+--------------------------------+
| < Ledger Donasi                |
| Status: [ Rantai valid: 12 blok]|
|                  [Verifikasi]  |
+--------------------------------+
| #12  11 Okt 2026 08:15         |
|      Hamba Allah | IDR 100.000 |
|      hash: 9f3a1c7e...        |
|      prev: 4b2d88a0...        |
+--------------------------------+
| #11  10 Okt 2026 19:40         |
|      Siti | SAR 50,00          |
|      hash: 4b2d88a0...        |
|      prev: c71e03fd...        |
+--------------------------------+
|  [ Ekspor JSON ]               |
+--------------------------------+
```

Gambar 9. Wireframe ledger (hash hanya contoh)

### 10.7 Tanya AI

```
+--------------------------------+
| < Tanya Fikih Dasar    [Hapus] |
+--------------------------------+
|        Anda:                   |
|        Apa saja rukun wudhu?   |
|                                |
| Barakah AI:                    |
| 1. Niat ...                    |
| 2. Membasuh wajah ...          |
| (ringkasan jawaban)            |
| Catatan: informasi umum,       |
| konsultasikan dengan ulama.    |
+--------------------------------+
| [ Ketik pertanyaan...   ][Kirim]|
+--------------------------------+
```

Gambar 10. Wireframe tanya jawab AI

### 10.8 Kuis

```
+--------------------------------+
| Kuis: Rukun Islam    Soal 3/10 |
| Waktu: 00:14        Skor: 20   |
+--------------------------------+
| Berapa jumlah rukun Islam?     |
|                                |
|  [ A. 3 ]    [ B. 4 ]          |
|  [ C. 5 ]    [ D. 6 ]          |
+--------------------------------+
```

Gambar 11. Wireframe kuis

## 11. Pengaturan dan Navigasi

1. Navigasi utama berupa bottom navigation dengan 5 tab: Jadwal, Kiblat, Tasbih, Donasi, Lainnya.
2. Tab Lainnya memuat Masjid Terdekat, Tanya AI, Kuis, dan Pengaturan.
3. Pengaturan memuat metode hitung sholat, mazhab Ashar, zona tampilan, pengingat adzan per waktu, suara, sensitivitas tasbih, mata uang utama, dan hapus data.

## 12. Model Data Ringkas

| Entitas | Atribut Utama |
|---|---|
| PrayerCache | date, lat, lon, method, fajr, sunrise, dhuhr, asr, maghrib, isha |
| Settings | calc_method, asr_school, display_tz, notif_flags, sound, shake_sensitivity, base_currency |
| ExchangeRate | base, quote, rate, fetched_at |
| LedgerBlock | idx, timestamp, donor_alias, campaign, amount, currency, amount_idr, rate_used, prev_hash, hash |
| TasbihLog | date, target, count |
| ChatMessage | id, role, content, created_at |
| QuizQuestion | id, category, question, options, answer_index, explanation |
| QuizScore | category, best_score, last_played_at |

Tabel 7. Entitas data

## 13. Dependensi Eksternal dan Integrasi

| Layanan | Kegunaan | Strategi Gagal |
|---|---|---|
| API jadwal sholat | Waktu sholat berdasarkan koordinat | Cache 7 hari atau hitung lokal |
| Overpass atau Places API | Daftar masjid terdekat | Tampilkan hasil cache terakhir |
| API kurs | Konversi IDR, USD, SAR | Pakai kurs cache berstempel waktu |
| Layanan AI lewat server perantara | Tanya jawab fikih | Pesan kesalahan dan opsi kirim ulang |
| Firestore (opsional) | Jangkar hash ledger | Antri dan kirim ulang saat online |

Tabel 8. Integrasi layanan eksternal

## 14. Risiko dan Mitigasi

| No | Risiko | Dampak | Mitigasi |
|---|---|---|---|
| 1 | Akurasi kiblat terganggu medan magnet | Arah salah | Kalibrasi, indikator akurasi, peringatan interferensi |
| 2 | Pembatasan latar belakang oleh sistem (hemat baterai) | Adzan tidak muncul | Alarm tepat, petunjuk pengecualian baterai, jadwal ulang berkala |
| 3 | Batas jumlah notifikasi terjadwal (terutama iOS) | Notifikasi tidak lengkap | Jadwalkan jendela 7 hari dan jadwalkan ulang saat aplikasi dibuka |
| 4 | Jawaban AI keliru atau tidak sesuai mazhab | Informasi menyesatkan | Batasi cakupan, disclaimer, sebut perbedaan pendapat, tautkan rujukan |
| 5 | Klaim "tidak bisa diubah" pada ledger lokal | Ekspektasi berlebihan | Jelaskan batasan, jangkar hash eksternal, istilah "rantai hash" |
| 6 | Kurs tidak tersedia atau berubah cepat | Nilai tidak akurat | Cache berstempel waktu, simpan rate_used pada tiap blok |
| 7 | Salah tafsir nisab dan harga emas | Zakat salah hitung | Nilai dapat dikonfigurasi, catatan rujukan lembaga resmi |
| 8 | Izin lokasi ditolak | Fitur utama tidak jalan | Mode lokasi manual |
| 9 | Perbedaan metode hitung sholat | Selisih waktu antar aplikasi | Metode dapat dipilih, tampilkan metode aktif |

Tabel 9. Risiko dan mitigasi

## 15. Rencana Pengembangan (Milestone)

| Tahap | Cakupan | Estimasi |
|---|---|---|
| 1 | Setup proyek, onboarding, perizinan, navigasi | Minggu 1 |
| 2 | Jadwal sholat, lokasi, cache, zona waktu | Minggu 2 sampai 3 |
| 3 | Kiblat, tasbih (sensor) | Minggu 3 sampai 4 |
| 4 | Masjid terdekat, notifikasi adzan | Minggu 4 sampai 5 |
| 5 | Kurs, zakat, donasi, ledger hash chain | Minggu 5 sampai 6 |
| 6 | AI tanya jawab, kuis | Minggu 6 sampai 7 |
| 7 | Pengujian, perbaikan, dokumentasi, demo | Minggu 7 sampai 8 |

Tabel 10. Milestone (estimasi, dapat disesuaikan dengan jadwal tugas akhir)

## 16. Strategi Pengujian

1. Uji unit: rumus kiblat, zakat 2,5% dan nisab, pembulatan mata uang, konversi zona waktu (termasuk DST London), pembuatan dan verifikasi hash.
2. Uji widget: layar jadwal, form donasi, kuis.
3. Uji integrasi: alur lokasi ke jadwal ke notifikasi, alur donasi ke ledger.
4. Uji perangkat nyata: sensor magnetometer dan accelerometer pada minimal dua perangkat berbeda.
5. Uji manipulasi ledger: ubah satu baris di SQLite, pastikan verifikasi gagal pada blok yang benar.
6. Uji kegunaan: minimal 5 responden dengan skenario tugas dan kuesioner SUS.

## 17. Pemetaan terhadap Kompetensi Mata Kuliah

| Komponen | Implementasi di Barakah | Modul |
|---|---|---|
| LBS | Lokasi, jadwal sholat, masjid terdekat | 2, 3 |
| Sensor | Magnetometer (kiblat), accelerometer (tasbih) | 4, 5 |
| Waktu | Konversi WIB, WITA, WIT, London | 6 |
| Mata uang | Zakat dan donasi IDR, USD, SAR | 7 |
| Blockchain | Ledger berantai hash SHA-256 | 8 |
| AI | Tanya jawab fikih dasar | 9 |
| Game | Kuis pengetahuan Islam | 10 |
| Notifikasi | Pengingat adzan | 11 |

Tabel 11. Pemetaan fitur terhadap komponen tugas

## 18. Asumsi dan Pertanyaan Terbuka

1. Asumsi: platform utama Android dengan Flutter. Jika memakai teknologi lain, Bagian 6 perlu disesuaikan.
2. Asumsi: donasi bersifat simulasi tanpa transaksi pembayaran nyata.
3. Asumsi: ledger disimpan lokal, dengan jangkar Firestore sebagai fitur opsional.
4. Pertanyaan terbuka 1: metode hitung sholat default (misalnya Kemenag RI) perlu ditetapkan.
5. Pertanyaan terbuka 2: penyedia AI dan mekanisme server perantara perlu diputuskan.
6. Pertanyaan terbuka 3: sumber bank soal kuis dan peninjau kontennya perlu ditentukan.

## 19. Glosarium

| Istilah | Arti |
|---|---|
| LBS | Location-Based Service, layanan berbasis lokasi |
| Magnetometer | Sensor medan magnet untuk menentukan arah utara magnetik |
| Accelerometer | Sensor percepatan untuk mendeteksi gerakan atau goyangan |
| DST | Daylight Saving Time, perubahan waktu musim panas |
| Hash chain | Rangkaian blok data di mana tiap blok memuat hash blok sebelumnya |
| SHA-256 | Fungsi hash kriptografi yang menghasilkan keluaran 256 bit (64 karakter heksadesimal) |
| Nisab | Batas minimal harta yang wajib dizakati |
| WCAG | Web Content Accessibility Guidelines, pedoman aksesibilitas |

Tabel 12. Glosarium
