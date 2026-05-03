# 📋 Dokumen Serah Terima & Catatan Perubahan
## Sistem Ujian Sekolah Tertulis – SD Muhammadiyah 01 Kukusan
**Repo:** `https://github.com/nitoe/sdm01`  
**PIC:** Pak Arif Azwar Anas · `arif.azwar79@gmail.com`

---

## 🔑 Informasi Teknis Penting

| Item | Nilai |
|---|---|
| **Spreadsheet ID** | `14hrojF0FMjhQjJMX5ZcWVUlwAgniTKw3_ddK_7PXB9I` |
| **Apps Script URL (v2 — AKTIF)** | `https://script.google.com/macros/s/AKfycbzHQPvnoBPRxzNVsGDLZqVE-WRU6Mog0Nj59DLgmLrubydm4S5xID7S-SJzLLXJ6yWujQ/exec` |
| **Apps Script URL (v1 — JANGAN DIPAKAI)** | `https://script.google.com/macros/s/AKfycbwJveJtAISKhveIQ4wspAaeaUKLrqB_IBY55qhOqDOl649QSjqtBa2hYhOrx7UNs0GbdA/exec` |
| **Email pengirim Brevo** | `arif.azwar79@gmail.com` |
| **Brevo plan** | Free (300 email/hari) |

---

## 👥 Daftar Guru dan Email

| No | Nama | Email |
|---|---|---|
| 1 | Pak Arif | arif.azwar79@gmail.com |
| 2 | Pak Raka | febrianrakaramadhan@gmail.com |
| 3 | Bu April | aprilianurhidayati8@gmail.com |
| 4 | Bu Yulia | yuliakatim29@gmail.com |
| 5 | Bu Syam | syamapriwilisseri@gmail.com |
| 6 | Bu Anas | anastasiayulianasari@gmail.com |
| 7 | Bu Ummu | lanternsdm@gmail.com |
| 8 | Bu Azizah | zahroibrahimazizah04@gmail.com |
| 9 | Bu Elya | elyalia38@gmail.com |
| 10 | Bu Marnie SK | marnieseptia1975@gmail.com |
| 11 | Pak Rizki | muhrizki07221@gmail.com |
| 12 | Bu Fitri | idatulfitri4@gmail.com |
| 13 | Pak Zakir | mudzakkirw0@gmail.com |
| 14 | Bu Silvi | silviasadiah@gmail.com |
| 15 | Pak Sandi | sandisandi4655@gmail.com |
| 16 | Bu Elsa | Nisyelsabila@gmail.com |
| 17 | Bu Ratih | ratihratih092@gmail.com |
| 18 | Bu Santi | susantiasuroh783@gmail.com |
| 19 | Bu Evi | eviridho22@gmail.com |
| 20 | Bu Mia | darmiati.mia69@gmail.com |
| 21 | Pak Hendra | hendrahindrawan1@gmail.com |
| 22 | Bu Suci | sucilestarii519@gmail.com |
| 23 | Bu Rahmah | rahma10filisthin@gmail.com |
| 24 | Pak Indra | luzyaspermana9776@gmail.com |
| 25 | Pak Abduh | rahmanabdulah882@gmail.com |

---

## 📁 File yang Perlu Diupload di Sesi Berikutnya

| # | File | Keterangan |
|---|---|---|
| 1 | **`CHANGELOG.md`** (file ini) | Konteks lengkap proyek |
| 2 | **`app_script_v2.gs`** | Referensi backend terbaru |
| 3 | **File HTML yang ingin dikerjakan** | Upload satu per satu atau sekaligus |

---

---

## 📝 Riwayat Perubahan

---

### Sesi 1 — Backend & Infrastruktur
**Tanggal:** sebelum 3 Mei 2026

#### Apps Script — Migrasi ke v2
- Migrasi pengiriman email dari `MailApp` (limit 100/hari) ke **Brevo API** (300/hari gratis)
- Response JSON terstruktur: `{ status, sheet, email, msg }` — HTML dapat membaca hasil pengiriman
- Mendukung **2 pengawas per ujian** (laporan dikirim ke keduanya sekaligus)
- Detail elemen disimpan sebagai teks terbaca di spreadsheet (bukan raw JSON)
- Validasi field wajib sebelum proses
- **Status:** Sudah diuji (`status:success, sheet:true, email:true`) ✅

#### Brevo
- Akun aktif, email pengirim `arif.azwar79@gmail.com` terverifikasi
- API Key terpasang di Apps Script ✅

---

### Sesi 2 — Perbaikan HTML `pendidikan-pancasila.html`
**Tanggal:** 3 Mei 2026  
**File:** `us-tertulis/pendidikan-pancasila.html`  
**Status:** Selesai & telah diuji ✅

#### Perubahan 1 — `SCRIPT_URL` diperbarui ke v2
URL lama (v1) diganti dengan URL Apps Script v2 yang baru agar response JSON dapat dibaca oleh browser.

