# Chrome Lock

Ekstensi Chrome untuk mengunci browser dengan password. Berasal dari Browser Lock v2.0.4 (oleh humbldump) dan sudah disesuaikan.

## Fitur

- **Kunci manual** lewat tombol "Lock Browser", menu klik kanan, atau pintasan **Ctrl+M** (Command+M di Mac).
- **Kunci otomatis** saat Chrome dibuka kembali, dan saat jendela pertama dibuat setelah Chrome ditutup. Anda akan diminta memasukkan password.
- **Mode karantina**: setelah beberapa kali password salah, browser dikunci sementara.
- **Tampilan**: nuansa emas, dengan ikon kompas. Jarum kompas berputar saat ikon diarahkan dengan kursor.

## Cara Memasang

1. Ekstrak `chrome_lock.zip`.
2. Buka `chrome://extensions` di Chrome.
3. Aktifkan **Developer mode** di pojok kanan atas.
4. Klik **Load unpacked**, lalu pilih folder `chrome_lock`.

Jika sudah terpasang dan ada perubahan, klik ikon muat ulang pada kartu ekstensi, atau hapus lalu pasang ulang.

## Struktur Folder

```
chrome_lock/
├── manifest.json            konfigurasi ekstensi
├── screen.html              halaman utama (popup dan pengaturan)
├── service-worker-loader.js memuat service worker
├── _locales/                teks dalam bahasa Inggris, Spanyol, dan Turki
├── src/assets/icons/        ikon ekstensi dan logo kompas
├── assets/                  kode aplikasi yang sudah dikompilasi
├── agent.md                 catatan perubahan dan aturan kerja
└── README.md
```

## Catatan Penting

- **Penyimpanan internal** tetap memakai kunci `BrowserLock`, supaya data pengaturan yang sudah ada tidak hilang.
- **Server asli** (`api.browserlock.io`) masih dipakai untuk login, password, dan verifikasi email. Tanpa server ini, fitur tersebut tidak berfungsi.
- **Kartu "Auto Lock"** di pengaturan disembunyikan, karena fitur ini selalu aktif.
- **Halaman pemasangan dan pembaruan** diarahkan ke `https://ozaa.my.id/`.
- Pembaruan dari Chrome Web Store tidak akan berlaku untuk versi ini, karena ID dan kode sudah diubah.

## Kode Asal

Kode di dalam folder `assets/` sudah dikompilasi dan diperkecil. Perubahan tercatat di `agent.md`.

## Kredit

- Browser Lock asli: humbldump
- Pengembangan dan penyesuaian: @iniozaa._
- Situs: https://ozaa.my.id/
