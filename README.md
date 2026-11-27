# KisiLab — AI-Powered Question Generator

KisiLab adalah aplikasi web untuk membantu guru mengelola kisi-kisi, membuat dan mengedit soal dengan AI, menyimpan bank soal, menyusun paket ujian, mencetak dokumen, serta melakukan backup lokal.

## Penting sebelum deployment

**Untuk mengaktifkan Gemini/OpenAI, deploy melalui repositori GitHub yang dihubungkan ke Netlify.** Netlify Drop/drag-and-drop untuk folder `dist` hanya menerbitkan file statis dan tidak memasang Netlify Functions, sehingga endpoint AI tidak tersedia pada metode itu.

ZIP ini memiliki file proyek langsung di root (tanpa folder pembungkus). Setelah diekstrak, `index.html`, `netlify.toml`, `package.json`, `src/`, dan `netlify/` langsung terlihat.

## Deploy melalui HP (GitHub → Netlify)

1. Ekstrak `KisiLab-Complete-WebApp.zip` di HP.
2. Buat repositori baru di GitHub melalui browser atau aplikasi GitHub.
3. Unggah seluruh isi folder hasil ekstrak ke root repositori, dengan tetap mempertahankan folder `src`, `public`, `netlify`, `docs`, `scripts`, dan `tests`.
4. Buka Netlify, pilih **Add new site → Import an existing project**.
5. Hubungkan GitHub dan pilih repositori KisiLab.
6. Pastikan Build command `npm run build`, Publish directory `dist`, Functions directory `netlify/functions`.
7. Deploy. Netlify akan menjalankan build dan memasang Functions dari `netlify/functions`.
8. Buka URL situs HTTPS yang diberikan Netlify.

Tidak perlu memasukkan API Key ke Netlify, GitHub, atau source code. API Key dimasukkan dari halaman Pengaturan AI di aplikasi.

## Menjalankan dan menguji

Memerlukan Node.js 20 atau lebih baru.

```bash
npm install
npm run dev
npm test
npm run build
npm run preview
```

Build menghasilkan folder `dist/`. Folder itu adalah hasil web statis; source Netlify Functions tetap berada di `netlify/functions/` dan dipasang oleh Netlify saat deployment berbasis Git.

## Mengatur AI

1. Buka menu **Pengaturan AI**.
2. Pilih Google Gemini atau OpenAI.
3. Masukkan API Key dan model yang tersedia pada akun provider.
4. Simpan, lalu tekan **Tes Koneksi**.
5. Setelah koneksi berhasil, gunakan Generator Soal AI, ekstraksi, atau Analisis Soal.

API Key disimpan pada IndexedDB browser dan tidak dienkripsi oleh aplikasi. Saat digunakan, key dikirim melalui HTTPS ke Netlify Function lalu diteruskan ke provider. Fungsi tidak menyimpan key ke database atau log aplikasi. Lindungi perangkat dan jangan memakai browser bersama yang tidak tepercaya.

## Data dan offline

Data KisiLab disimpan pada IndexedDB perangkat. Tidak ada sinkronisasi otomatis antarperangkat. Gunakan Backup & Restore untuk memindahkan data secara manual. AI membutuhkan koneksi internet. Aplikasi shell dan file yang sudah tersimpan dapat tersedia offline setelah pertama kali dibuka; library eksternal dan fitur pembacaan dokumen tertentu memerlukan internet saat pertama kali dipakai.

## Fitur yang belum tersedia / batasan

- Image generation tidak diaktifkan: API key standar Gemini/OpenAI tidak menjamin akses ke model pembuat gambar. Aplikasi menolak permintaan ini secara eksplisit, bukan menampilkan hasil palsu.
- OCR menggunakan Tesseract.js melalui CDN dan memerlukan unduhan model bahasa saat pertama kali digunakan.
- Analisis AI adalah saran, bukan validasi akademik final.
- Penyetaraan kesulitan multi-paket otomatis dan analisis psikometrik statistik butir belum diimplementasikan.
- Ketersediaan model, kuota, harga, dan akses API mengikuti akun/provider masing-masing.
