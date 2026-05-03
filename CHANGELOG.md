# 📋 Dokumen Serah Terima Proyek
## Sistem Ujian Sekolah Tertulis – SD Muhammadiyah 01 Kukusan
**Tanggal:** 3 Mei 2026  
**Status:** Backend selesai ✅ | Perubahan HTML: belum dimulai ⏳

---

## 🧭 Konteks Proyek

Proyek ini adalah sistem ujian sekolah tertulis online untuk **kelas 6 SD Muhammadiyah 01 Kukusan**, bagian dari repo GitHub `https://github.com/nitoe/sdm01`. File ujian berbasis HTML murni (tanpa framework), dilengkapi backend Google Apps Script yang menyimpan hasil ke Google Spreadsheet dan mengirim laporan ke email guru pengawas.

**Pengembang/PIC:** Pak Arif Azwar Anas (Guru Kelas 6 & Wakasek Kurikulum)  
**Email PIC:** arif.azwar79@gmail.com

---

## ✅ Yang Sudah Selesai di Sesi Ini

### 1. Backend Apps Script (v2) — SELESAI
- Migrasi pengiriman email dari `MailApp` (limit 100/hari) ke **Brevo API** (300/hari gratis)
- Response JSON terstruktur: `{ status, sheet, email, msg }` — memungkinkan HTML membaca hasil pengiriman
- Mendukung **2 pengawas per ujian** (email dikirim ke keduanya sekaligus)
- Detail elemen disimpan sebagai teks terbaca di spreadsheet (bukan raw JSON)
- Validasi field wajib sebelum proses
- **Sudah diuji dan berjalan sempurna** (`status:success, sheet:true, email:true`)

### 2. Brevo — SELESAI
- Akun Brevo aktif, email pengirim `arif.azwar79@gmail.com` terverifikasi
- API Key sudah terpasang di Apps Script

---

## 🔑 Informasi Teknis Penting

| Item | Nilai |
|---|---|
| **Spreadsheet ID** | `14hrojF0FMjhQjJMX5ZcWVUlwAgniTKw3_ddK_7PXB9I` |
| **Apps Script URL (BARU – v2)** | `https://script.google.com/macros/s/AKfycbzHQPvnoBPRxzNVsGDLZqVE-WRU6Mog0Nj59DLgmLrubydm4S5xID7S-SJzLLXJ6yWujQ/exec` |
| **Apps Script URL (LAMA – v1, jangan dipakai)** | `https://script.google.com/macros/s/AKfycbwJveJtAISKhveIQ4wspAaeaUKLrqB_IBY55qhOqDOl649QSjqtBa2hYhOrx7UNs0GbdA/exec` |
| **Email pengirim Brevo** | `arif.azwar79@gmail.com` |
| **Brevo plan** | Free (300 email/hari) |
| **Email penerima laporan** | 2 guru pengawas per ujian (dipilih siswa dari dropdown) |

---

## ⏳ Yang Belum Dikerjakan — Agenda Sesi Berikutnya

### Perubahan HTML pada 13 file ujian di folder `us-tertulis/`

Setiap file HTML perlu **5 perubahan**:

1. **`CONFIG.PENGAWAS`** — tambah array 2 pengawas (nama + email) per mata pelajaran
2. **Slide Login** — tambah 2 dropdown pemilihan guru pengawas + peringatan jangan salah pilih
3. **`init()`** — tambah kode populasi dropdown pengawas
4. **`login()`** — tambah validasi pemilihan pengawas + simpan ke session
5. **`submitExam()`** — ganti dengan versi baru yang:
   - Tidak menampilkan nilai/skor ke siswa
   - Menggunakan fetch dengan `redirect: 'follow'` (bukan `no-cors`)
   - Menampilkan konfirmasi "laporan terkirim" atau pesan error + tombol retry
   - Menyertakan data pengawas ke payload kiriman
