# agent.md

Nama proyek: **Chrome Lock** (folder `chrome_lock`, arsip `chrome_lock.zip`). README: `README.md`.

Catatan untuk setiap perintah selanjutnya pada proyek ini.

## Proyek
- Nama ekstensi: **Chrome Lock|By @iniozaa._** (diturunkan dari Browser Lock v2.0.4 oleh humbldump).
- Format: folder ekstensi Chrome (Manifest V3), dimuat dengan "Load unpacked".
- Sumber: `chrome.crx` asli dibongkar ke folder ini. Kode di `assets/` sudah dikompilasi dan diperkecil.
- Bahasa komunikasi dengan pengguna: Bahasa Indonesia.

## Perubahan yang sudah dibuat
- `manifest.json`: `short_name` dan `default_title` menjadi "Chrome Lock|By @iniozaa._".
- `_locales/en|es|tr/messages.json`: `full_name` dan `name` menjadi "Chrome Lock|By @iniozaa._".
- `screen.html`: `<title>` menjadi "Chrome Lock|By @iniozaa._".
- `src/assets/icons/{16,24,48,64,128}-logo.png`: diganti dengan gambar kompas emas (transparan, dipotong dan disesuaikan ke persegi). Logo Al-Hikmah sudah tidak dipakai. File ini juga dipakai sebagai logo di layar kunci, halaman update, dan welcome.
- `assets/screen.html-*.js`: ikon perisai di layar kunci (dua versi) diganti dengan logo; header "Browser"+"Lock" menjadi "Raden"+"Ozaa".
- `assets/*.js`: teks tampilan "BrowserLock" / "Browser Lock" menjadi "Chrome Lock|By @iniozaa._".
- `assets/serviceWorker.ts-*.js`:
  - `welcome_url` dan `update_url` diarahkan ke https://www.ozaa.my.id/.
  - `setUninstallURL` dikosongkan, sehingga tidak membuka browserlock.io.
- Auto lock AKTIF (permintaan terbaru): browser terkunci otomatis saat Chrome dibuka lagi (onStartup) dan saat jendela pertama dibuat setelah Chrome ditutup (sessionStorage.auto_locked). Kartu "Auto Lock" di pengaturan disembunyikan, dan `auto_lock.active` selalu dianggap true.
  - `assets/serviceWorker.ts-*.js`: listener `onStartup` terdaftar lagi.
  - `assets/BLLock-*.js`: default `auto_lock.active` = true; pengecekan `active` di `lockTheBrowser` dipaksa true.
- Warna UI disesuaikan dengan kompas emas: semua warna berhue ungu/indigo/biru (200–300°) di CSS dan JS dipindah ke hue emas (42°), kecerahan dipertahankan. Berkas: `assets/*.css`, `assets/*.js`, dan `assets/*.svg`. Juga mencakup nilai `rgb(r g b)` dan halaman `update.html`/`welcome.html`.
- Gaya liquid glass dibatalkan atas permintaan pengguna (blok CSS dihapus). Warna emas tetap dipakai.
- Ikon di layar kunci: tanpa lingkaran/border/crop bulat, bentuk kompas asli (termasuk cincin di atas) ditampilkan utuh. Hanya jarum dan bayangannya yang berputar. Kompas dipisah menjadi dua lapisan: `src/assets/icons/compass-base.png` (kompas diam, jarum sudah di-inpaint) dan `src/assets/icons/compass-needle.png` (hanya jarum). Hanya jarum yang berputar 180° saat hover lewat class `.compass-needle` (CSS di `<head>` `screen.html`). Bayangan jarum dibuat dengan `drop-shadow` pada `.compass-needle` sehingga ikut berputar. Sisa bayangan asli di lapisan diam masih samar; penyempurnaan penuh butuh kompas baru (SVG) yang dibuat dari awal. Wrapper `.compass-wrap` 96x96 px.
- Halaman update dan welcome dihapus. `welcome_url` dan `update_url` di service worker langsung mengarah ke https://www.ozaa.my.id/ (dibuka otomatis, tanpa halaman lokal).

## Yang sengaja TIDAK diubah
- `key:"BrowserLock"` di penyimpanan (persist). Mengubahnya akan menghapus data pengaturan yang sudah tersimpan.
- `https://api.browserlock.io` dan `/api/v2/bl`. Fitur login, kata sandi, dan verifikasi email bergantung pada server ini.
- `start_url` default auto-lock (`https://browserlock.io`). Belum diminta untuk diganti.
- Field `key` atau ID ekstensi: tidak ada di folder unpacked.

## Aturan kerja
- Jangan menyalin atau menampilkan logo lembaga pihak ketiga pada ekstensi tanpa konfirmasi jelas dari pengguna. Teks pada logo tidak boleh diubah menjadi nama lain.
- Setiap perubahan pada `assets/` dicatat di bagian "Perubahan yang sudah dibuat" di file ini.
- Setelah perubahan, zip ulang `chrome_lock` menjadi `chrome_lock.zip` di `/mnt/user-data/outputs/` dan sajikan dengan present_files.
- Pengguna perlu menghapus ekstensi lama dan memuat ulang folder dengan Load unpacked agar perubahan terlihat.
- Jangan mengklaim sebuah perubahan berhasil tanpa memeriksa file hasilnya.