#### Perubahan 2 — `CONFIG.PENGAWAS` ditambahkan
Array berisi 25 guru beserta email masing-masing. Karena jadwal pengawas belum final dan dapat berubah sewaktu-waktu, seluruh guru dimasukkan sebagai opsi. Untuk membatasi pilihan per mata pelajaran, hapus saja entri yang tidak bertugas dari array tersebut.

#### Perubahan 3 — Slide Login: dropdown pemilihan pengawas
Ditambahkan dua dropdown (Pengawas 1 wajib, Pengawas 2 opsional) dan kotak peringatan kuning: *"Pilih guru yang benar-benar bertugas mengawasimu hari ini."*

#### Perubahan 4 — `init()`: populasi dropdown otomatis
Fungsi `init()` sekarang membaca `CONFIG.PENGAWAS` dan mengisi kedua dropdown secara otomatis saat halaman dimuat.

#### Perubahan 5 — `login()`: validasi & simpan data pengawas
- Wajib memilih Pengawas 1 sebelum bisa masuk ujian
- Validasi tambahan: Pengawas 1 dan Pengawas 2 tidak boleh sama
- Nama dan email pengawas disimpan ke `session` untuk dikirim bersama payload

#### Perubahan 6 — `submitExam()`: fetch diperbarui
- Mode `no-cors` diganti dengan `redirect: 'follow'` agar response JSON bisa dibaca
- Data pengawas (`pengawas1Nama`, `pengawas1Email`, `pengawas2Nama`, `pengawas2Email`) disertakan dalam payload kiriman
- Skor/nilai **tidak lagi ditampilkan** kepada siswa
- Fungsi `_sendPayload()` dipisah untuk mendukung fitur **tombol Coba Lagi**

#### Perubahan 7 — Slide Hasil: tampilkan status pengiriman
Slide hasil tidak lagi menampilkan nilai/skor kepada siswa. Sebagai gantinya ditampilkan:
- ✅ "Laporan berhasil terkirim!" — jika backend merespons `status: success` atau `partial`
- ❌ "Gagal terhubung ke server" + tombol **Coba Lagi** — jika fetch gagal atau error

---

### Sesi 2 (lanjutan) — Fitur Pengatur Ukuran Teks
**Tanggal:** 3 Mei 2026  
**File:** `us-tertulis/pendidikan-pancasila.html`  
**Status:** Selesai ✅

#### Fitur A+ / A− (Pengatur Ukuran Font)
Ditambahkan kontrol ukuran teks di header, di samping timer, untuk membantu siswa yang menggunakan monitor kecil atau resolusi tinggi.

**Cara kerja:**
- Tombol **A+** memperbesar teks, tombol **A−** memperkecil teks
- 6 tingkatan tersedia: 82% → 90% → **100%** (default) → 111% → 122% → 135%
- Persentase ukuran aktif ditampilkan di antara kedua tombol
- Tombol dinonaktifkan (abu-abu) saat sudah mencapai batas minimum atau maksimum
- Pengaturan **disimpan di localStorage** (`UST_FONT_IDX`) dan otomatis dipulihkan saat halaman dibuka kembali
- Header (judul & timer) tidak terpengaruh — hanya area konten soal dan form yang berubah ukurannya

**Detail teknis:**
- CSS variable `--font-scale` pada `:root` dikontrol via JavaScript
- `font-size: calc(1rem * var(--font-scale))` diterapkan ke `.quiz-scroll-area` dan `.center-content-wrapper`
- Method `app.changeFont(dir)` menangani logika naik/turun dan update UI tombol

---

## ⏳ Yang Belum Dikerjakan

### 12 file HTML tersisa (perubahan sama seperti Sesi 2)

```
us-tertulis/
├── al-islam.html
├── bahasa-arab.html
├── bahasa-indonesia.html
├── bahasa-inggris.html
├── bahasa-sunda.html
├── ipas.html
├── kka.html
├── kmdy.html
├── matematika.html
├── pjok.html
├── seni-budaya.html
└── tik.html
```

Setiap file perlu perubahan yang **identik** dengan yang sudah diterapkan di `pendidikan-pancasila.html` (7 perubahan Sesi 2 + fitur A+/A−), dengan penyesuaian:
- `mapel` di `submitExam()` diganti sesuai nama mata pelajaran
- `STORAGE_KEY` di `CONFIG` diganti agar unik per mapel
- Kategori soal (`cats`) di `submitExam()` disesuaikan per mapel

---

## ⚠️ Catatan Penting untuk Sesi Berikutnya

- **Jangan gunakan URL Apps Script lama** di file HTML manapun
- **Fetch harus `redirect: 'follow'`**, bukan `mode: 'no-cors'`
- Fitur A+/A− menggunakan key localStorage `UST_FONT_IDX` — ini **berbagi antar semua file ujian** di perangkat yang sama, sehingga preferensi ukuran font siswa otomatis konsisten di semua mata pelajaran
- Setelah semua HTML selesai, lakukan **uji end-to-end** dari browser langsung
