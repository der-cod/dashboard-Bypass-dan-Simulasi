DASHBOARD BYPASS DAN SIMULASI - VERSI PWA
==========================================

ISI PAKET
- index.html, manifest.webmanifest, sw.js, ikon (icon-*.png)
- lib/  : tempat tiga library ekspor Excel/PDF (lihat "Ekspor offline")

SYARAT PWA (penting)
PWA hanya bisa dipasang lewat HTTPS, atau lewat http://localhost.
Dibuka lewat http://alamat-ip-server biasa: halaman tetap bisa dipakai sebagai web biasa,
tetapi tombol "Pasang aplikasi" dan mode offline tidak aktif.

CARA PASANG
1. Letakkan seluruh isi folder ini di satu folder pada web server (semua file sejajar).
2. Opsi hosting:
   a. Hosting statis berHTTPS (Netlify, Cloudflare Pages, GitHub Pages). Paling mudah.
   b. IIS di server sendiri: aktifkan HTTPS dengan sertifikat yang dipercaya perangkat pengguna
      dan tambahkan MIME type .webmanifest = application/manifest+json.
   c. Uji cepat: jalankan "python -m http.server 8000" di folder ini, buka http://localhost:8000
3. Buka alamatnya di Chrome atau Edge, tekan "Pasang aplikasi" (atau menu browser > Instal aplikasi).

TAB DI DALAM APLIKASI
- Aktif sekarang: daftar yang belum dilepas, kolom Keterangan, dan Lepas manual.
- Per tanggal: rincian pada satu tanggal.
- Paling sering: peringkat jumlah kejadian atau total durasi.
- Insight: bypass lama, peralatan berulang, pola jam, sebaran durasi.
- Tren: jumlah aktif per hari, perbandingan dua tanggal, ringkasan per departemen.

IMPOR DBF (MENGGABUNG)
- "Perbarui data (unggah DBF)": pilih SP_Evt.DBF dan/atau MMM_Evt.DBF.
- Isi file DIGABUNG ke salinan tersimpan di browser perangkat itu. Hanya baris yang belum ada yang
  ditambahkan, data lama tidak hilang, dan pelepasan manual tetap berlaku.
- "Ekspor DBF" menulis seluruh data tersimpan ditambah baris pelepasan manual. Simpan sebagai file
  terpisah, jangan menimpa file asli sistem. Ekspor berkala sebagai cadangan, karena data browser
  bisa hilang jika dibersihkan.
- "Kosongkan data unggahan tersimpan" menghapus salinan itu (tekan dua kali).

EKSPOR OFFLINE (Excel dan PDF)
Halaman mencoba folder lib/ dulu, lalu internet (cdnjs). Untuk server tanpa internet, unduh
tiga file di komputer yang punya internet, simpan di lib/ dengan nama persis:
   lib/xlsx.full.min.js              https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js
   lib/jspdf.umd.min.js              https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js
   lib/jspdf.plugin.autotable.min.js https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.8.2/jspdf.plugin.autotable.min.js
Tanpa file ini dan tanpa internet, semua tampilan tetap jalan, hanya ekspor Excel/PDF yang tidak tersedia
(ekspor DBF tetap bisa).

MEMPERBARUI VERSI APLIKASI
Ganti index.html di server. Jika sw.js atau ikon berubah, naikkan nomor versi V di sw.js.

PRIVASI
index.html memuat nama peralatan dan nama user dari event log. Simpan di server sesuai kebijakan perusahaan.