6. **Slide Hasil** — ganti konten dari tampilan nilai menjadi tampilan status pengiriman
7. **`SCRIPT_URL`** — ganti URL lama dengan URL baru v2

### Daftar 13 file yang perlu diubah:
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
├── pendidikan-pancasila.html  ← gunakan ini sebagai referensi/template
├── pjok.html
├── seni-budaya.html
└── tik.html
```

### Yang belum diputuskan:
- **Jadwal pengawas per mata pelajaran** belum diterima. Perlu ditentukan guru mana (Pengawas 1 & 2) untuk setiap mata pelajaran sebelum HTML bisa diubah.

---

## 👥 Daftar Guru dan Email

```
1.  Pak Arif    : arif.azwar79@gmail.com
2.  Pak Raka    : febrianrakaramadhan@gmail.com
3.  Bu April    : aprilianurhidayati8@gmail.com
4.  Bu Yulia    : yuliakatim29@gmail.com
5.  Bu Syam     : syamapriwilisseri@gmail.com
6.  Bu Anas     : anastasiayulianasari@gmail.com
7.  Bu Ummu     : lanternsdm@gmail.com
8.  Bu Azizah   : zahroibrahimazizah04@gmail.com
9.  Bu Elya     : elyalia38@gmail.com
10. Bu Marnie SK: marnieseptia1975@gmail.com
11. Pak Rizki   : muhrizki07221@gmail.com
12. Bu Fitri    : idatulfitri4@gmail.com
13. Pak Zakir   : mudzakkirw0@gmail.com
14. Bu Silvi    : silviasadiah@gmail.com
15. Pak Sandi   : sandisandi4655@gmail.com
16. Bu Elsa     : Nisyelsabila@gmail.com
17. Bu Ratih    : ratihratih092@gmail.com
18. Bu Santi    : susantiasuroh783@gmail.com
19. Bu Evi      : eviridho22@gmail.com
20. Bu Mia      : darmiati.mia69@gmail.com
21. Pak Hendra  : hendrahindrawan1@gmail.com
22. Bu Suci     : sucilestarii519@gmail.com
23. Bu Rahmah   : rahma10filisthin@gmail.com
24. Pak Indra   : luzyaspermana9776@gmail.com
25. Pak Abduh   : rahmanabdulah882@gmail.com
```

---

## 📁 File Referensi yang Perlu Diupload di Sesi Berikutnya

Upload file-file ini di awal percakapan baru:

| # | File | Keterangan |
|---|---|---|
| 1 | **`SERAH_TERIMA_PROYEK.md`** (file ini) | Konteks lengkap proyek |
| 2 | **`app_script_v2.gs`** | Referensi backend terbaru |
| 3 | **`Daftar_guru_dan_emailnya.txt`** | Untuk config PENGAWAS |
| 4 | **File HTML yang ingin dikerjakan** | Upload satu per satu atau sekaligus |

> 💡 **Saran urutan pengerjaan:** Mulai dari `pendidikan-pancasila.html` karena sudah paling familiar, jadikan template, lalu replikasi ke file lain.

---

## 📌 Instruksi untuk Claude di Sesi Berikutnya

Saat memulai percakapan baru, gunakan prompt pembuka seperti ini:

> *"Ini adalah kelanjutan proyek ujian sekolah SDM01. Saya upload dokumen serah terima dan file terkait. Tolong baca dulu dokumen serah terimanya, lalu kita lanjutkan mengerjakan perubahan HTML file ujian. Saya juga akan segera memberikan jadwal pengawas per mata pelajaran."*

---

## ⚠️ Catatan Penting

- **Jangan gunakan URL Apps Script lama** di file HTML manapun. Semua file harus menggunakan URL v2 yang baru.
- **Fetch harus menggunakan `redirect: 'follow'`**, bukan `mode: 'no-cors'`, agar response dari server bisa dibaca oleh browser.
- Setelah semua HTML selesai diubah, lakukan **uji coba end-to-end** dari browser dengan membuka salah satu file HTML langsung.
