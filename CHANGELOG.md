# 📋 Catatan Perubahan — Sesi 3
**Tanggal:** 3 Mei 2026
**File yang diubah:** `pendidikan-pancasila.html`, `bahasa-inggris.html`
**Status:** Selesai ✅

---

## 🐛 Bug yang Diperbaiki

### Bug 1 — Kontrol A−/A+ dan timer tampil sebelum ujian dimulai
**File:** keduanya
**Gejala:** Tombol A−/A+ dan timer `--:--` terlihat di header saat slide PIN dan Login, padahal seharusnya hanya muncul ketika ujian sudah dimulai.
**Perbaikan:**
- Bungkus `font-ctrl` dan `timer-box` dalam satu `<div id="exam-controls" style="display:none">` di dalam header.
- `user-badge` (nama siswa) turut dipindahkan ke dalam div tersebut agar konsisten.
- Di fungsi `startExam()`, tambahkan: `document.getElementById('exam-controls').style.display = 'flex'` sehingga kontrol baru muncul tepat saat ujian mulai.

---

### Bug 2 — Soal tertutup / tidak terlihat di `bahasa-inggris.html` (tampilan 100%)
**File:** `bahasa-inggris.html` saja
**Gejala:** Navigasi soal (sidebar kanan) menimpa area soal. Soal baru terlihat ketika browser di-zoom out.
**Akar masalah:** Satu `</div>` ekstra tepat setelah penutup `slide-result` (baris 214 pada versi lama). Akibatnya:
- `</div>` yang pertama menutup `main-stage` (benar)
- `</div>` ekstra menutup `workspace` terlalu dini
- `<div class="side-panel">` menjadi berada *di luar* `workspace`, sehingga sidebar dan area soal tidak lagi sejajar secara flex-horizontal → sidebar jatuh ke bawah, menimpa konten.

**Perbaikan:** Hapus satu `</div>` ekstra tersebut agar struktur DOM kembali benar:
```
workspace
├── main-stage  (semua slide)
└── side-panel  (sidebar navigasi)
```

---

### Bug 3 — Scrollbar muncul di posisi aneh pada slide Login
**File:** keduanya
**Gejala:** Saat di slide Login (form isi nama, kelas, pengawas), muncul scrollbar di dalam area konten karena kartu login terlalu tinggi, dan efek `justify-content: center` menyebabkan konten keluar batas dari atas.
**Perbaikan:** Ubah default `.center-content-wrapper` dari `justify-content: center` menjadi `justify-content: flex-start`, lalu tambahkan override khusus untuk slide PIN dan Hasil yang memang perlu konten dicentrasi secara vertikal:
```css
.center-content-wrapper { justify-content: flex-start; }
#slide-pin .center-content-wrapper,
#slide-result .center-content-wrapper { justify-content: center; }
```

---

## ✅ Yang Tidak Berubah
- Semua soal, kunci jawaban, dan logika penilaian tidak disentuh.
- URL Apps Script, PIN hash, daftar pengawas, dan konfigurasi lain tetap sama.
- File-file HTML lain (al-islam, bahasa-arab, dst.) belum dikerjakan — masih menggunakan kode lama tanpa perbaikan Sesi 2 & 3.

---

## ⏳ Pekerjaan Berikutnya
Terapkan perubahan yang sama (Sesi 2 + Sesi 3) ke 11 file HTML tersisa:
```
al-islam.html, bahasa-arab.html, bahasa-indonesia.html,
bahasa-sunda.html, ipas.html, kka.html, kmdy.html,
matematika.html, pjok.html, seni-budaya.html, tik.html
```
Setiap file memerlukan 7 perubahan Sesi 2 + fitur A+/A− + 3 perbaikan Bug Sesi 3 di atas, dengan penyesuaian `mapel` dan `STORAGE_KEY`.
